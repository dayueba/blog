面试的时候问到闭包，会问到不合理的使用闭包有什么缺点，答案是内存泄漏。

## JS 内存生命周期
每一门语言都有自己的内存管理机制，这是一种基本能力。

区别在于，一些语言会将这种能力开放 —— 比如 C 语言中的 malloc() 和 free() 方法 ，这些方法的暴露，使得开发者能够切身感受到内存管理这件事情的存在。

而在另一些语言 —— 比如 JS 中，这种能力是被 “隐藏” 了的：JS 并没有暴露任何内存操作给开发者，而是自己默默地自动完成了所有的管理动作。这是 JS 内存管理不被大多数同学所重视的原因。

JS 的内存生命周期，和大多数程序语言一样，分为三个阶段。
1. 分配内存
2. 在分配的内存里存入数据，此后可以修改以及读取
3. 释放内存

## 栈内存与堆内存

**基本类型和引用类型**
JS 中的数据类型，整体上来说只有两类：基本类型和引用类型。

其中基本类型包括：Sting、Number、Boolean、null、undefined、Symbol。这类型的数据最明显的特征是大小固定、体积轻量、相对简单，它们被放在 JS 的栈内存里存储。

而排除掉基本类型，剩下的数据类型就是引用类型，比如 Object、Array、Function 等等等等。这类数据比较复杂、占用空间较大、且大小不定，它们被放在 JS 的堆内存里存储。

**图解堆与栈**
和栈分别是不同的数据结构。栈是线性表的一种，而堆则是树形结构。

![](https://img1.sycdn.imooc.com/5e66f52e0001bc2711160686.png)

在访问 a、b、c 三个变量时，过程非常简单：从栈中直接获取该变量的值。

而在访问 d 和 e 时，则需要分两步走：

1. 从栈中获取变量对应对象的引用（即它在堆内存中的地址）
2. 拿着 1 中获取到的地址，再去堆内存空间查询，才能拿到我们想要的数据

## 垃圾回收机制
在 JS 中，我们讨论的垃圾回收算法有两种 —— 引用计数法和标记清除法。

**引用计数法**
这是最初级的垃圾回收算法，它在现代浏览器里几乎已经被淘汰得干干净净，但是仍有一些面试官执着于询问该方法的思路、以便于判断你对 JS 的了解是否足够全面和深入。

在引用计数法的机制下，内存中的每一个值都会对应一个引用计数。当垃圾收集器感知到某个值的引用计数为 0 时，就判断它 “没用” 了，随即这块内存就会被释放。

引用计数法为啥被淘汰
```javascript
function badCycle() {
  var cycleObj1 = {}
  var cycleObj2 = {}
  cycleObj1.target = cycleObj2
  cycleObj2.target = cycleObj1
}

badCycle()
```
在代码第 8 行，我们执行了 badCycle 这个函数。大家知道，函数作用域的生命非常短暂，当函数执行完之后，作用域内的变量也会全部被视作 “垃圾” 进而移除。

但如果咱们用了引用计数法，那么即使 badCycle 执行完毕，cycleObj1 和 cycleObj2 还是会活得好好的 —— 因为 cycleObj2 的引用计数为 1（cycleObj1.target），而 cycleObj1 的引用计数也为 1 （cycleObj2.target）（如下图）。

![](https://img1.sycdn.imooc.com/5e66f5630001067710400236.png)

没错，引用计数法无法甄别循环引用场景下的 “垃圾”！

如果任由 cycleObj1、cycleObj2 这样的变量肆虐内存，那么内存泄漏将是不可避免的结局。

标记清除法

在标记清除算法中，一个变量是否被需要的判断标准，是它是否可抵达 。

这个算法有两个阶段，分别是标记阶段和清除阶段：

- 标记阶段：垃圾收集器会先找到根对象，在浏览器里，根对象是 Window；在 Node 里，根对象是 Global。从根对象出发，垃圾收集器会扫描所有可以通过根对象触及的变量，这些对象会被标记为 “可抵达”。
- 清除阶段： 没有被标记为 “可抵达” 的变量，就会被认为是不需要的变量，这波变量会被清除

现在大家按照标记清除法的思路，再来看这段代码：

```javascript
function badCycle() {
  var cycleObj1 = {}
  var cycleObj2 = {}
  cycleObj1.target = cycleObj2
  cycleObj2.target = cycleObj1
}

badCycle()
```
badCycle 执行完毕后，从根对象 Window 出发，cycleObj1 和 cycleObj2 都会被识别为不可达的对象，它们会按照预期被清除掉。这样一来，循环引用的问题，就被标记清除干脆地解决掉了。

## 闭包与内存泄漏
### 什么是内存泄露
该释放的变量（内存垃圾）没有被释放，仍然霸占着原有的内存不松手，导致内存占用不断攀高，带来性能恶化、系统崩溃等一系列问题，这种现象就叫内存泄漏。

事实上，单纯由闭包导致的内存泄漏，极少极少（除非你的操作极其不规范，但那就不是闭包的问题了，是代码写得有问题）。真正导致内存泄漏的原因，我们还需要从其他方面来看

面试官未必会直接问你 “闭包是如何导致内存泄漏的？”（如果他是一个足够严谨的工程师，想必也不会这样问），而更倾向于让你 “看代码找问题”。在 “有问题” 的代码里，最为大家所津津乐道的其实是 “theThing” 问题。也就是下面这段流传已久的代码：

```javascript
var theThing = null;
var replaceThing = function () {
  var originalThing = theThing;
  var unused = function () {
    if (originalThing) // 'originalThing'的引用
      console.log("嘿嘿嘿");
  };
  theThing = {
    longStr: new Array(1000000).join('*'),
    someMethod: function () {
      console.log("哈哈哈");
    }
  };
};
setInterval(replaceThing, 1000);
```

思考：上面这段代码有什么问题？

要想揪出其中的问题，大家需要对 V8 引擎有所了解，尤其是这一点：在 V8 中，一旦不同的作用域位于同一个父级作用域下，那么它们会共享这个父级作用域。

在这段代码里， unused 是一个不会被使用的闭包，但和它共享同一个父级作用域的 someMethod，则是一个 “可抵达”（也就意味着可以被使用）的闭包。unused 引用了 originalThing，这导致和它共享作用域的 someMethod 也间接地引用了 originalThing。结果就是 someMethod “被迫” 产生了对 originalThing 的持续引用，originalThing 虽然没有任何意义和作用，却永远不会被回收。不仅如此，originalThing 每次 setInterval 都会改变一次指向（指向最近一次的 theThing 赋值结果），这导致无法被回收的无用 originalThing 越堆积越多，最终导致严重的内存泄漏。

### 内存泄漏成因分析
除了上面分析这种情况，可能导致内存泄漏的因素，还可以考虑以下几点：

“手滑” 导致的全局变量
```javascript
function test() {
  me = 'xiuyan'
}
```
当你在非严格模式下写代码时，me 而非 var me 这种写法，会导致这个 me 被默默地挂载到全局对象上。

根据我们前面所讲的垃圾回收策略，本来 me 这个变量，如果被 var 声明过，它作为函数作用域内的变量，在函数调用结束后就会消失 —— 这也是我们所期望的。但现在它是一个全局变量了，永远无法被清除。这样的变量一多，问题就来了。

忘记清除的 setInterval 和 setTimeout

我们在实现轮询效果时，会用到 setInterval：

```js
setInterval(function() {
    // 函数体
}, 1000);
```

或者链式调用 setTimeout：

```js
setTimeout(function() {
  // 函数体
  setTimeout(arguments.callee, 1000);
}, 1000)
```

在 setInterval 和链式调用的 setTimeout 这两种场景下，定时器的工作可以说都是无穷无尽的。当定时器囊括的函数逻辑不再被需要、而我们又忘记手动清除定时器时，它们就会永远保持对内存的占用。因此当我们使用定时器时，一定要先问问自己：我打算什么时候干掉这玩意儿？