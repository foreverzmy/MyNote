# WebAssembly.validate\(\)

该函数验证给定的 WebAssembly 二进制数组，返回字节是否形成了有效的 wasm 模块：`true/false`。

## 用法：

```js
  WebAssembly.validate(bufferSource);
```

* 参数：

  `bufferSource`：要验证的WebAssembly二进制代码的类型化数组 或 ArrayBuffer。

* 返回值：

  一个指定 bufferSource 是否有效 wasm 模块的布尔值 `true/false`。

* 注意：

  如果 bufferSource 不是类型化的数组或 ArrayBuffer，则抛出 TypeError。

## 例子

```ts
import * as fs from 'fs';

const path = './addOne.wasm';
const buffer = fs.readFileSync(path);

const valid = WebAssembly.validate(buffer);
console.log(valid); // >true
```





