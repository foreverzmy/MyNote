# @extend（扩展）

当一个样式类（class）含有另一个类的所有样式，并且它有自己的特定样式的时候可以使用 @extend 。例如，编译前：

```css
.lemonade {
  border: 1px yellow;
  background-color: #fdd;
}
.strawberry {
  @extend .lemonade;
  border-color: pink;
}
```

转译后：

```css
.lemonade, .strawberry {
  border: 1px yellow;
  background-color: #fdd;
}
 
.strawberry {
  border-color: pink;
}
```

搭配占位符（Placeholders） 使用，转译前：

```css
$lemon-yellow : red;
a%drink {
  font-size: 2em;
  background-color: $lemon-yellow;
}
 
.lemonade {
  @extend %drink;
  font-size: 1.5em;
}
```

转译后：

```css
a.lemonade {
  font-size: 2em;
  background-color: red;
}
 
.lemonade {
  font-size: 1.5em;
}
```

@mixin和@extend比较，转译前：

```css
@mixin no-variable {
  font-size: 12px;
  color: #FFF;
  opacity: .9;
}
 
%placeholder {
  font-size: 12px;
  color: #FFF;
  opacity: .9;
}
 
span {
  @extend %placeholder;
}
 
div {
  @extend %placeholder;
}
 
p {
  @include no-variable;
}
 
h1 {
  @include no-variable;
}
```

转译后：

```css
span, div {
  font-size: 12px;
  color: #FFF;
  opacity: .9;
}
 
p {
  font-size: 12px;
  color: #FFF;
  opacity: .9;
}
 
h1 {
  font-size: 12px;
  color: #FFF;
  opacity: .9;
}
```