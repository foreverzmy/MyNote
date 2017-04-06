# @import 引用

可以引入其他 Sass、SCSS 文件。我们通常使用 `Partials` 去处理特定功能，方便管理和维护。以下是引用 `_variables.scss` 文件的范例，其中文件名前的 `_` 表示引用前要先编译：

```css
@import "variables";
```