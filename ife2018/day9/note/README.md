# day9~11 2018.5.2~2018.5.4

## 切图

### 推荐设置

移动工具设置：快捷键V——上方属性栏，自动选择不要勾选，冒号后，选中图层。当，想选中一个图层时，按住ctrl+左键，就会选中此图层，并可以拖拽  
视图设置：上方菜单栏-视图-显示-智能参考线（切图会提供很大帮助）  
打开标尺：上方菜单栏-视图-标尺（也可以ctrl+r）  
窗口设置：不需要的统统关闭；库、颜色、右侧的：通道、路径等关闭，只留四大面板在右面信息和字符（放上面），图层和历史记录（放下面）  
信息设置：单击信息右侧的设置-面板选项：第一第二颜色模式：RGB；标尺单位：像素；文档尺寸勾选  
编辑设置：菜单栏-编辑-首选项-单位与标尺，将标尺和文字都改为像素  
小经验：
选中一个图层：右下角图层位置，ctrl+点击，在图片中形成一个选区，并且选区的信息会出现在面板中；如果选中字的话，字体信息也会显示在面板上。  
建议：窗口-工作区-新建工作区：取名，并勾选两个选项：此方法可以保存之前的设置信息，以免，软件设置复位基本功能后，找不回之前的设置。

### 切图方法

[https://www.cnblogs.com/w-wanglei/p/5598336.html](https://www.cnblogs.com/w-wanglei/p/5598336.html)

## 透明

1. css3的opacity:x，x 的取值从 0 到 1，如opacity: 0.8
2. css3的rgba(red, green, blue, alpha)，alpha的取值从 0 到 1，如rgba(255,255,255,0.8)
3. IE专属滤镜 filter:Alpha(opacity=x)，x 的取值从 0 到 100，如filter:Alpha(opacity=80)

## 过渡效果 `transition`

> 我们可以在不使用 Flash 动画或 JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。

CSS transform 属性 , 只对 `block` 级元素生效！

示例:

```css
div
{
transition: width 2s;
-moz-transition: width 2s;	/* Firefox 4 */
-webkit-transition: width 2s;	/* Safari 和 Chrome */
-o-transition: width 2s;	/* Opera */
}
```

值:

属性|描述
---|---
transition|简写属性，用于在一个属性中设置四个过渡属性。
transition-property|规定应用过渡的 CSS 属性的名称。
transition-duration|定义过渡效果花费的时间。默认是 0。
transition-timing-function|规定过渡效果的时间曲线。默认是 "ease"。
transition-delay|规定过渡效果何时开始。默认是 0。