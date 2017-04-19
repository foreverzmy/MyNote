# Common chunk

利用 webpack.optimize.CommonsChunkPlugin，可以将共用的组件代码块分离出来。

例：

```js
// main1.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('a')
);

// main2.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h2>Hello Webpack</h2>,
  document.getElementById('b')
);
```

* index.html

```html
<html>
  <body>
    <div id="a"></div>
    <div id="b"></div>
    <script src="init.js"></script>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

* webpack.config.js

```js
const webpack = require('webpack')

const webpackConfig = {
  //1.入口
  entry: {
    bundle1: './main1.jsx',
    bundle2: './main2.jsx'
  },
  //2.输出
  output: {
    filename: '[name].js', //输出文件名
  },
  //3.加载器
  module: {
    rules: [
      //3.1 编译es6
      {
        test: /\.js[x]$/, //文件后缀、类型      
        exclude: /node_modules/, //排除这个目录的文件
        loader: 'babel-loader', //使用的加载器
        options: {
          presets: ['react', "es2015"], //插件
        }
      }
    ]
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin('init.js')
  ]
};
module.exports = webpackConfig;
```

会生成 init.js 、bundle1.js 和 bundle2.js 三个文件。init.js 是 bundle1.js 和 bundle2.js 的公共部分。