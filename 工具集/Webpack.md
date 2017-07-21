# Webpack 使用

## 安装

```npm
npm i -g webpack
```

## 使用

在项目根目录新建 `webpack.config.js` :

* 简单配置

```js
const webpackConfig = {
  //1.入口
  entry : './src/index.js', //入口文件
  //2.输出
  output : {
    path: './dist', //输出路径
    filename : 'bundle.js', //输出文件名
  }
};
module.exports = webpackConfig;
```

* 打包

根目录下执行 `webpack` 命令进行打包。

在根目录 `dist` 文件夹下会有打包好的 `bundle.js` 文件。

## 插件

webpack 还有很丰富的插件支持，使 webpack 的功能更加强大。


## 打包 CSS 文件

* 安装

```npm
npm i style-loader css-loader --save
```

* 使用

```js
// webpack.config.js
module: {                          
  rules: [
  // 打包css
  {
    test: /\.css$/,
    use: ['style-loader','css-loader'],
  }]
}
```

## Plugin

一般来说需要把所有静态文件输出到一个目录下。现在我们原始的 `html` 文件还在 `src` 目录下，而打包后的 `js` 在 `dist`，需要复制一份 `html`，使用 `HtmlWebpackPlugin` 来解决这个问题。

* 安装

```npm
npm i html-webpack-plugin --save
```

* 使用

```js
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin');

module: {                          
  插件
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),               //压缩js文件
    new HtmlWebpackPlugin({template: 'src/index.html'})  //设置HtmlWebpackPlugin插件及html模板路径
  ],
}
```

执行 `webpack` 后会看到 `dist` 目录下产生了一个 `index.html` 文件，内容如下:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello Webpack</title>
  </head>
  <body>
    ...
  <script type="text/javascript" src="bundle.js"></script></body>
</html>
```

会发现webpack自动添加了js文件的引入。

一份配置文件

```js
const path = require('path');
const fs = require('fs');
const webpack = require('webpack');
const ExtractTextPlugin = require('extract-text-webpack-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const OpenBrowserPlugin = require('open-browser-webpack-plugin');
const StyleExtHtmlWebpackPlugin = require('style-ext-html-webpack-plugin');
const CompressionPlugin = require('compression-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');

const outpath = 'build';

module.exports = {
  entry: './src/app.js',

  output: {
    path: path.resolve(__dirname, outpath),
    filename: 'bundle.[chunkhash].js'
  },
  module: {
    rules: [{
      test: /\.scss?$/,
      use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: ['css-loader', 'sass-loader']
      })
      // ['style-loader', 'css-loader', 'sass-loader']
    }, {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        query: {
          presets: ['es2015']
        }
      }
    }, ]
  },
  // 新引入
  plugins: [
    // Scope Hoisting
    new webpack.optimize.ModuleConcatenationPlugin(),
    // Code Splitting
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      filename: 'vendor.[chunkhash].js',
      minChunks(module) {
        return module.context &&
          module.context.indexOf('node_modules') >= 0;
      }
    }),
    // 自动创建 index.html 并压缩
    new HtmlWebpackPlugin({
      template: './index.html',
      excludeChunks: ['base'],
      filename: 'index.html',
      minify: {
        collapseWhitespace: true,
        collapseInlineTagWhitespace: true,
        removeComments: true,
        removeRedundantAttributes: true
      }
    }),
    // 使用标识符压缩
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false,
        screw_ie8: true,
        conditionals: true,
        unused: true,
        comparisons: true,
        sequences: true,
        dead_code: true,
        evaluate: true,
        if_return: true,
        join_vars: true
      },
      output: {
        comments: false
      }
    }),
    new webpack.HashedModuleIdsPlugin(),
    // React 生产版本
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('production')
    }),
    // 内联 css 文件
    new ExtractTextPlugin({
      filename: '[name].[contenthash].css',
      allChunks: true
    }),
    new StyleExtHtmlWebpackPlugin({
      minify: true
    }),
    // Gzip压缩
    new CompressionPlugin({
      asset: '[path].gz[query]',
      algorithm: 'gzip',
      test: /\.js$|\.css$|\.html$|\.eot?.+$|\.ttf?.+$|\.woff?.+$|\.svg?.+$/,
      threshold: 10240,
      minRatio: 0.8
    }),
    // 删除打包文件夹
    new CleanWebpackPlugin(['dist', 'build', ], 　 //匹配删除的文件
      {
        root: __dirname, //根目录
        verbose: true, //开启在控制台输出信息
        dry: false, //启用删除文件
      }
    ),
    // 开发状态自动启动浏览器
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    }),
  ],
  devServer: {
    //webpack-dev-server
    historyApiFallback: true,
    inline: true, // auto refresh
    port: 8080,
    proxy: {
      '/uptoken/*': {
        target: 'http://localhost:9000',
        secure: false
      }
    }
  },
};
```