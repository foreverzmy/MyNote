# WebAssembly.Module

`WebAssembly.Module` 对象包含已经由浏览器编译的静态的 WebAssembly 代码，并且可以与 Worker 共享，在 IndexedDB 中缓存，并且可以实例化多次。

可以调用 `WebAssembly.Module()` 构造函数来同步编译给定的 WebAssembly 二进制代码。 但是，获取 `Module` 的主要途径是通过异步编译功能 ( 如 `WebAssembly.compile()` ) 或通过读取 IndexedDB 中的 `Module`。

**重要提示**：

由于大型模块的编译可能开销很大，因此开发人员在同步编译时绝对需要使用 `Module()` 构造函数; 所有其他时候都应该使用异步的 `WebAssembly.compile()` 方法。

## 用法

```ts
const myModule = new WebAssembly.Module(bufferSource);
```

* 参数：

`bufferSource`：包含 要编译的 `.wasm` 模块二进制代码 的 类型数组 或 `ArrayBuffer`。

## Module() 的构造函数属性

* WebAssembly.Module.customSections()

给定一个模块和字符串，返回具有 给定字符串名称的模块 中 所有自定义段 的副本。

* WebAssembly.Module.exports()

给定一个模块，返回一个包含所有声明导出的的数组。

* WebAssembly.Module.imports()

给定一个模块，返回一个包含所有声明导入的的数组。

## Module 实例

所有 Module 实例都继承自 `Module()` 构造函数的 `prototype` 对象--这可以被修改以影响所有的 Module 实例。

### 实例属性

* Module.prototype.constructor

返回创建此对象实例的函数。 默认情况下，这是 `WebAssembly.Module()` 的构造函数。

* Module.prototype[@@toStringTag]

`@@toStringTag` 的初始值是字符串 `WebAssembly.Module`.

### 实例方法

Module 实例没有自己的默认方法。

## 例子

```ts
// main.ts
import * as fs from 'fs';

const path = './addOne.wasm';
const buffer = fs.readFileSync(path);

const mod = new WebAssembly.Module(buffer);

WebAssembly.Module.exports(mod); // ->[{ name: 'memory', kind: 'memory' }, { name: 'add', kind: 'function' }]
const imp = WebAssembly.Module.imports(mod); // ->[ { module: 'env', name: 'addOne', kind: 'function' } ]
const cus = WebAssembly.Module.customSections(mod, 'name'); // ->[]

const importObject = {
  env: {
    addOne: function (arg) {
      return arg + 1;
    }
  }
};

WebAssembly.instantiate(mod, importObject)
  .then((instance: any) => {
    const result = instance.exports.add(4, 5);
    console.log(result); // >10
  });
```

编译为 wasm 的 c 文件如下：

```c
// addOne.c
extern int addOne(int);
int add(int a, int b) {
  return addOne(a + b);
}
```

`WebAssembly.Module()` 构造函数同步编译 WebAssembly 二进制代码。返回值可以通过 `WebAssembly.instantiate` 来实例化。