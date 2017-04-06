# Variables（变量）

变量可以用来储存值，可以增加重用性。在 Sass 中我们使用 `$` 来表示变量，变量类型可以是 `Numbers`（可以有单位或无单位）、`Strings`、`Booleans`、`null`值（视为空值），甚至可以使用 `Lists`、`Maps`。

变量的使用：

```css
$translucent-white: rgba(255,255,255,0.3);
p {
  background-color: $translucent-white;
}
```

Lists 类型的值可以用空格或加逗号分隔，Maps代表一个键和值对集合，键用于查找值。和 Lists 不同，Maps必须始终使用括号括起来，并且必须用逗号分隔。：

```css
$font-style-2: Helvetica, Arial, sans-serif;
$standard-border: 4px solid black;
 
p {
    border: $standard-border;
}
 
/* maps key:value */
$font-style-2: (key1: value1, key2: value2);
```