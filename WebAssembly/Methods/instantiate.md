# WebAssembly.instantiate()

该函数是用于编译和实例化 WebAssembly 代码的主要API。 此功能有两个重载：

    主要重载采用 WebAssembly 二进制代码，以类型化的数组或 ArrayBuffer 的形式，并在一个步骤中同时执行编译和实例化。resolve 的 Promise 为编译的 `WebAssembly.Module` 及其第一个 `WebAssembly.Instance`。

    次要重载采用已编译的 `WebAssembly.Module`，并 resolve 一个解析为该模块的实例的 Promise。 如果模块已经从高速缓存中进行了编译或检索，这个重载是很有用的。


## 主要重载 - 采用二进制代码

* 用法：

  ```ts
  Promise<ResultObject> WebAssembly.instantiate(bufferSource, importObject);
  ```

* 参数：

  `bufferSource`：一个包含要编译的 `.wasm` 模块的二进制代码的类型数组或ArrayBuffer。

  `importObject`：包含要导入到新创建的实例中的值的对象，例如函数或 `WebAssembly.Memory` 对象。每个声明导入的编译模块必须有一个匹配的属性，否则会抛出一个 `WebAssembly.LinkError`。

* 返回值

  resolve 一个包含以下两个字段的 ResultObject 的 Promise.

  module：表示编译的 WebAssembly 模块的 `WebAssembly.Module` 对象。 此模块可以再次实例化，通过 `postMessage()` 或在IndexedDB中缓存 共享。

  instance：包含所有导出的 WebAssembly 函数的 `WebAssembly.Instance` 对象。

* 注意：

  如果任一参数不是正确的类型或结构，则抛出 TypeError。

  如果操作失败，Promise 会 reject 一个 `WebAssembly.CompileError`、`WebAssembly.LinkError` 或 `WebAssembly.RuntimeError`，具体取决于失败的原因。

## 二次重载 - 采用模块对象实例

* 用法：

  ```ts
  Promise<WebAssembly.Instance> WebAssembly.instantiate(module, importObject);
  ```

* 参数：

  `module`：要实例化的 `WebAssembly.Module` 对象。

  `importObjec`：包含要导入到新创建的实例中的值的对象，例如函数或 `WebAssembly.Memory` 对象。每个声明的模块导入必须有一个匹配的属性，否则会抛出一个 `WebAssembly.LinkError`。

* 返回值：
  resolve 一个 `WebAssembly.Instance` 对象的 Promis。

* 注意：

  如果任一参数不是正确的类型或结构，则抛出 TypeError。

  如果操作失败，Promise 会 reject 一个 `WebAssembly.CompileError`、`WebAssembly.LinkError` 或 `WebAssembly.RuntimeError`，具体取决于失败的原因。

  在 C 文件中通过 `extern` 的形式导入 js 变量和函数，但是导入的变量和函数必须在对象 `importObjec` 的 `env` 属性中，因为 C 中默认 `extern` 读取的是 `env` 对象中的属性和方法。

  在 C++ 中函数要写在 `extern "C"{}` 中，因为 C++ 有重载的概念，会把定义的方法名编译，前后加上字符串，函数名变得不可测，写入 `extern "C"{}` 会按照 C 的方式编译，函数名不变。

## 例子

二次重载：

```ts
import * as fs from 'fs';
import { EventEmitter } from 'events';

const path = './addOne.wasm';
const buffer = fs.readFileSync(path);

const emitter = new EventEmitter();

WebAssembly.compile(buffer).then(mod => emitter.emit('mod', mod));

const importObject = {
  env: {
    addOne: function (arg) {
      return arg + 1;
    }
  }
};

emitter.addListener('mod', mod => {
  console.log('module received from main thread');
  WebAssembly.instantiate(mod, importObject)
    .then((instance: any) => {
      const result = instance.exports.add(4, 5);
      console.log(result);
    });
  const exports = WebAssembly.Module.exports(mod);
  console.log(exports);
})
```

```c
// addOne.c
// 导入 js 函数
extern int addOne(int);

int add(int a, int b) {
  return addOne(a + b);
}
```

结果会输出 10。在 C 中定义了 `add` 函数执行 js 中的 `addOne` 函数，同时传入了 js 传过来的两个数字相加，执行结果就是两个数字相加后再加1。