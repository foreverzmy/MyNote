# SASS && SCSS

Sass(Syntactically Awesome StyleSheets) 是对 CSS 的扩展，可以编译成传统CSS，供浏览器使用。使用 Sass 是为了解决在大型项目中传统CSS会遇到的重复、可维护性差等问题。Sass 新增了nested rules（嵌套规则）, variables（变量）, mixins（混入）, selector inheritance（选择器继承）等特性。

SCSS 是 Sass 3 引入新的语法，其语法完全兼容 CSS3，并且继承了 Sass 的强大功能。也就是说，任何标准的 CSS3 样式表都是具有相同语义的有效的 SCSS 文件。另外，SCSS 还能识别大部分 CSS hacks（一些 CSS 小技巧）和特定于浏览器的语法，例如：古老的 IE filter 语法。

使用 Sass 优点：

* 简单简洁
* 语义化（expressive）
* 重复使用性好（reusable）
* 可维护性和扩展性好

Sass 的语法分为：

* 新的SCSS  ( Sassy CSS、Sass 3，扩展名为 `*.scss` )；
* 旧的SASS  ( 学习Haml，具备不使用大括弧格式、使用缩排，不能直接使用CSS语法、学习曲线较高等特性，扩展名为 `*.sass` )；

由于新的 SCSS 语法是 CSS3 的超集合，所以传统的 CSS3 档案就算直接复制过来也不会出错，学习曲线相对较缓。