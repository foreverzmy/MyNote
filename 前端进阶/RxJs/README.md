# What is RxJs

说道 RxJx 就要说 Reactive Programming（响应式编程），RxJx 就是它的 js 版本的实现，全称是 ReactiveX ，是使用 Observable 序列来进行异步编程的库，提供一系列方法来操作 Observable ，使异步编程或基于回调的代码更容易。

# 什么是 Reactive Programming

其实 Reactive Programming 就是处理异步数据流。在 js 中的各种事件都是异步事件流，可以对它们进行监听，然后做出相应的响应。而 Reactive 则把是把这种行为给扩展了，不仅把各种事件当做 stream ， 而是把所有东西都可以当作一个 stream ：比如变量，用户的输入，属性，缓存，数据结构等等。你可以监听他们，然后做出响应。

在此基础上，你可以使用很多非常棒的函数，比如可以 combine ，create，filter 各种各样的 stream ，因为 Rx 借鉴了函数式编程。一个 stream 可以当作另一个 stream 的输入（input）。甚至多个 stream 也能当作另外一个 stream 的输入。而且，你可以合并（merge）两个 stream 。你也可以把一个 stream 里你只感兴趣的事件 filter 到另外一个 stream 。你还可以把一个 stream 中的数据映射（map）到另外一个 stream 中。

# 为什么使用 RxJs

JavaScript 经常说的异步回调地狱是非常麻烦的，陷入回调地狱的代码是非常差的代码，非常容易出错并且难以读懂，使用 RxJs 就可以优雅的避开这种回调。而且 RxJs 比 Promise 更加的方便和更能强大。

# RxJS 的基本概念

* Observable 可观察对象：表示一个可调用的未来值或者事件的集合。
* Observer 观察者：一个回调函数集合,它知道怎样去监听被Observable发送的值
* Subscription 订阅： 表示一个可观察对象的执行，主要用于取消执行。
* Operators 操作符： 纯粹的函数，使得以函数编程的方式处理集合比如:map,filter,contact,flatmap。
* Subject (主题)：等同于一个事件驱动器，是将一个值或者事件广播到多个观察者的唯一途径。
* Schedulers (调度者)： 用来控制并发，当计算发生的时候允许我们协调，比如 setTimeout , requestAnimationFrame

[ rxjs 官方文档中文翻译](https://buctwbzs.gitbooks.io/rxjs/)