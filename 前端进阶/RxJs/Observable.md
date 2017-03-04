# 观察者 ( Observer ) 模式

Observer 模式是一种设计模式，其中一个对象 (称为 subject )维持一系列依赖与它的对象，将有关状态的人格变更自动通知给他们。

观察者模式在 Web 中最常见的应该是 DOM 事件的监听和触发。

* 订阅：通过 `addEventListener` 订阅 `document.body` 的 `click` 事件。
* 发布：当 `body` 节点被点击时，`body` 节点便会向订阅者发布这个消息。

```javascript
document.body.addEventListener('click', function listener(e) {
  console.log(e);
},false);

document.body.click(); // 模拟用户点击
```

将上述例子抽象模型，并对应通用的观察者模型

![](http://static.open-open.com/lib/uploadImg/20161102/20161102101109_17.png)

# Observable

* Observable 用于观察数据流并在值、错误或完成时发射函数，并将这些值传入函数;
* Observable 可以通过 Observer 来订阅;
* Observable 会持续观察数据流并及时进行相应更新
* 可以与数据流进行交互


## 创建 Observable

有好多种方式创建 Observable ，但是最常见的方式之一就是通过 `create` 操作符。在 `Rx.Observalbe` 对象的 `create` 操作符中需要传递一个回调函数，这个回调函数中需要传递一个订阅者参数（ Observer ，相当于传统观察者模式中的 listener ）。在这个方法中定义了 Observable 如何发射值，下面就举个例子来说明：

```javascript
var observable = Rx.Observable.create(function(observer) {
  observer.onNext('Simon');
  observer.onNext('Jen');
  observer.onNext('Sergi');
  observer.onCompleted(); // 成功完成
});
```

当我们订阅这个 `Observable` ，它通过调用 `onNext()` 发射三个字符串给他的订阅者（监听者），最后调用 `onCompleted()` 标识这个序列完成了。

## observer

我们是如何准确的订阅一个 `Observable` ？通过 `Observers`（也就是订阅者);

observers 监听 observable ，不论何时在 Observable 中发生了什么事件，它会调用它的 observers 中相应的方法。

observers有三个方法：

* `onNext`：当 observable 发射了一个新值它就会被调用。
* `onCompleted`：再没有任何有效数据的信号时被调用，在 onCompleted 被调用后，之后的 onNext 调用将会无效。
* `onError`：当 observable 中发生了错误后将会被调用，在 onError 被调用后，之后的 onNext 调用将会无效。 