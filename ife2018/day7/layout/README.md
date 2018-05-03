* 1 实现一个两栏布局，左侧占30%宽度，右侧占70%宽度
  * [1.1 双float](#11-双float)
  * [1.2 绝对定位](#12-绝对定位)
  * [1.3 flex](#13-flex)
* 2 实现一个两栏布局，左侧固定宽度，右侧根据浏览器宽度进行自适应变化
  * [2.1 float+margin](#21-float+margin)
  * [2.2 float+BFC](#22-float+BFC)
  * [2.3 absolute+margin](#23-absolute+margin)
  * [2.4 flex](#24-flex)
* 3 实现一个两栏布局，右侧固定宽度，左侧根据浏览器宽度进行自适应变化
  * 类似于上例
* 4 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化
  * [4.1 浮动法](#41-浮动法)
  * [4.2 定位法](#42-定位法)
  * [4.3 圣杯](#43-圣杯)
  * [4.4 双飞翼](#44-双飞翼)
  * [4.5 flex](#45-flex)
* 5 实现一个三栏布局，左侧固定宽度，中间固定宽度，右侧根据浏览器宽度变化而自适应变化
  * 类似于上例
* 6 

## 1 实现一个两栏布局，左侧占30%宽度，右侧占70%宽度

```html
<div class="page">
    <div class="left"></div>
    <div class="right"></div>
</div>
```

### 1.1 双float

```css
.left, .right {
    float: left;
    height: 200px;
}
.left {
    width: 30%;
    background-color: red;
}
.right {
    width: 70%;
    background-color: yellow;
}
```

示例: [demo](11.html)

### 1.2 绝对定位

```css
.page {
    position: relative;
}
.left,
.right {
    height: 200px;
}
.left {
    position: absolute;
    top: 0;
    left: 0;
    width: 30%;
    background-color: red;
}
.right {
    position: absolute;
    top: 0;
    left: 30%;
    width: 70%;
    background-color: yellow;
}
```

示例: [demo](12.html)

### 1.3 flex

```css
.page {
    display: flex;
}
.left,
.right {
    height: 200px;
}
.left {
    flex: 0 0 30%;
    background-color: red;
}
.right {
    flex: 0 0 70%;
    background-color: yellow;
}
```

示例: [demo](13.html)

## 2. 实现一个两栏布局，左侧固定宽度，右侧根据浏览器宽度进行自适应变化

```html
<div class="page">
    <div class="left">左 固定300px</div>
    <div class="right">右 这边是自适应文本 实现一个两栏布局，左侧固定宽度，右侧根据浏览器宽度进行自适应变化</div>
</div>
```

### 2.1 float+margin

```css
.page {
    zoom: 1;
}
.page:after {
    content: " ";
    display: block;
    height: 0;
    clear: both;
}
.left,
.right {
    min-height: 300px;
}
.left {
    float: left;
    width: 300px;
    background-color: red;
}
.right {
    margin-left: 300px
    background-color: yellow;
}
```

示例: [demo](21.html)

### 2.2 float+BFC

```css
.page {
    zoom: 1;
}
.page:after {
    content: " ";
    display: block;
    height: 0;
    clear: both;
}
.left,
.right {
    min-height: 300px;
}
.left {
    float: left;
    width: 300px;
    background-color: red;
    margin-right: 10px;
}
.right {
    overflow: hidden;
    background-color: yellow;
}
```

示例: [demo](22.html)

### 2.3 absolute+margin

```css
.page {
    position: relative;
}
.left,
.right {
    min-height: 300px;
}
.left {
    position: absolute;
    top: 0;
    left: 0;
    width: 300px;
    background-color: red;
}
.right {
    margin-left: 310px;
    background-color: yellow;
}
```

示例: [demo](23.html)

### 2.4 flex

```css
.page {
    display: flex;
}
.left,
.right {
    min-height: 300px;
}
.left {
    flex: 0 0 300px;
    background-color: red;
}
.right {
    flex: 1 1 auto;
    background-color: yellow;
}
```

示例: [demo](24.html)

## 3 实现一个两栏布局，右侧固定宽度，左侧根据浏览器宽度进行自适应变化

类似于前例

## 4 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化

### 4.1 浮动法

```html
<div class="left">左 宽度300px</div>
<div class="right">右 宽度300px</div>
<div class="center">中 自适应</div>
```

```css
.center {
    margin: 0 300px;
    height: 300px;
    background-color: red;
}
.left, .right {
    width: 300px;
    height: 300px;
    background-color: yellow;
}
.left {
    float:left;
}
.right {
    float:right;
}
```

示例: [demo](41.html)

### 4.2 定位法

```html
<div class="left">左 宽度300px</div>
<div class="center">中 自适应 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化</div>
<div class="right">右 宽度300px</div>
```

```css
.center {
    margin: 0 300px;
    height: 300px;
    background-color: red;
}
.left, .right {
    position: absolute;
    top: 0;
    width: 300px;
    height: 300px;
    background-color: yellow;
}
.left {
    left: 0;
}
.right {
    right: 0;
}
```

示例: [demo](42.html)

### 4.3 圣杯

```html
<div class="container">
    <div class="center">中 自适应 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化</div>
    <div class="left">左 宽度300px</div>
    <div class="right">右 宽度300px</div>
</div>
```

```css
.container {
    height: 100%;
    min-width: 300px;
    padding: 0 300px;
    overflow: hidden;
}
.center {
    float: left;
    width: 100%;
    height: 300px;
    background-color: red;
}
.left {
    float: left;
    position: relative;
    left: -300px;
    width: 300px;
    height: 300px;
    margin-left: -100%;
    background-color: yellow;
}
.right {
    float: left;
    position: relative;
    right: -300px;
    width: 300px;
    height: 300px;
    margin-left: -300px;
    background-color: blue;
}
```

示例: [demo](43.html)

### 4.4 双飞翼
```html
<div class="container">
    <div class="main">
        <div class="center">中 自适应 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化</div>
    </div>
    <div class="left">左 宽度300px</div>
    <div class="right">右 宽度300px</div>
</div>
```

```css
.container {
    height: 100%;
    min-width: 300px;
    overflow: hidden;
}
.main .center {
    margin: 0 300px;  /* 与圣杯的区别 */
}
.main {
    float: left;
    width: 100%;
    height: 300px;
    background-color: red;
}
.left {
    float: left;
    width: 300px;
    height: 300px;
    margin-left: -100%;
    background-color: yellow;
}
.right {
    float: left;
    width: 300px;
    height: 300px;
    margin-left: -300px;
    background-color: blue;
}
```

示例: [demo](44.html)

### 4.5 flex
```html
<div class="container">
    <div class="left">左 宽度300px</div>
    <div class="center">中 自适应 实现一个三栏布局，左侧固定宽度，右侧固定宽度，中间部分宽度随浏览器宽度变化而自适应变化</div>
    <div class="right">右 宽度300px</div>
</div>
```

```css
.container {
    display: flex;
}
.left, .right {
    flex: 0 0 300px;
    min-height: 300px;
}
.center {
    flex: 1 1 auto;
    background-color: yellow;
    min-height: 300px;
}
.left {
    background-color: red;
}
.right {
    background-color: blue;
}
```

示例: [demo](45.html)

## 5 实现一个三栏布局，左侧固定宽度，中间固定宽度，右侧根据浏览器宽度变化而自适应变化

类似于上例

## 6 练习

[![img](img/ife.png)](../index.html)



