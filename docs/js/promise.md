异步解决方案
- 事件监听
- 发布订阅
- 回调函数
- promise
- generator
- async/await

## Promise相关面试题
### 说说你理解的 Promise
答题时务必囊括以下几个要点：**代理对象、三个状态、状态切换机制**

Promise 对象是一个代理对象。它接受你传入的 executor（执行器）作为入参，允许你把异步任务的成功和失败分别绑定到对应的处理方法上去。一个 Promise 实例有三种状态：

- pending 状态，表示进行中。这是 Promise 实例创建后的一个初始态；
- fulfilled 状态，表示成功完成。这是我们在执行器中调用 resolve 后，达成的状态；
- rejected 状态，表示操作失败、被拒绝。这是我们在执行器中调用 reject后，达成的状态；

Promise实例的状态是可以改变的，但它只允许被改变一次。当我们的实例状态从 pending 切换为 rejected 后，就无法再扭转为 fulfilled，反之同理。当 Promise 的状态为 resolved 时，会触发其对应的 then 方法入参里的 onfulfilled 函数；当 Promise 的状态为 rejected 时，会触发其对应的 then 方法入参里的 onrejected 函数。

### Promise 常见方法有哪些
- Promise.all(iterable)：这个方法返回一个新的 promise 对象，该 promise 对象在 iterable 参数对象里所有的 promise 对象都成功的时候才会触发成功，一旦有任何一个 iterable 里面的 promise 对象失败则立即触发该 promise 对象的失败。
- Promise.race(iterable)：当 iterable 参数里的任意一个子 promise 被成功或失败后，父 promise 马上也会用子 promise 的成功返回值或失败详情作为参数调用父 promise 绑定的相应处理函数，并返回该 promise 对象。
- Promise.reject(reason)： 返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法
- Promise.resolve(value)：它返回一个 Promise 对象，但是这个对象的状态由你传入的value决定，情形分以下两种：
    - 如果传入的是一个带有 then 方法的对象（我们称为 thenable 对象），返回的Promise对象的最终状态由then方法执行决定
    - 否则的话，返回的 Promise 对象状态为 fulfilled，同时这里的 value 会作为 then 方法中指定的 onfulfilled 的入参

### 看代码得输出结果
第一题
```js
const promise = new Promise((resolve, reject) => {
  resolve('第 1 次 resolve')
  console.log('resolve后的普通逻辑')
  reject('error')
  resolve('第 2 次 resolve')
})
 
promise
.then((res) => {
  console.log('then: ', res)
})
.catch((err) => {
  console.log('catch: ', err)
})
```
运行结果
```
resolve后的普通逻辑
then:  第 1 次 resolve
```

考点点拨：Promise 对象的状态只能被改变一次

分析：这段代码里，promise 初始状态为 pending，我们在函数体第一行就用 resolve 把它置为了 fulfilled 态。这个切换完成后，后续所有尝试进一步作状态切换的动作全部不生效，所以后续的 reject、resolve大家直接忽略掉就好；需要注意的是，我们忽略的是第一次 resolve 后的 reject、resolve，而不是忽略它身后的所有代码。因此 console.log(‘resolve后的普通逻辑’) 这句，仍然可以正常被执行。至于这里为啥它输出在 ”then: 第 1 次 resolve“ 的前面，原因和真题1是一样一样的~

第二题
```js
Promise.resolve(1)
  .then(Promise.resolve(2))
  .then(3)
  .then()
  .then(console.log)
```
运行结果：
```
1
```

考点点拨：Promise 值穿透问题

分析：大家知道，then 方法里允许我们传入两个参数：onFulfilled（成功态的处理函数）和 onRejected（失败态的处理函数）。

你可以两者都传，也可以只传前者或者后者。但是无论如何，then 方法的入参只能是函数。万一你想塞给它一些乱七八糟的东西，它就会“翻脸不认人”。

具体到我们这个题里，第一个 then 方法中传入的是一个 Promise 对象，then 说：”我不认识“；第二个 then 中传入的是一个数字， then 继续说”我不认识“；第四个干脆啥也没穿，then 说”入参undefined了，拜拜“；直到第五个入参，一个函数被传了进来，then 哭了：”终于等到一个我能处理的！“，于是只有最后一个入参生效了。

在这个过程中，我们最初 resolve 出来那个值，穿越了一个又一个无效的 then 调用，就好像是这些 then 调用都是透明的、不存在的一样，因此这种情形我们也形象地称它是 Promise 的“值穿透”

