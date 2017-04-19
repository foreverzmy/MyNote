# Vendor chunk

利用 webpack.optimize.CommonsChunkPlugin ，你可以把第三方库抽离出来。

* main.js

```js
const $ = require('jquery');
$('h1').text('Hello World');
```

* index.html

```html
<html>
  <body>
    <h1></h1>
    <script src="vendor.js"></script>
    <script src="bundle.js"></script>
  </body>
</html>
```

* webpack.config.js

```js
const webpack = require('webpack');

module.exports = {
  entry: {
    app: './main.js',
    vendor: ['jquery'],
  },
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      filename: 'vendor.js'
    })
  ]
};
```