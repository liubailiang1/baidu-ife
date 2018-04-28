## day4 2018.4.27

#### 背景 background

```
背景指的是元素内容、内边距和边界下层的区域
(可用background-clip修改)
```

属性|说明|值|备注
---|---|---|---
background-color|背景色||建议加上，作为后备，以防背景图像无法加载
background-image|背景图像|url(...)、渐变: linear-gradient(to 渐变的方向,开始的颜色,结尾的颜色)|渐变可以在中途选择其他的点
background-repeat|背景重复|repeat(默认)、repeat-x、repeat-y、no-repeat|
background-position|背景定位|关键字、百分数值、长度值|坐标系为x坐标从左到右,y坐标从上到下;可以用于[雪碧图](http://www.imooc.com/learn/93)
background-attachment|背景附着|scroll(默认)、fixed|
background-size|背景图像大小|长度值、百分数值、cover、contain|
background|背景简写||可按任意顺序放置

<hr>

#### 边框 border

属性|说明|值|备注
---|---|---|---
border|边框简写|[border-width border-style border-color /inherit]|三角形和梯形可以使用border+transparent来做
border-style|边框样式|none、hidden、dotted、dashed、solid、double、(groove、ridge、inset、outset、)inherit|[样式预览](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-style)
border-width|边框宽度||不支持百分比、默认为medium(3px)
border-color|边框颜色|透明:transparent|默认颜色同color
border-radius|边界圆角||

<hr>

#### 列表 list

属性|说明|值|备注
---|---|---|---
list-style-type|列表标志|[标志值](http://www.w3school.com.cn/cssref/pr_list-style-type.asp)|
list-style-image|列表项图像|url()|可用background代替
list-style-position|列表项位置|inside(文本内文本环绕)、outside(默认)、inherit|
list-style|列表简写|顺序:list-style-type list-style-position list-style-image(可省略某个值)

<hr>

#### 连接 a

根据所处状态决定样式

```css
a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */
```

>注意: 一定要按照LVHA的顺序指定！

可用background为连接增加小图标

[制作导航条的方法](http://www.runoob.com/css/css-navbar.html)

<hr>

#### 选择器(2)

> [选择器参考手册](http://www.w3school.com.cn/cssref/css_selectors.asp)

##### 分组和继承

```
分组: 选择器用逗号分开，被分组的选择器可以分享相同的声明
```

```
继承: 正常情况下，子元素从父元素继承属性
但也会出现特殊情况，只能通过组选择器来对待
```

##### 派生选择器

```css
/* 根据文档的上下文关系来确定某个标签的样式 */
li p {
	
}
```

##### 伪类选择器

> CSS 伪类用于向某些选择器添加特殊的效果。  
CSS 伪元素用于将特殊的效果添加到某些选择器。
  
两者区别在于: 伪类的效果可以通过添加一个实际的`类`来达到，而伪元素的效果则需要通过添加一个实际的`元素`才能达到

###### 伪类
![伪类](http://segmentfault.com/img/bVcccn)

[p:first-child指的是p元素是某元素的第一个子元素](http://www.w3school.com.cn/tiy/t.asp?f=css_sel_firstchild)

###### 伪元素

![伪元素](http://segmentfault.com/img/bVccco)

##### 组合器

[Combinators](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors)|Select
---|---
A,B|匹配满足A（和/或）B的任意元素（参见下方 同一规则集上的多个选择器）.
A B|匹配任意元素，满足条件：B是A的后代结点（B是A的子节点，或者A的子节点的子节点）
A > B|匹配任意元素，满足条件：B是A的直接子节点
A + B|匹配任意元素，满足条件：B是A的下一个兄弟节点（AB有相同的父结点，并且B紧跟在A的后面）
A ~ B|匹配任意元素，满足条件：B是A之后的兄弟节点中的任意一个（AB有相同的父节点，B在A之后，但不一定是紧挨着A)

##### 层叠

>①找出所有相关的规则，这些规则包含于一个给定元素匹配的选择器  
②对显式权重对所有声明排序。标志!important的规则的权重要高于没有!important标志的规则。创作人员的样式>读者的样式。有!important的读者样式强于其他所有样式（读者的重要声明>创作人员的重要声明>创作人员的普通声明>读者的普通声明>用户代理声明）  
③按特殊性排序，特殊性高的优先  
④按出现顺序排序，越后出现的权重就越大。

###### 重要性: 

`!important`总是优先于其他规则

###### 特殊性: 

```
内联样式1000;
ID属性100;
类属性/属性选择/伪类010;
元素/伪元素001
```
