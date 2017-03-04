# 认识 Angular-CLI

开发 Angular 需要很多的工具，比如 Typescript 、 Webpack 、 Karma 等等，这些工具自己去配置会很麻烦，所以 Angular 官方推出了 Angular-CLI 。

Angular-CLI 不仅仅是一个构建 Angular 的工具，而是一个集成了很多工具的平台。

# 安装

Angular-CLI 新版本已经更名为 @angular/cli

```
npm install -g @angular/cli
```

# 常用命令

* 创建项目

```
ng new my-project
``` 

`ng new` 会自动创建 Angular 项目并安装依赖，安装依赖时可以按住 `Ctrl+C` 来停止，然后自己科学的安装依赖。

* 创建模块

```
ng g cl MyClass
ng g c  MyComponent
ng g d  MyDirective
ng g e  MyEnum
ng g m  MyModule
ng g p  MyPipe
ng g s  MyService
```

其中 `g` 是 `generate` 的缩写，后面的也都是缩写，可以通过 `ng g` 来创建这些模块，它们会被自动创建到 `src/app/` 下面的文件夹下，并且以小驼峰式创建文件夹： `src/app/my-component`

* 启动项目

```
ng serve
```

`ng serve` 会启动项目，默认为 `4200` 端口。但这时是在未编译的状态下运行项目，所以js文件会很大，也可以通过下面的命令来解决这个问题：

```
ng serve --prod --aot
```

此时会自动启用 AOT ，此时启动项目就会发现加载的资源很小。

* 构建项目

```
ng build
```

构建项目会在项目下生成一个 `dist` 的文件夹，构建后的项目就在这个文件夹里了。

* 测试项目

```
ng test
```

会使用karma自动测试项目里的测试用例。
