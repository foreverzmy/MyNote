# Code splitting

对于大型项目，把所有代码编译到一个文件并不是有效的， webpack 允许你把代码分成好多块。

特别是某种情况下，只需要个别代码这些块可以按需加载。

在 commonjs 中有一个 Modules/Async/A 规范，里面定义了 require.ensure 语法。webpack 实现了它，作用是可以在打包的时候进行代码分片，并异步加载分片后的代码。用法如下：

```js
require.ensure([], function(require){
    const list = require('./list');
    list.show();
});
```

此时list.js会被打包成一个单独的chunk文件，大概长这样：
`1.fb874860b35831bc96a8.js`。可读性比较差。我在上一篇结尾也提到了，给它命名的方式，那就是给require.ensure传递第三个参数，如：

```js
require.ensure([], function(require){
    var list = require('./list');
    list.show();
}, 'list');
```

这样就能得到你想要的文件名称：
首先，你需要用 require.ensure to 来定义一个分割的点。

例：

* main.js

```js
require.ensure(['./a'], function(require) {
  const content = require('./a');
  document.open();
  document.write('<h1>' + content + '</h1>');
  document.close();
});
```

* a.js

```js
module.exports = 'Hello World';
```

* index.html

```html
<html>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```

* webpack.config.js

```js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```

启动服务.

```
$ webpack-dev-server
```

在界面上, 你感觉不到任何不一样的地方. 但是, Webpack 已经把 `main.js` 和 `a.js` 编译成( `bundle.js` 和 `0.bundle.js` )的块。

