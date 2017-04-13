# Image loader

Webpack 允许在 js 文件中 import 图片 , 通过 `url-loader` 和 `file-loader` 来预处理图片文件。

例子：

* index.html

```html
<html>
  <body>
    <script type="text/javascript" src="bundle.js"></script>
  </body>
</html>
```

* main.js

```js
// main.js
const img = document.createElement("img");
img.src = require('./timg.jpg');
document.body.appendChild(img);
```

* webpack.config.js

```js
// webpack.config.js
const webpackConfig = {
  //1.入口
  entry: './main.js', //入口文件
  //2.输出
  output: {
    // path: './dist', //输出路径
    filename: 'bundle.js', //输出文件名
  },
  //3.加载器
  module: {
    rules: [
      //3.1 编译es6
      {
        test: /\.(png|jpg)$/, //文件后缀、类型      
        loader: 'url-loader', //使用的加载器
      }
    ]
  }
};
module.exports = webpackConfig;
```


