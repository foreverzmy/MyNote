# CSS-loader

Webpack 允许在 js 文件中 import CSS , 通过 CSS-loader 来预处理 css 文件。

## 安装 

```npm
$ npm i style-loader css-loader --save
```

例子：

* index.html

```html
<html>

<head>
  <script type="text/javascript" src="bundle.js"></script>
</head>

<body>
  <h1>Hello World</h1>
</body>

</html>
```

* style.css

```css
h1 {
  color: red;
}
```

* main.js

```js
// main.js
import './style.css';
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
        test: /\.css$/, //文件后缀、类型      
        use: ['style-loader', 'css-loader'] //使用的加载器
      }
    ]
  }
};
module.exports = webpackConfig;
```

启动服务后, `index.html` 有内部样式.

```html
<head>
  <script type="text/javascript" src="bundle.js"></script>
  <style type="text/css">
    body {
      background-color: blue;
    }
  </style>
</head>
```
