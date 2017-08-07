# WebAssembly.Instance()

`WebAssembly.Instance` 对象是 `WebAssembly.Module` 的有状态的可执行实例。实例对象包含所有导出的 WebAssembly 函数，允许从 JavaScript 调用 WebAssembly 代码。

可以调用 `WebAssembly.Instance()` 构造函数来同步实例化给定的 `WebAssembly.Module` 对象。 但是，获取实例的主要方式是通过异步 `WebAssembly.instantiate()` 函数。

## 构造函数

**重要提示**：

由于大型模块的实例化可能很昂贵，因此开发人员只有在绝对需要同步实例化时才应使用 `Instance()` 构造函数; 所有其他时候都应该使用异步 `WebAssembly.instantiate()` 方法。

* 用法：

```ts
const myInstance = new WebAssembly.Instance(module, importObject);
```

* 参数：

  `module`：要实例化的 `WebAssembly.Module` 对象。

  `importObjec` (可选)：包含要导入到新创建的实例中的值的对象，例如函数或 `WebAssembly.Memory` 对象。每个声明的模块导入必须有一个匹配的属性，否则会抛出一个 `WebAssembly.LinkError`。

## Instance 实例

所有 Instance 实例都继承自 `Instance()` 构造函数的原型对象 - 这可以被修改以影响所有 Instance 实例。

### 实例属性

* Instance.prototype.constructor

返回创建此对象实例的函数。 默认情况下，这是 `WebAssembly.Instance()` 构造函数。

* Instance.prototype.exports (只读)

返回包含作为其成员的所有从 WebAssembly 模块实例导出的函数的对象，以允许它们被 JavaScript 访问和使用。

### 实例方法

无。