# DOM 节点与元素

## DOM 节点

根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：

* 整个文档是一个文档节点
* 每个 HTML 元素是元素节点
* HTML 元素内的文本是文本节点
* 每个 HTML 属性是属性节点
* 注释是注释节点

HTML DOM 将 HTML 文档视作树结构。这种结构被称为节点树。

### 节点间关系

| 方法 | 关系 |
|:----:|:----:|
| node.parentNode | 父节点 |
| node.childNodes | 所有直接子节点 |
| node.firstChild | 第一个直接子节点 |
| node.lastChild | 最后一个直接子节点 |
| node.previousSibling | 前一个兄弟 |
| node.nextSibling | 后一个兄弟 |

**强调**: 文本节点也是节点对象，以上6个关系都会受看不见的空文本的干扰。

## DOM 元素

DOM 元素是仅包含元素节点的树结构，用来添加、删除和替换 HTML 元素。

### 节点间关系

| 方法 | 关系 |
|:----:|:----:|
| node.parentElement | 父元素 |
| node.children | 所有直接子元素 |
| node.firstElementChild | 第一个直接子元素 |
| node.lastElementChild | 最后一个直接子元素 |
| node.previousElementSibling | 前一个兄弟元素 |
| node.nextElementSibling | 后一个兄弟元素 |

**强调**: 元素树不会受空文本的干扰，childNodes和children: 返回的是动态集合。

## 按选择器查找

1. 只查找一个符合选择器条件的元素:

```js
const elem=parent.querySelector("selector")`
```
    查找任意父元素下，符合选择器selector要求的一个子元素

2. 查找多个符合选择器条件的元素：

```js
const elems = parent.querySelectorAll("selector");
```
    查找任意父元素下，符合选择器selector要求的所有子元素.

## 将新元素添加到指定父元素下

```js
parent.appendChild(a);
parent.insertBefore(a,oldElem);
parent.replaceChild(a,oldElem);
```

## 克隆元素

```js
elem.cloneNode(); // 浅克隆，只复制元素本身，不复制内容；
elem.cloneNode(true); // 深克隆，既复制元素本身，又复制内容
```

## 遍历子代节点

*遍历所有子代节点：`NodeIterator`;

  1. 创建NodeIterator对象
```js
const iterator = document.createNodeIterator(root, NodeFilter.SHOW_ALL,null, false);
```
    root-开始节点对象

  2. 反复调用 iterator 的 nextNode 方法

* 任意跳转：TreeWalker;
```js
var walker = document.createTreeWalker(root, NodeFilter.SHOW_ALL,null, false);
```
    root-开始节点对象