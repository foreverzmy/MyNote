# WebAssembly.compile()

该函数从 WebAssembly 二进制代码编译 `WebAssembly.Module`，在实例化前编译一个模块要使用这个函数，否则使用 `WebAssembly.instantiate()` 函数。

* 用法：

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