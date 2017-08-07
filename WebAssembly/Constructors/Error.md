# Error

WebAssembly 有一下三种形式的 Error：

## WebAssembly.CompileError()

`WebAssembly.CompileError()` 构造函数创建一个新的 WebAssembly CompileError 对象，它指示 WebAssembly 解码或验证期间的错误。

## WebAssembly.LinkError()

`WebAssembly.LinkError()` 构造函数创建一个新的 WebAssembly LinkError 对象，该对象指示模块实例化期间的错误（除了启动函数的陷阱）。

## WebAssembly.RuntimeError()

`WebAssembly.RuntimeError()` 构造函数创建一个新的 WebAssembly RuntimeError 对象 - 当 WebAssembly 指定陷阱时抛出的类型。