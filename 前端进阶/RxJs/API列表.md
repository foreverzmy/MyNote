

| 方法 | 用法 | 作用 |
|:----|:----|:---|
| Rx.Observable | | 创建一个可观察对象 |
| bindCallback | Rx.Observable.bindCallback(jQuery.getJSON); | 将一个回调函数API转化为一个能返回一个Observable的函数 |
| bindNodeCallback | Rx.Observable.bindNodeCallback(fs.readFile); | 将一个NodeJS风格的回调函数API转化为一个能返回可观察对象的函数 |
| combineLatest | Rx.Observable.combineLatest(obsX, obsY, (x, y) => x + y); | 组合多个Observable产生一个新的Observable，其发射的值根据其每个输入Observable的最新值计算 |
| concat | Rx.Observable.concat(observableX, observableY); | 产生一个Observable，它取作为参数的 Observable 发射的每个值，并顺序(基于作为输入的可观察对象的顺序)发出所有值 |
| create | Rx.Observable.create(obs => { obs.next(1) }); | 创建一个新的Observable，当被订阅时，它将执行指定的函数 |
| defer | Rx.Observable.defer(() => Rx.Observable.of()); | 参数为一个Observable工厂函数，当被订阅时工厂函数被调用产生一个可观察对象 |
| empty | Rx.Observable.empty(); | 创建一个不发射任何值的Observable,它只会发射一个complate通知 |
| forkJoin | Rx.Observable.forkJoin(...args); |  并行运行所有可观察序列并收集其最后的元素 |
| from | Rx.Observable.from([10,20,30]); | 将一个数组、类数组(字符串也可以)，Promise、可迭代对象，类可观察对象、转化为一个Observable |
| fromEvent | Rx.Observable.fromEvent(element, 'click'); | 将一个元素上的事件转化为一个Observable |
| fromEventPattern | Rx.Observable.fromEventPattern(addClickHandler, removeClickHandler); | 通过使用addHandler和removeHandler函数添加和删除处理程序。 当输出Observable被订阅时，addHandler被调用，并且当订阅被取消订阅时调用removeHandler |
| fromPromise | Rx.Observable.fromPromise(fetch('http://myserver.com/')); | 转化一个Promise为一个Obseervable |
| interval | Rx.Observable.interval(1000); | 返回一个以周期性的、递增的方式发射值的Observable |
| merge | Rx.Observable.merge(obs1, obs2, obs3, concurrent); | 创建一个发射所有被合并的observable所发射的值。 |
| never | Rx.Observable.never(); | 创建一个不发射任何值的Observable |
| of | Rx.Observable.of(1, 2, 3); | 创建一个Observable，发射指定参数的值，一个接一个，最后发出complate |
| range | Rx.Observable.range(1, 10); | 创建发射一个数字序列的 observable |
| throw | Rx.Observable.throw(new Error('oops!')); | 创建一个只发出error通知的Observable |
| timer | Rx.Observable.timer(3000, 1000); | 类似于interval,但是第一个参数用来设置发射第一个值得延迟时间 |
| toAsync | const fun = Rx.Observable.toAsync((x, y) => return x + y); func(3,4) | 将函数转换为异步函数。生成的异步函数的每次调用都会导致调用指定调度程序上的原始同步函数 |
| using |  |  |
| when |  |  |
| while |  |  |
| webSocket |  |  |
| zip |  |  |

