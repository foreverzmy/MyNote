# WebAssembly.compile()

该函数从 WebAssembly 二进制代码编译 `WebAssembly.Module`，在实例化前编译一个模块要使用这个函数，否则使用 `WebAssembly.instantiate()` 函数。

## 用法：

 ```ts
 Promise<WebAssembly.Module> WebAssembly.compile(bufferSource);
 ```

* 参数：

  `bufferSource`：一个包含要编译的 `.wasm` 模块的二进制代码的类型数组或ArrayBuffer。

* 返回值：

  `resolve` 一个表示编译模块 WebAssembly.Module 对象的 Promise。

* 注意

  如果 bufferSource 不是类型化的数组或 ArrayBuffer，则抛出 TypeError。
  如果编译失败，则 Promise 将 reject `WebAssembly.CompileError`。

## 例子

使用 `compile()` 函数编译加载的 wasm 字节代码，然后使用 `emit` 将时间发送给监听器。

```ts
// main.ts
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
})
```

编译为 wasm 的 c 文件如下：

```c
// addOne.c
extern int addOne(int);
int add(int a, int b) {
  return addOne(a + b);
}
```

在这个例子中，先加载 wasm 文件，然后使用 `compile()` 函数编译加载的 wasm 字节代码，`main.ts` 中的 `mod` 就是一个 `WebAssembly.Module` 对象，然后使用 `WebAssembly.instantiate` 实例化该对象生成 `WebAssembly.instance` 类型的实例化对象，可以从中调用在 C 中定义的方法。本例在实例化时传入了 `importObject` 对象，传入的对象可以在 C 中调用。