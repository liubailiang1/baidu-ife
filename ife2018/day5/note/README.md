## day5~6 2018.4.28~2018.4.29

#### 1. 盒子模型

![盒子模型](https://mdn.mozillademos.org/files/13647/box-model-standard-small.png)

盒子的宽度 = margin-left + border-left + padding-left + 
width + padding-right + border-right + margin-right

##### 1.1 内容区

`width`和`height`是框内容显示的区域——包括框内的文本内容，以及表示嵌套子元素的其他框

> 也可以使用`min-width`、`max-width`、`min-height`、`max-height`来设置最低/最高限度的width和height

默认情况下，`width`和`height`只包括内容区域的宽和高，不包括border、padding、margin。  
使用`box-sizing`可以使其包含content、padding、border

`box-sizing`的值:

```css
/* 默认值，标准盒子模型，只含内容区 */ 
box-sizing:content-box;
/* width 和 height 属性包括内容，内边距和边框，但不包括外边距 */ 
box-sizing:border-box;
```

##### 1.2 内边距

padding

##### 1.3 边框

[border 详见day3的笔记](https://yuqy96.github.io/baidu-ife/ife2018/day4/note/)

##### 1.4 外边框

margin

> 外边距塌陷: **块级元素**的**上外边距和下外边距**有时会合并（或折叠）为一个外边距，其大小取其中的最大者  
>1. 相邻兄弟元素margin合并  
>2. 父级和第一个/最后一个子元素  
>3. 空块级元素的margin合并


##### 1.5 注意点

1. 框的高度不能使用百分比长度
2. border不能使用百分比长度
3. 如果内容区过大，将会溢出，此时可使用overflow

overflow的值:

```css
/* 默认值。内容不会被修剪，会呈现在元素框之外  */
overflow: visible;
/* 内容会被修剪，并且其余内容不可见  */
overflow: hidden;
/* 内容会被修剪，浏览器会显示滚动条以便查看其余内容  */
overflow: scroll;
/* 由浏览器定夺，如果内容被修剪，就会显示滚动条  */
overflow: auto;
```

##### 1.6 框类型 `display`

值|说明
---|---
block|块框（ block box）是定义为堆放在其他框上的框（例如：其内容会独占一行），而且可以设置它的宽高，之前所有对于框模型的应用适用于块框 （ block box）
inline|行内框（ inline box）与块框是相反的，它随着文档的文字（例如：它将会和周围的文字和其他行内元素出现在同一行，而且它的内容会像一段中的文字一样随着文字部分的流动而打乱），对行内盒设置宽高无效，设置padding, margin 和 border都会更新周围文字的位置，但是对于周围的的块框（ block box）不会有影响。
inline-block|行内块状框（inline-block box） 像是上述两种的集合：它不会重新另起一行但会像行内框（ inline box）一样随着周围文字而流动，而且他能够设置宽高，并且像块框一样保持了其块特性的完整性，它不会在段落行中断开。
table|像处理table布局那样处理非table元素，而不是滥用HTML的&lt;table>;标签来达到同样的目的。
flex|处理一些困扰CSS已久的一些传统布局问题，例如布置一系列弹性等宽容器或者垂直居中内容。
grid|给出一种简单实现CSS网格系统的方式，而在传统上它依赖于一些棘手难以处理的CSS网格框架

----

#### 2.浮动 `float`

##### 2.1 浮动的背景和工作原理

浮动的最初是用来**让文字环绕图片**, 所以我能能推出:  
浮动会**脱离**正常的文档流，并吸附到其父容器左边，正常布局中位于浮动元素下的内容会**围绕**着浮动元素

##### 2.2 浮动的块状性和去空格

> 设置float属性后，元素实际上会inline-block块状化

> 多个img都浮动会去除掉他们间的空格

##### 2.3 浮动的包裹性

包裹性指的是元素尺寸刚好容纳内容, 表现得就像`diaplay:inline-block`一样

具有包裹性的其他属性:

```css
display:inline-block
position:absolute/fixed/sticky
overflow:hidden/scroll
```

##### 2.4 浮动的破坏性

会使父元素**高度塌陷**——为了实现文字环绕效果

具有破坏性的其他属性:

```css
display:none
position:absolute/fixed/sticky
```

怎么解决破坏性带来的问题呢？

##### 2.5 清除浮动 (clearfix hack)

###### 2.5.1 投机取巧法

在父元素底部加上`<div style="clear:both;"></div>`

虽说兼容性好，但是浪费一个标签，违反了**语义化**，不推荐

###### 2.5.2 overflow + zoom法

----
补充知识: BFC(Block Formatting Context)

BFC:块级格式化上下文【在css3中叫Flow Root】是一个独立布局环境，相邻盒子margin垂直方向会重叠。
  
什么样的元素会为其内容生成一个BFC呢？
  
1. 浮动元素，即float:left/right  
2. 绝对定位元素，即position:absolute/fixed  
3. 块容器，即display:table-cell/table-caption/inline-block    
4. 设置了除visible外的overflow值的块盒子，即overflow:hidden/scroll/auto

BFC特性：

1. 创建了BFC的元素中，**子浮动元素也会参与高度计算**  
2. 与浮动元素相邻的、创建了BFC的元素，都不能与浮动元素相互覆盖
3. 创建了BFC的元素不会与它们的子元素margin重叠

----

因为子浮动元素也会参与高度计算, 所以借此可以得到以下方法:

```css
.fix {
	overflow:hidden; zoom:1;
}
```

方法不错，但是可能内容会被裁减掉，可以偶尔用用

###### 2.5.3 after + zoom法

看一下2.5.1，虽然不错，但是违反语义化; 所以就想到了通过CSS来添加子元素，不修改HTML代码 —— `:after`选择符

```css
.clearfix:after {
	content: " ";  //content可以任意发挥
	display: block;
	line-height: 0;  //height: 0也行
	clear: both;
}
.clearfix {
    zoom: 1; 
}
```

这个方法最佳, 推荐这个方法

##### 2.5 浮动布局

> 转发自 [CSS深入理解之float浮动(张鑫旭)](https://www.imooc.com/learn/121)

###### 2.5.1 单侧尺寸固定的流体布局

法一: 改变DOM位置:

![img](https://yuqy96.github.io/baidu-ife/ife2018/day5/img/1.png)

1. width+float  
2. margin-left/padding-left

法二: 不改变DOM位置:

![img](https://yuqy96.github.io/baidu-ife/ife2018/day5/img/2.png)

2嵌在1中

1. width:100%+float:left（自适应的容器外）
2. padding-right/margin-right
3. width+float+margin(负)

###### 2.5.2 两侧都适应的流体布局

> 原理是左栏浮动，右栏生成BFC，根据BFC特性与浮动元素相邻的、创建了BFC的元素，都不能与浮动元素相互覆盖。

![img](https://yuqy96.github.io/baidu-ife/ife2018/day5/img/3.png)

1. float
2. display:table-cell/inline-block
