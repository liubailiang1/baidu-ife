# day16 2018.5.14

## 1. JavaScript实现

ECMAScript、文档对象模型(DOM)、浏览器对象模型(BOM)

### 1.1 ECMAScript

`ECMA-262`中定义的标准，用于创建通用目的的脚本语言。提供核心语言功能

> `ECMA-262`是由Ecma国际发布的标准。包含通用目的的脚本语言规范

`ECMAScript`宿主环境包括: 浏览器、Node、Adobe Flash

`ECMAScript`规定了: 语法、类型、语句、关键字、保留字、操作符、对象

### 1.2 DOM

`DOM`是针对XML但经过扩展用于HTML的应用程序编程接口(API)。提供访问和操作网页内容的方法和交口

`DOM`把整个页面映射为一个多层节点结构

### 1.3 BOM

`BOM`可以访问和操作浏览器窗口。提供与浏览器交互的方法和接口

## 2 加入JavaScript代码

为了使先呈现出页面的内容，现代一般把全部的JavaScript引用放到`<body>`中

```html
<script src="">
</script>
```

包含在`<script>`元素中的代码将被从上至下依次解释

