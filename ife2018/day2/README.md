## day2 2018.4.25

#### HTML元素总结

[W3school标签列表](http://www.w3school.com.cn/tags/html_ref_byfunc.asp)

[W3C](https://www.w3.org/TR/2017/REC-html52-20171214/semantics.html#the-html-element)

说明：

* `<tt> <i> <b> <big> <small>`等字体样式标签和`<em> <strong> <dfn> <code> <samp> <kbd> <var> <cite>`等短语标签，如果只是为了改变样式的话，建议使用样式表

#### Web语义化

* 目的：用机器可读的、被广泛认可的语义信息来描述内容
* 理解：让机器能够读懂，使用正确的标签，合适的class id，方便爬虫、阅读
* 指南：[阮一峰HTML编写指南](http://www.ruanyifeng.com/blog/2009/05/guide_to_semantic_html_elements.html)

#### 验证

* HTML是什么，HTML5是什么
> HTML(超文本标记语言Hyper Text Markup Language)是一种描述网页的标记语言  
> HTML5是最新的HTML标准，拥有新的元素，更丰富的内容，更强大的适配性

* HTML元素标签、属性都是什么概念？
> HTML元素标签组成了HTML文档，指的是在开始标签和结束标签之间的所有内容  
> HTML属性为HTML标签提供了更多的信息

* 文档类型是什么概念，起什么作用？
> DOCTYPE 文档类型，用来说明所用html的类型，指出应该用什么规则去解释文档

* meta标签都用来做什么的？
> 提供有关页面的元信息，常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。

* Web语义化是什么，是为了解决什么问题
> 使用正确的标签，公认的class id，建立更优化的标准，方便机器、人读懂代码想要表达的意思。让爬虫等能更好的理解到HTML文档

* 链接是什么概念，对应什么标签？
> 指从一个网页指向一个目标的连接关系  
> 1. \<link> 可以链接到一个外部样式表  
> 2. \<a> 超链接

* 常用标签都有哪些，都适合用在什么场景
> \<div> 可用于划分网页的区域，表示页面的分栏，分离一个版块的正文、评论、文章等  
> \<p> 文本段落，不能包含其他块级元素  
> \<h1>~\<h6> 用于标题  
> \<a> \<img>  
> 表单标签、列表标签

* 表单标签都有哪些，对应着什么功能，都有哪些属性
> [表单总结](https://www.jianshu.com/p/711c2c3386be)  
> \<form> 向服务器传输数据 action代表该表单数据要提交到的服务器地址，method表示提交方式
>
```html
<!-- 常用输入框，用于文本输入 -->
<input type="text" name="text" placeholder="请输入">
<!-- 密码输入，非明文显示 -->
<input type="password" name="text" placeholder="密码">
<!-- 单选框，往往两个以上出现 -->
<input type="radio" name="sex">男
<input type="radio" name="sex">女
<!-- 多选框 -->
<input type="checkbox" name="hobby">旅游
<input type="checkbox" name="hobby">宠物
<!-- 按钮 -->
<input type="button" value="点我">
<!-- 文本域 -->
<textarea name="comment" id="comment" cols="50" rows="10"></textarea>
<!-- 下拉框 -->
<select name="car" id="car">
    <option value="1">宝马</option>
    <option value="2">奔驰</option>
    <option value="3" selected>特斯拉</option>
</select>
```

* ol, ul, li, dl, dd, dt等这些标签都适合用在什么地方，举个例子
> ol 有序列表
> ul 无序列表
> dl 术语列表，dt表示术语，dd表示定义
> 列表可用于制作导航

PS：markdown几个转义字符：

描述|实体名称|实体编号
---|---|---
&nbsp;|空格|&nbsp
&lt;|小于号|&lt
&gt;|大于号|&gt
&amp;|与号|&amp
&quot;|引号|&quot
&apos;|撇号|&apos