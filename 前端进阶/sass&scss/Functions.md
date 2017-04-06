# Functions（函数）

ass内置了一些好用函数可以简单设定色相、渐变等，例如：adjust-hue($color, $degrees)、fade-out：

更多内置函数的列表请查看[这个页面](http://sass-lang.com/documentation/Sass/Script/Functions.html)

## Operations（运算）

通过加减乘除和取余等运算符可以方便运算所需的属性值。Sass 支持数字标准的算术运算（加法 `+` ，减法 `-` ，乘法 `*` ，除法 `/` 和取模 `%` ）。Sass 数学函数在算术运算期间会保留单位。数字类型支持关系运算符( `<` , `>` , `<=` , `>=` )，并且所有类型支持相等运算符( `==` , `!=` )。

比如颜色运算：

```css
p {
  color: #010203 + #040506;
}
```

计算 `01 + 04 = 05`, `02 + 05 = 07`, 和 `03 + 06 = 09`，并且转译为：

```css
p {
  color: #050709; 
}
```

除法 `/` 使用上需要注意：

```css
p {
  font: 10px/8px;             // 原生的CSS，不作为除法
  $width: 1000px;
  width: $width/2;            // 使用了变量, 作为除法
  width: round(1.5)/2;        // 使用了函数, 作为除法
  height: (500px/2);          // 使用了括号, 作为除法
  margin-left: 5px + 8px/2px; // 使用了 +, 作为除法
  font: (italic bold 10px/8px); // 在一个列表（list）中，括号可以被忽略。
}
```

转译为：

```css
p {
  font: 10px/8px;
  width: 500px;
  height: 250px;
  margin-left: 9px; 
}

也可以使用 `@each` 语法迭代 list 内容：

```css
$list: (orange, purple, teal);
 
@each $item in $list {
  .#{$item} {
    background: $item;
  }
}
```

这里再次提醒一下，参数当作字串传入时需要使用 `#{}` 插值。编译后：

```css
.orange {
  background: orange;
}
 
.purple {
  background: purple;
}
 
.teal {
  background: teal;
}
```

使用 `@for` 迭代，并加入条件判断：

```css
$total:3;
$step :2;
@for $i from 1 through $total {
  .ray:nth-child(#{$i}) {
    background: adjust-hue(blue, $i * $step);
    // if()函数
    width: if($i % 2 == 0, 300px, 350px);
    margin-left: if($i % 2 == 0, 0px, 50px);
  }
}
```

编译后：

```css
.ray:nth-child(1) {
  background: #0900ff;
  width: 350px;
  margin-left: 50px;
}
 
.ray:nth-child(2) {
  background: #1100ff;
  width: 300px;
  margin-left: 0px;
}
 
.ray:nth-child(3) {
  background: #1a00ff;
  width: 350px;
  margin-left: 50px;
}
```

这里还有一个就是 `if()` 函数，第1个参数是判断条件，第2个参数是判断条件为 `true` 时返回的值，第3个参数是判断条件为 `false` 时返回的值。
