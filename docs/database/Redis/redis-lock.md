## 认识线程锁、进程锁、分布式锁
- **线程锁**: 单线程编程模式下请求是顺序的，一个好处是不需要考虑线程安全、资源竞争问题，因此当你进行 Node.js 编程时，也不会去考虑线程安全问题。那么多线程编程模式下，例如 Java 你可能很熟悉一个词 synchronized，通常也是 Java 中解决并发编程最简单的一种方式，synchronized 可以保证在同一时刻仅有一个线程去执行某个方法或某块代码。
- **进程锁**: 一个服务部署于一台服务器，同时开启多个进程，Node.js 编程中为了利用操作系统资源，根据 CPU 的核心数可以开启多进程模式，这个时候如果对一个共享资源操作还是会遇到资源竞争问题，另外每一个进程都是相互独立的，拥有自己独立的内存空间。关于进程锁通过 Java 中的 synchronized 也很难去解决，synchronized 仅局限于在同一个 JVM 中有效。
- **分布式锁**: 一个服务无论是单线程还是多进程模式，当多机部署、处于分布式环境下对同一共享资源进行操作还是会面临同样的问题。此时就要去引入一个概念分布式锁。如下图所示，由于先读数据在通过业务逻辑修改之后进行 SET 操作，这并不是一个原子操作，当多个客户端对同一资源进行先读后写操作就会引发并发问题，这时就要引入分布式锁去解决，通常也是一个很广泛的解决方案

## 什么是好的分布式锁
- 最好是一把可重入锁，避免死锁
- 最好是一把阻塞锁
- 最好是一把公平锁
- 有高可用的释放锁和获取锁功能
- 获取和释放锁的性能良好

## 超时问题
我们之前设置的超时时间是5秒，但是如果程序执行的逻辑超过了5秒，这样当前线程并没有执行完，其它线程由于拿到了锁也开始执行。此时可能会出现问题。
为了避免这个问题，有两种做法
- redis分布式锁不要用于较长时间的任务。
- 不设置过期时间，而是设置一个watchdog，启动一个定时任务在锁快过期的时候进行续约

## 可重入性
**可重入性是指线程在持有锁的情况下再次请求加锁，如果一个锁支持同一个线程的多次加锁，那么这个锁就是可以重入的。**

## Redis 单实例分布式锁实现

### 上锁
在单实例下，实现分布式锁超级简单，不需要lua脚本，使用一条命令直接搞定
```bash
set key value [EX seconds] [PX milliseconds] [NX|XX]
```
对其中使用到的参数做个说明

- value：建议设置为一个随机值，在释放锁的时候会进一步讲解
- EX seconds：设置的过期时间
- PX milliseconds：也是设置过期时间，单位不一样
- NX|XX：NX 同 setnx 效果是一样的

### 释放锁

在上锁的过程中为了防止锁被误删，可以在锁的名字上加上能够区分不同客户端的标志或者锁变量的值不用true而是用一个唯一值表示。所以在 del key 之前需要先判断这个 key 存在且 value 等于自己指定的值才执行删除操作。判断和删除不是一个原子性的操作，这时候就需借助 Lua 脚本实现。

### demo
```javascript
const Redis = require("ioredis");
const redis = new Redis();
const uuid = require("uuid").v4;

redis.defineCommand("unlock", {
  numberOfKeys: 1,
  lua: `
  if redis.call("get",KEYS[1]) == ARGV[1] then
    return redis.call("del",KEYS[1])
  else
    return 0
  end
  `,
});

async function main() {

  // 上锁
  const key = 'key';
  const value = uuid();
  const lock_time = 5;
  if (await redis.set(key, value, 'ex', lock_time, 'nx') === 'OK') {
    console.log('上锁成功！')
  }
  if (await redis.set(key, value, 'ex', lock_time, 'nx') !== 'OK') {
    console.log('上锁失败！')
  }
  
  // 解锁
  if (await redis.unlock(key, uuid()) !== 1) {
    console.log('解锁失败！')
  }
  if (await redis.unlock(key, value) === 1) {
    console.log('解锁成功！')
  }
}

main().then(process.exit);
```
**注意：**
- 上面代码的中获取不到锁就直接失败，不能阻塞，实际使用可以在获取不到锁的情况下每间隔一段时间重新尝试获取锁，但是这样无法保证先获取失败的先获取到锁，使用zookeeper实现分布式锁可以实现这个需求，获取不到锁的情况可以阻塞，并且后面的请求按照顺序获得上一个释放的锁。
- 对于释放锁是否需要lua脚本，还有一种简单的实现方法是这样:
```javascript
  if (value === await redis.get(key)) {
    await redis.del(key)
  }
```

## Redis 多实例分布式锁实现/Redlock 算法
先了解下Redis单实例实现分布式锁的问题

**因为Redis节点之间数据并不是强一致性的，会存在延迟。当主节点上锁后，数据还没同步到从节点，此时进行主从节点的切换，那么这个锁就会丢失了。**


如何解决这个问题呢？Redis 提供的解决方案就是Redlock算法。http://redis.cn/topics/distlock.html

**算法思想：**
Redlock 在上述文档也有描述，这里简单做个总结：Redlock 在 Redis 单实例或多实例中提供了强有力的保障，本身具备容错能力，它会从 N 个实例使用相同的 key、随机值尝试 set key value [EX seconds] [PX milliseconds] [NX|XX] 命令去获取锁，在**有效时间**内至少 N/2+1 个 Redis 实例取到锁，此时就认为取锁成功，否则取锁失败，失败情况下客户端应该在所有的 Redis 实例上进行解锁。
> 有效时间：记录加锁的时间，如果加锁时间超过了过长，则对所有节点释放锁操

虽然看起来流程复杂，但是各个语言也早有封装好的包，直接使用即可，nodejs可使用这个：https://www.npmjs.com/package/redlock