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

### babel

`babel` 是用来转译 js 的工具，使用 babel 可以将高版本的 js 转译到低版本的 js 。

* 安装

```npm
npm i babel-loader babel-core babel-preset-es2015 babel-preset-react --save
```

* 使用

```js
// webpack.config.js
const webpackConfig = {
  //1.入口
  entry : './src/index.js',        //入口文件
  //2.输出
  output : {
    path: './dist',             //输出路径
    filename : 'bundle.js',     //输出文件名
  },
  //3.加载器
  module: {                          
    rules: [
    //3.1 编译es6
    {
      test: /\.(js|jsx)$/,        //文件后缀、类型      
      exclude: /node_modules/,    //排除这个目录的文件
      loader: 'babel-loader',     //使用的加载器
      options: {
        presets: ['react', "es2015"], //插件
      },
    }]
  }
};
module.exports = webpackConfig;
```

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
