# Nesting（嵌套）

Sass 允许将一个 CSS 样式嵌套进另一个样式中，内层样式仅适用于外层样式的选择器范围内，可以理解为层级选择器，有助于降低父元素重复性。转译前：

```css
.parent {
  color: blue;
  .child {
    font-size: 12px;
  }
}
```

转译后：

```css
.parent {
  color: blue;
}
 
.parent .child {
    font-size: 12px;
}
```

有些时候需要直接使用嵌套外层的父选择器，这个时候需要使用 `&`。例如:

```css
a {
  font-weight: bold;
  text-decoration: none;
  &:hover { text-decoration: underline; }
  body.firefox & { font-weight: normal; }
}
```

转译后：

```css
a {
  font-weight: bold;
  text-decoration: none; 
}
a:hover {
  text-decoration: underline; 
}
body.firefox a {
  font-weight: normal; 
}
```

嵌套不仅只用于子选择器上，还可以使用在同一个命名空间中的属性上，例如：

```css
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

转译后：

```css
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold; 
}
```