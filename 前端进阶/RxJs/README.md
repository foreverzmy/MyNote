# What is RxJs

说道 RxJx 就要说 Reactive Programming（响应式编程），RxJx 就是它的 js 版本的实现。

# 什么是 Reactive Programming

其实 Reactive Programming 就是处理异步数据流。在 js 中的各种事件都是异步事件流，可以对它们进行监听，然后做出相应的响应。而 Reactive 则把是把这种行为给扩展了，不仅把各种事件当做 stream ， 而是把所有东西都可以当作一个 stream ：比如变量，用户的输入，属性，缓存，数据结构等等。你可以监听他们，然后做出响应。

在此基础上，你可以使用很多非常棒的函数，比如可以 combine ，create，filter 各种各样的 stream ，因为 Rx 借鉴了函数式编程。一个 stream 可以当作另一个 stream 的输入（input）。甚至多个 stream 也能当作另外一个 stream 的输入。而且，你可以合并（merge）两个 stream 。你也可以把一个 stream 里你只感兴趣的事件 filter 到另外一个 stream 。你还可以把一个 stream 中的数据映射（map）到另外一个 stream 中。
