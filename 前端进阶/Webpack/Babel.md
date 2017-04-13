# Babel-loader

通过使用不同的 loader，webpack 通过调用外部的脚本或工具可以对各种各样的格式的文件进行处理(更多信息). 例如, `Babel-loader`。 `Babel` 其实是一个编译 JavaScript 的平台可以将 `JSX/ES6` 文件转换成浏览器可以识别的 js 文件。

## 安装

Babel 一般需要很多的库结合使用，我们可以一起安装好：

```
$ npm i babel-loader babel-core babel-preset-es2015 babel-preset-react --save
```

## 使用

通过一个简单的 React 例子来说：

```jsx
// main.jsx
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.querySelector('#wrapper')
);
```

index.html

```html
<html>

<body>
  <div id="wrapper"></div>
  <script src="/bundle.js"></script>
</body>

</html>
```

```js
// webpack.config.js
const webpackConfig = {
  //1.入口
  entry: './main.jsx', //入口文件
  //2.输出
  output: {
    path: './dist', //输出路径
    filename: 'bundle.js', //输出文件名
  },
  //3.加载器
  module: {
    rules: [
      //3.1 编译es6
      {
        test: /\.(js|jsx)$/, //文件后缀、类型      
        exclude: /node_modules/, //排除这个目录的文件
        loader: 'babel-loader', //使用的加载器
        options: {
          presets: ['react', "es2015"], //插件
        },
      }
    ]
  }
};
module.exports = webpackConfig;
```



