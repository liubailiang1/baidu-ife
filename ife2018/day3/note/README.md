## day3 2018.4.26

#### CSS简介

1. 作用: 样式化和排版网页
2. 定义: 用于向用户指定文档如何呈现的语言
3. 工作: 浏览器将HTML和CSS转化成DOM，并显示DOM的内容。  
浏览器会解析HTML并通过它创建DOM，之后解析CSS
4. 语法:
![规则](https://mdn.mozillademos.org/files/3668/css%20syntax%20-%20ruleset.png) 
`CSS规则 = 选择器 + 声明块` 
![声明块](https://mdn.mozillademos.org/files/3667/css%20syntax%20-%20declarations%20block.png)
`声明块 = {多条声明}``声明 = 属性:属性值;`

> 样式表除了CSS规则外还有@规则(用来传递元数据、条件信息和其它描述性信息)、嵌套规则 —— 比如可用@import引入其他CSS文件;可用@media(){}来区别不同设备应用不同的样式

<hr>

#### CSS选择器(1)

> 选择器: 用于定位我们想要样式化的网页HTML元素，便于精准选择要样式化的元素

##### 简单选择器:

`基于元素类型(或其class id)直接匹配文档的一个或多个元素`

分类|说明|示例
---|---|---
元素选择器|选择指定类型的元素|p {}
类选择器|选择指定的class属性的元素|.part {}
ID选择器|选择指定id的单个元素|#part1 {}
通用选择器|选择一个页面上的所有元素|* {}

##### 属性选择器: 

`根据元素的属性和属性值匹配元素`

分类|情况|说明
---|---|---
存在和值属性选择器|[attr] {}|包含attr属性的所有属性
 |[attr=val] {}|attr 属性被赋值为 val 的所有元素
 |[attr~=val] {}|attr 属性的值（以空格间隔出多个值）中有包含 val 值的所有元素
子串值属性选择器|[attr	&brvbar;=val] {}|attr属性的值是 val 或值以 val- 开头的元素）。
 |[attr^=val]|attr属性的值以val开头（包括 val）的元素。
 |[attr$=val]|attr属性的值以val结尾（包括 val）的元素。
 |[attr*=val]|attr属性的值中包含字符串 val 的元素。
 
<hr>

#### 字体属性

属性|说明|值|备注
---|---|---|---
color|改变前景内容(文本)和text-decoration的线的颜色|
font-family|设置字体||[安全字体](https://www.cssfontstack.com/)
font-size|字体大小||单位:px(绝对)、em(父元素的字体大小)、rem(根元素的字体大小,通常为16px)
font-style|斜体|normal、italic、oblique|oblique为在没有斜体版本下模拟斜体
font-weight|粗体|normal、bold、lighter、bolder、100-900|
text-transform|转换|none、uppercase(大写)、lowercase(小写)、capitalize(首字母大写)、full-width|
text-decoration|文本划线|none、underline、overline、line-through|
text-shadow|文字阴影|水平偏移 垂直偏移 模糊半径 基础颜色|
text-align|文本对齐|left、right、center、justify|相对于盒子
line-height|行高||[深入理解line-height](http://www.zhangxinxu.com/wordpress/2009/11/css%E8%A1%8C%E9%AB%98line-height%E7%9A%84%E4%B8%80%E4%BA%9B%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E5%8F%8A%E5%BA%94%E7%94%A8/)
letter-spacing|字母间距||
word-spacing|单词间距||
text-indent|文本块中首行文本的缩进||

<hr>

#### 验证

1. 什么是CSS，CSS是如何工作的  
```
CSS是向用户指定文档如何呈现的语言;
浏览器将HTML和CSS转化成DOM，并显示DOM的内容
```
2. CSS的基本语法是怎样的  
```css
选择器 {
	属性:属性值; //声明
}
```
3. CSS选择器是什么概念，简单选择器和属性选择器是什么  
```
定位需要样式化的元素;
简单选择器是基于元素类型(或其class id)直接匹配文档的一个或多个元素;
属性选择器是根据元素的属性和属性值匹配元素
```
4. 文本样式都有哪些相关属性，对应哪些值  
```
见上方表格
```
