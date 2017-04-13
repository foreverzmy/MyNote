#  CSS Module

CSS Module可以开启全局变量和局部变量，:global(...)表示全局变量，可以在全局中使用样式。

例：

* index.html

```html
<html>
<body>
  <h1 class="h1">Hello World</h1>
  <h2 class="h2">Hello Webpack</h2>
  <div id="example"></div>
  <script src="./bundle.js"></script>
</body>
</html>
```

* style.css

```css
.h1 {
  color: red;
}
:global(.h2) {
  color: blue;
}
```

* mian.js

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import style from './style.css'

ReactDOM.render(
  <div>
    <h1 className={style.h1}>Hello World</h1>
    <h2 className="h2">Hello Webpack</h2>
  </div>,
  document.getElementById('example')
);
```

* webpack.config.js

```js
// webpack.config.js
const webpackConfig = {
  //1.入口
  entry: './main.jsx', //入口文件
  //2.输出
  output: {
    filename: 'bundle.js', //输出文件名
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
        },
      }, {
        test: /\.css$/, //文件后缀、类型      
        use: ['style-loader', 'css-loader'] //使用的加载器
      }
    ]
  }
};
module.exports = webpackConfig;
```

启动服务

```
$ webpack-dev-server
```

* 访问 `http://127.0.0.1:8080` , 你将看到只有第一个 `h1` 是红的,因为它是局部, 同时 `h2` 是蓝色的, 因为是 `h2` 全局的。
