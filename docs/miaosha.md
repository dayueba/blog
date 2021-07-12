<!-- TOC -->
- [秒杀项目的介绍](#秒杀项目的介绍)
- [秒杀设计](#秒杀设计)
  - [库存预热](#库存预热)
  - [防止超卖](#防止超卖)
  - [流量削峰](#流量削峰)
- [扩展](#扩展)
  - [限购](#限购)
  - [限流](#限流)
  - [防止链接暴露](#防止链接暴露)
  - [服务单一原则](#服务单一原则)
  - [Nginx](#Nginx)
  - [Redis集群](#Redis集群)
- [前端优化](#前端优化)
- [总结](#总结)
<!-- /TOC -->

## 秒杀项目的介绍
秒杀的本质，就是对库存的抢夺。在用户并发量极高的情况下，每个秒杀的用户都去数据库中查库存，减库存，会导致数据库的奔溃。同时秒杀还有时间极短的特点。

## 秒杀设计
针对秒杀项目的特点以及主要问题，来设计项目


### 库存预热
秒杀项目首先最重要的是要抗的住秒杀时间内的用户并发量
> MySQL单机能够支持1000QPS，Redis单机能支持10wQPS，QPS：每秒请求次数

所以防止每个请求都访问MySQL，我们需要将库存信息加载到Redis中，直接通过Redis来判断并扣减库存。

### 防止超卖
电商项目中都需要防止超卖，有时候面试时也会问这个问题

由于我们直接扣减Redis中库存，所以需要防止Redis中的库存变为负数

现在主要问题是，Redis服务涉及两个操作，一个是查看库存是否大于0，二是库存减一，所以解决思路就是将讲个操作合二为一。

解决办法：可以使用Redis事务，但是Lua脚本更加强大。所以这里选择使用Lua脚本

> Lua脚本是Redis2.6版本推出的，通过内嵌对Lua环境的支持，Redis解决了长久以来不能高效处理CAS命令的缺点，并且可以通过组合多个命令，轻松实现以前很难实现或不能高效实现的模式。
>
> Lua脚本是类似于Redis事务，有一定的原子性，不会被其它命令插队，可以完成一些Redis事务性操作

```
// 例子
if (redis.call('exists', KEYS[1]=1)) then
  local stock = tonumber(redis.call('get', KEYS[1]));
  if (stock <= 0)
    return -1;
  end;
  redis.call('decr', KEYS[1]);
  return stock - 1;
end;
return -1;
```

> 为了更加安全，也可以在MySQL再判断一次是否超库存，可以使用事务，也可以直接使用行锁
> 
> 使用行锁的例子：update miaosha_goods set miaosha_stock = miaosha_stock - 1 where goods_id = 1 and miaosha_stock > 0 

### 流量削峰
以上的设计可以解决秒杀商品较少的情况，但是如果是秒杀商品数量较大，比如纸巾等商品，秒杀数据达到10w。10w个请求知道到MySQL中，MySQL还是抗不住。

所以这时候需要消息队列来进行一个削峰
> 消息队列的介绍，可以看另一篇文章：[消息队列总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/message-queue)


## 扩展

### 限购
一人限购N个

方法1: MySQL数据校验，可以在扣减库存后，生成订单前根据user_id和goods_id，判断是否超过数量

方法2: Redis数据校验，维护一个记录秒杀成功的用户集合，判断用户是否已经秒杀成功过

### 限流

限流的作用和意义：**防止恶意请求以及爬虫**
1. 设置用户黑名单，IP黑名单
2. 当库存为0时，直接拒绝后面当所有请求

### 防止链接暴露
url动态化，秒杀链接加盐。

例子：

![链接](https://cdn.nlark.com/yuque/0/2020/png/1416082/1593670232027-284fbc30-5b4d-4287-968b-fe4963f55efa.png)

### 服务单一原则
微服务的思想，为秒杀创建单独的服务以及单独的数据库。
就算秒杀服务挂了，也不影响其它服务

### Nginx
利用**负载均衡**缓解服务器压力

恶意请求拦截也需要用到它，一般单个用户请求次数太夸张，不像人为的请求在网关那一层就得拦截掉了，不然请求多了他抢不抢得到是一回事，服务器压力上去了，可能占用网络带宽或者把**服务器打崩、缓存击穿**等等。

### Redis集群
添加Redis服务, 提高并发能力

## 前端优化
项目主要针对后端，所以前端优化就简单提一下。
1. 点击秒杀按钮后一段时间内将按钮置灰，无法点击
2. 可以将部分请求直接跳转到繁忙页
3. 秒杀活动未开始前，禁用秒杀按钮
4. 添加验证码，防止爬虫
5. 资源静态化，利用cdn

## 总结
以上是一个简单的秒杀项目设计思路。项目是单机版，分布式系统还需要考虑分布式事务等。