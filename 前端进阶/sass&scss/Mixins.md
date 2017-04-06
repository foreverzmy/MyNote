# Mixins（混入）

混入( mixin )允许您定义可以在整个样式表中重复使用的样式，从而避免了使用无语意的类（ class ），比如 `.float-left`。混入( mixin )还可以包含所有的 CSS 规则，以及任何其他在 Sass 文档中被允许使用的东西。他们甚至可以带参数，引入变量，只需少量的混入( mixin )代码就能输出多样化的样式。

定义的混入 `@mixin` 使用 `@include` 引用。

```css
/* 定义一个mixin */
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}
 
//引用mixin
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```

转译后：

```css
.page-title {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
  padding: 4px;
  margin-top: 10px; 
}
```

再来举一个最常见的例子，比如给属性加上跨浏览器的前缀，这里我们使用了一个参数$radius。例如：

```css
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
 
.box { @include border-radius(10px); }
```

转译后：

```css
.box {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```

参数还可以使用默认值，对上面的例子稍作修改：

```css
@mixin border-radius($radius:10px) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
.box1 { @include border-radius(); }
.box2 { @include border-radius(20px); }
```

转译后：

```css
.box1 {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
 
.box2 {
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  -ms-border-radius: 20px;
  border-radius: 20px;
}
```

有时我们也需要处理参数复杂的情形，此时可以使用 Lists、Maps 类型来辅助，例如：

```css
/* 定义一个混入，用于定义线性渐变 */
@mixin stripes($direction, $width-percent, $stripe-color, $stripe-background: #FFF) {
  background: repeating-linear-gradient(
    $direction,
    $stripe-background,
    $stripe-background ($width-percent - 1),
    $stripe-color 1%,
    $stripe-background $width-percent
  );
}
/* 定义一个map，作为混入参数 */
$college-ruled-style: ( 
  direction: to bottom,
  width-percent: 15%,
  stripe-color: blue,
  stripe-background: white
);
/* 通过map类型作为参数，引用混入。 */
.definition {
  width: 100%;
  height: 100%;
  @include stripes( $college-ruled-style ... );
}
```

这里有需要注意一个地方，这里的参数是一个可变参数，参数后面需要跟 `...` 进行传递([可变参数](http://www.css88.com/doc/sass/#variable-arguments))。

转译后：

```css
.definition {
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(to bottom, white, white 14%, blue 1%, white 15%);
}
```

还有种情况是参数当作字串传入（或者字符串插值），说的通俗一点就是带引号的字符串将被编译为不带引号的字符串，需要使用 `#{}` 插值，例如：

```css
/* 使用 #{$file} 接收 */
@mixin photo-content($file) {
  content: url(#{$file}.jpg); //string interpolation
  object-fit: cover;
}
 
.photo { 
  @include photo-content('titanosaur');
  width: 60%;
  margin: 0px auto; 
}
```

转译后：

```css
.photo {
  content: url(titanosaur.jpg);
  object-fit: cover;
  width: 60%;
  margin: 0px auto;
}
```

混入中也可以使用嵌套：

```css
@mixin hover-color($color) {
  &:hover {
    color: $color;
  }
}
 
.word {
  @include hover-color(red);
}
```

转译后：

```css
.word:hover {
  color: red;
}
```