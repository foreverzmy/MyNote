# ESLint 配置

[中文官网](http://eslint.cn/)
[参考](https://github.com/Jocs/ESLint_docs/blob/master/Configration/ESLint_configration.md)

我的配置：

```json
{
  // 想使用的额外的语言特性
  "ecmaFeatures": {
    "arrowFunctions": true, // enable arrow functions
    "binaryLiterals": true, // enable binary literals
    "blockBindings": true, // enable let and const
    "classes": true, // enable classes 类
    "defaultParams": true, // enable default function parameters
    "destructuring": false, // enable destructuring 解构
    "experimentalObjectRestSpread": false, // enable support for the experimental object rest/spread properties 
    "forOf": true, // enable for-of loops
    "generators": false, // enable generators
    "globalReturn": false, // 允许在全局作用域下使用 return 语句
    "impliedStrict": true, // 启用全局 strict mode
    "jsx": false, // 启用 JSX
    "modules": false, // enable modules and global strict mode
    "objectLiteralComputedProperties": false,
    "objectLiteralDuplicateProperties": false,
    "objectLiteralShorthandMethods": false,
    "objectLiteralShorthandProperties": false,
    "octalLiterals": false,
    "regexUFlag": false,
    "regexYFlag": false,
    "restParams": false,
    "spread": false,
    "superInFunctions": false,
    "templateStrings": false,
    "unicodeCodePointEscapes": false
  },
  // 环境定义了预定义的全局变量
  "env": {
    "browser": true, // browser 全局变量
    "node": true, // Node.js 全局变量和 Node.js 作用域。
    "commonjs": true, //  CommonJS 全局变量和 CommonJS 作用域
    "amd": false, // 定义 require() 和 define() 作为像 amd 一样的全局变量
    "es6": true, // 支持除模块外所有 ECMAScript 6 特性
    "jquery": false, // jQuery 全局变量
    "meteor": false, // Meteor 全局变量
    "mongo": false, // MongoDB 全局变量
    "applescript": false, // AppleScript 全局变量
    "greasemonkey": false, // GreaseMonkey 全局变量
    "atomtest": false, // Atom 测试全局变量
    "embertest": false, // Ember 测试全局变量
    "mocha": true, // 添加所有的 Mocha 测试全局变量
    "jasmine": false, // 添加所有的 Jasmine 版本 1.3 和 2.0 的测试全局变量
    "phantomjs": false, // PhantomJS 全局变量
    "jest": false, // Jest 全局变量
    "nashorn": false, // Java 8 Nashorn 全局变量
    "prototypejs": false, // Prototype.js 全局变量
    "protractor": false, // Protractor 全局变量
    "qunit": false, // QUnit 全局变量
    "serviceworker": false, // Service Worker 全局变量
    "shared-node-browser": false, // Node 和 Browser 通用全局变量
    "shelljs": false, // ShellJS 全局变量
    "webextensions": false, // WebExtensions 全局变量
    "worker": false // web workers 全局变量
  },
  "extends": "",
  // 中添加项目所需全局变量
  "globals": {
    "document": true,
    "navigator": true,
    "window": true
  },
  "parser": "",
  // JavaScript 语言选项
  "parserOptions": {
    "ecmaFeatures": {},
    "ecmaVersion": 6, // ECMAScript 版本
    "sourceType": "script"
  },
  "plugins": [],
  "root": false,
  // 可能的错误  //
  "rules": {
    "no-var": 2, // 要求或禁止 var 声明中的初始化
    "init-declarations": 2,
    "semi": 1, // 需要分号
    "no-extra-semi": 2, // 禁止不必要的分号
    "quotes": [2, "single"], // 使用单引号
    "no-extra-parens": 2, // 禁止不必要的括号
    "no-cond-assign": 2, // 禁止条件表达式中出现赋值操作符
    "no-control-regex": 2, // 禁止在正则表达式中使用控制字符 ：new RegExp("\x1f")
    "no-constant-condition": 2,
    "no-dupe-args": 2, // 禁止function 定义中出现重名参数
    "no-dupe-keys": 2, // 禁止对象字面量中出现重复的 key 
    "no-dupe-class-members": 2, // 禁止类成员中出现重复的名称
    "no-duplicate-case": 2, // 禁止出现重复的 case 标签
    "no-empty": 2, // 禁止出现空语句块
    "no-ex-assign": 2, // 禁止对 catch 子句的参数重新赋值
    "no-shadow": 2, // 禁止变量声明与外层作用域的变量同名
    "no-unused-vars": 1, // 禁止出现未使用过的变量
    "no-const-assign": 2, // 禁止修改 const 声明的变量
    "prefer-arrow-callback": 2, // 要求使用箭头函数作为回调
    "linebreak-style": 0, // 强制使用一致的换行风格
    "indent": [2, 2] // 强制使用一致的缩进:2 space
  },
  "settings": {}
}
```