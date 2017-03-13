# 组件

前端中的组件是一堆为了实现同一业务逻辑的代码文件的组合，将相关文件都放到同一个目录中，就形成了一个独立性非常强的组件。

Angular 中使用了Web Component 的标准来实现组件化：[Web Component](../前端进阶/WebComponent/README.md)

组件是 Angular 应用的最小的逻辑单元，模块则是在组件之上的一层抽象。组件以及其他部分，如指令、管道、服务、路由等都可以被包含到一个模块中，外部通过引用这个模块来使用一系列封装好的功能。

可以把 Angular 应用想象成一棵树，模块是这棵树的树枝，组件是这棵树的叶子，每个 Angular 应用都必须要有一个根模块（树干），并且根模块中必须通过 Bootstrap 指定根组件，用于启动 Angular 应用。

## 创建组件 

创建组件跟简单，可以通过一下三个步骤创建组件：

1. 从 `@angular/core` 中引入 `Component` 装饰器;
2. 建立一个普通的类，并用 `@Component` 修饰它;
3. 在 `@Component` 中，设置 `selector` 自定义标签和 `template/templateUrl` 模板以及 `styles/styleUrls` 样式。

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent { }
```

> 在新版的 Angular 中自定义标签需要以 `app-` 开头，否则会报错。

以上代码会创建一个最简单的 Angular 组件，使用这个组件需要在 HTML 中添加 `<app-root></app-root>` 标签，然后 Angular 便会在此标签中插入组件中指定的模板。

## 组件的基础构成

组件由组件装饰器、组件元数据、模板和组件类组成。先来了解一下组件装饰器和组件类，后面有章节详细说明组件元数据和模板。

### 组件装饰器( Component Decorator )

每个组件类必须使用 `@Component` 进行修饰才能成为 Angular 组件; `@Component` 是 TypeScript 的语法，它是一个装饰器，任何一个 Angular 的组件都会用这个装饰器修饰，如果移除了这个装饰器，它将不再是 Angular 组件了。

### 组件类

组件实际上也是一个普通的类，组件的逻辑都在组件类里定义并实现。