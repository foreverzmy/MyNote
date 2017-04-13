# UglifyJs

Webpack 可以去掉本身附加的东西，优化代码。

例子：

* webpack.config.js

```js
// webpack.config.js
const UglifyJSPlugin = require('uglifyjs-webpack-plugin');

const webpackConfig = {
  //1.入口
  entry: './main.js', //入口文件
  //2.输出
  output: {
    filename: 'bundle.js', //输出文件名
  },
  // 3.插件
  plugins: [
    new UglifyJSPlugin({
      compress: {
        warnings: false
      }
    })
  ]
};
module.exports = webpackConfig;
```