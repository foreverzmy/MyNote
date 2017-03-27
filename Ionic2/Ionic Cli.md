# Ionic Cli 安装与使用

Ionic2 应用使用 `ionic cli` 创建，使用 Cordova 打包成本地应用。在安装 `ionic cli` 之前，需要先安装 Node.js。

## 安装

* 安装 ionic

```npm
npm i -g ionic
```

* 安装 Cordova

```npm
npm i -g cordova
```

## 使用

###　创建新项目

```npm 
ionic start MyIonic2Project --v2
```

* 注意

1. 也可以不加 `--v2`，默认就是 ionic2 版本的项目。

2. 创建的项目默认会使用 [tabs](https://github.com/driftyco/ionic2-starter-tabs) 模板，如果默认模板不是您想要使用的，Ionic有几个模板可用：

  * tabs：一个简单的3标签布局
  * sidemenu：一边有一个可滑动菜单的布局
  * blank：一个空白的项目
  * super：启动项目超过14个可以使用的页面设计
  * tutorial：指导启动项目


### 启动项目

在项目根目录下运行以下命令:

```npm
ionic serve
```

浏览器会自动打开一个地址为 `http://localhost:8100` 的窗口，端口号根据当前PC的实际情况可能会有变化，如果 `8100` 被占用了会使用 `8101` 等。