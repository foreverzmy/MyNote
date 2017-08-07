# WebAssembly.Memory()

`WebAssembly.Memory()` 构造函数创建一个新的 Memory 对象，它是一个可调整大小的 ArrayBuffer，它保存由 WebAssembly 实例访问的内存的原始字节。

由 JavaScript 或 WebAssembly 代码创建的内存将可以从 JavaScript 和 WebAssembly 进行访问和变换。

## 构造函数

* 用法：

```ts
const myMemory = new WebAssembly.Memory(memoryDescriptor);
```

* 参数：

    memoryDescriptor：可以包含以下成员的对象：

        1. initial：WebAssembly 内存的初始大小，以 WebAssembly 页为单位。
        
        2. maximum (可选)： maximum 允许以 WebAssembly pages 为单位设置 WebAssembly 内存的大小增长。 当存在时，maximum 参数充当引擎的提示，以预留内存。然而，引擎可能会忽略或夹住此预留请求。通常，大多数 WebAssembly 模块不需要设置最大值。
      
    * Note：WebAssembly pages 具有 65,536 字节的固定大小，即 64 KiB。

* 错误

    如果 `memoryDescriptor` 不是类型对象，则会抛出 `TypeError`。
    
    如果指定的最大值并小于初始值，则抛出 `RangeError`。

## Memory 实例

所有内存实例都继承自 `Memory()` 构造函数的原型对象 - 这可以修改为影响所有内存实例。

### 实例属性

* Memory.prototype.constructor

返回创建此对象实例的函数。 默认情况下，这是 `WebAssembly.Memory()` 构造函数。

* Memory.prototype.buffer

一个访问器属性，返回内存中包含的缓冲区。

## 实例方法

* Memory.prototype.grow()

将内存实例的大小增加指定数量的 WebAssembly pages（每个大小为64KB）。