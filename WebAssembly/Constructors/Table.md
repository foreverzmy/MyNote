# WebAssembly.Table()

`WebAssembly.Table()` 构造函数创建给定大小和元素类型的新 Table 对象。

这是一个 JavaScript 包装器对象 - 一个表示 WebAssembly 表的阵列式结构，它存储函数引用。 由 JavaScript 或 WebAssembly 创建的 table 将可以从 JavaScript 和 WebAssembly 中访问和变换。

* 注意：表格目前只能存储函数引用，但将来可能会扩展

## 构造函数

* 用法：

  ```js
  const myTable = new WebAssembly.Table(tableDescriptor);
  ```

* 参数：

  tableDescriptor：可以包含以下成员的对象：

      1. element：表示要存储在表中的值的类型的字符串。 目前这只能有一个值`anyfunc`（函数）。

      2. initial：WebAssembly Table 的初始元素数。

      3. maximum (可选)：允许 WebAssembly Table 生成的元素的最大数量。

* 错误

  1. 如果 tableDescriptor 不是类型对象，则抛出 TypeError。
  2. 如果指定了最大值并小于初始值，则抛出 RangeError。

## Table 实例

所有表实例继承自 `Table()` 构造函数的原型对象 - 这可以被修改以影响所有表实例。

### 实例属性

* Table.prototype.constructor

返回创建此对象实例的函数。 默认情况下，这是 `WebAssembly.Table()` 构造函数。

* Table.prototype.length

返回 table 的长度，即元素的数量。

### 实例方法

* Table.prototype.get()

访问函数 - 获取存储在给定索引中的元素。

* Table.prototype.grow()

将 table 实例的大小增加指定数量的元素。

* Table.prototype.set()

将给定索引处存储的元素设置为给定值。