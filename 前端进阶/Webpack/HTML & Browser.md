# HTML & Browser

这里介绍两个插件，一个是 `html-webpack-plugin`，这个插件会自动创建 HTML 文件，不用再手动创建 HTML 文件了。还有一个是 `open-browser-webpack-plugin` ，这个插件会自动帮你打开浏览器并进入项目主页。

```js
// webpack.config.js
const HtmlwebpackPlugin = require('html-webpack-plugin');
const OpenBrowserPlugin = require('open-browser-webpack-plugin');

module.exports = {
  //1.入口
  entry: './main.js',
  //1.入口
  output: {
    filename: 'bundle.js'
  },
  // 3.插件
  plugins: [
    // 自动生成 HTML
    new HtmlwebpackPlugin({
      title: 'Webpack-demos',
      filename: 'index.html'
    }),
    // 自动打开项目
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    })
  ]
};
```

运行 `webpack-dev-server` 启动项目，启动这个需要 node 7 版本以上。