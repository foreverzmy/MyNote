# html标准属性:

## 核心DOM: 万能，繁琐 

| 属性/方法 | 类型 |作用|
|:--------|:----|:---|
| elem.attributes['i/属性名']; | Object | 获得属性节点对象 |
| elem.getAttributeNode('属性名'); | Object | 获得属性节点对象 |
| node.getAttribute('属性名'); | String | 直接获得属性值 |
| node.value / node.nodeValue; | String | 获得节点值 |
| elem.setAttribute('属性名','属性值'); |  | 修改属性值 |
| elem.hasAttribute(属性名); | | 判断是否包含属性 |
| elem.removeAttribute(属性名); |  | 移除属性 |


## HTML DOM: 

```js
elem.属性名
```
attribute 万能，但是只能获得和修改页面存在且有值的属性，而 DOM 可以定义自定义属性: `data-属性名=""`;
 
访问: 凡是data-开头的自定义属性，都在程序中用“dataset.属性名”方式访问

## 修改样式表中的样式:——不建议使用
   
1. 获得样式表对象:`var sheet=document.styleSheets[i];`
2. 获得要修改的cssRule对象: `var rule=sheet.cssRules[i];`
3. 改属性值:`rule.style.属性名=值;`