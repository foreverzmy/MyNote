# 关于这章

这章介绍了 Angular 的基本构造，即 Angular 是怎么运行起来了。这章会一步一步的搭建一个 Hello World 的例子。

## app.component.ts

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent { }
```

* app.component.html

```html
<h3>Hello World!</h3>
```

上述代码中，首先通过 `import` 从 Angular 的基础包 `@angular/core` 中引入组件模块 `Component` ,通过 `@Component` 装饰器来告诉 Angular 怎样创建这个组件。在组件在中可以定义该组件的 DOM 元素名称，如 `selector: 'app-root'` ,也可以给组件引入所需要的模板，如 `templateUrl: './app.component.html'`;最后，定义一个组件类并对外输出该类，这样在其他的文件中就可以通过这个类名引用该组件。

## app.module.ts

在 Angular 中需要用模块来组织一些功能紧密相关的代码块，每个应用至少有一个模块，习惯上把它叫做 `AppModule`：

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

* @NgModule：用于定义模块用的装饰器;
* declarations：导入模块依赖的组件、指令等;
* imports：用来导入当前模块所需的其他模块。在这个例子中，几乎每个应用的跟模块都需要导入 `BrowserModule` 模块，它注册了一些关键的 `Provider` 和通用的指令，所以在 `imports` 属性中配置，作为公共模块供全局调用;
* bootstrap：标记出引导组件，在 Angular 启动应用时，将被标记的组件渲染到模板中。

## main.ts

Angular 项目一般有一个入口文件，通过这个文件来串联起整个项目。

```ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```

要启动应用，主要依赖于 Angular 自带的 `platformBrowserDynamic` 函数和应用模块 `AppModule` ，然后调用 `platformBrowserDynamic().bootstrapModule()` 方法，来编译启动 `AppModule` 模块。

## index.html

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Project01</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root>Loading...</app-root>
</body>
</html>
```

其中的 `app-root` 标签就是我们在根组件 `app.component.ts` 中定义的 `selector` 。

这样就是一个最简单的 Angular 项目了。