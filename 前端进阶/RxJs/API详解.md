# RxJS API

## Observable

### Observable.amb

方法定义：

```js
Rx.Observable.amb(...args)
```

* 作用：从一系列流中，订阅最先发射的值的可观察对象并忽略其他的可观察对象。

* 参数 `args` (Array|arguments)：方法参数为多个可观察对象（流），或者是Promise对象，对象间存在竞争关系。

* 返回值 (Observable) ：方法返回呈竞争态的多个可观察对象中，首先发射的可观察对象。

函数需要做出选择 ，选择的依据就是哪一个可观察对象（流）先发射了值。选择后，仅有“联通”的可观察对象会被观察到。

* 示例代码：

```js
const source = Rx.Observable.amb(
  Rx.Observable
    .fromEvent(input1, 'click')
    .map(()=>'one'),
  Rx.Observable
    .fromEvent(input2, 'click')
    .map(()=>'two')
);
const subscription = source.subscribe(
  x => console.log(x),
  err => console.log('Error: ' + err),
  () => console.log('Completed'),
);
```

### Observable.case

方法定义：

```js
Rx.Observable.case(selector, sources, [elseSource|scheduler])
```

* 作用：选择序列中特定可观察对象进行订阅，在特定可观察对象不存在的情况下，返回传入的默认可观察对象。

* 参数：

  1. selector (Function): 返回键的字符串的函数，键用以与sources中的键名进行比较。
  2. sources (Object): 一个包含可观察对象的Javascript对象。
  3. [elseSource|scheduler] (Observable | Scheduler):当selector无法匹配sources时，该对象被默认返回。 如果没有明确指定，将返回附加了指定scheduler的Rx.Observabe.empty 对象。

* 返回值 (Observable): 返回值为经过选择后的 Observable（可观察对象）。

* 示例代码：

```js
const sources = {
  hello: Rx.Observable.just('clx'),
  world: Rx.Observable.just('wxq') 
};

const subscription = Rx.Observable.case(()=>"hello", sources, Rx.Observable.empty())

subscription.subscribe(x => console.log(x));
```

示例中，匿名函数 `()=>"hello"` 指定需要在sources中返回的可观察对象的键名为 `hello` ，命令行最终输出 `clx` 。

### Observable.catch

方法定义：

```js
Rx.Observable.catch(...args)
```

* 作用：序列中可观察对象因为异常而被终止后，继续订阅序列中的其他可观察对象。

* 参数 args (Array | arguments): 可观察对象序列。

* 返回值 (Observable): 可观察对象序列中能够正确终止，不抛出异常的第一个可观察对象。

* 示例代码

```js
const obs1 = Rx.Observable.throw(new Error('error'));
const obs2 = Rx.Observable.return(42);

const source = Rx.Observable.catch(obs1, obs2);

const subscription = source.subscribe(
  x => console.log(`onNext: ${x}`),
  e => console.log(`onError: ${e}`),
  () => console.log('onCompleted'));
```

在订阅时， obs1 抛出错误后，程序继续执行，转而输出没有异常的 obs2 ，并输出 obs2 发射的值 42。


### Observable.combineLatest

方法定义

```js
Rx.Observable.combineLatest(...args, [resultSelector])
```

* 作用：通过处理函数总是将指定的可观察对象序列中最新发射的值合并为一个可观察对象。

* 参数：
  1. args (arguments | Array): 一系列可观察对象或可观察对象的数组。
  2. [resultSelector] (Function): 在所有可观察对象都发射值后调用的处理函数。

*返回值 (Observable): 由传入的可观察序列经过处理函数合并后的结果组成的可观察序列。


`Observable.combineLastest()` 函数，总是合并序列中最新发射的值。

* 示例代码：

```js
const colors = ["紫色","黄色","蓝色","黑色"];
const shapes = ["小星星","圆形","三角形","正方形","心形","五边形"];
const source1 = Rx.Observable
  .interval(3000)
  .map(()=>colors.pop());
const source2 = Rx.Observable
  .interval(2000)
  .map(()=>shapes.pop());

const combined = Rx.Observable
  .combineLatest(source1, source2, 
    (x, y) => {
      return x + "的" + y
    },
  })
  .take(8);

combined.subscribe((shaped)=>console.log(shaped));
```

输出结果为：

```js
"黑色的五边形"
"黑色的心形"
"蓝色的心形"
"蓝色的正方形"
"蓝色的三角形"
"黄色的三角形"
"黄色的圆形"
"紫色的圆形"
```
