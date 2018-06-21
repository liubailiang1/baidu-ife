# day20~21

## 1. 事件

### 1.1 定义

1. 事件类型: 说明发生什么类型事件的字符串, 例如: mousemove、click
2. 事件目标: 发生的事件或与之相关的对象, 例如: Window、Document、Element
3. 事件处理程序/事件监听程序: 处理或相应事件的函数
4. 事件对象: 与特定事件相关且包含有关该事件详细信息的对象
5. 事件传播: 浏览器决定哪个对象触发其事件处理程序

### 1.2 事件类型

分类|类型|说明
---|---|---
表单|submit|表单提交, 返回false取消提交
 |reset|表单重置
 |click|表单元素激活
 |change|改变表单元素所代表的值
 |focus|收到键盘的焦点
 |blur|失去焦点
Window|load|所有外部资源完全加载并显示给用户时
 |unload|用户离开当前文档, 转向其他文档(不能取消转向)
 |beforeunload|提供询问用户是否离开的机会
 |focus/blur|浏览器窗口获得/失去键盘焦点
 |resize|调整浏览器窗口大小
 |scroll|浏览器滚动
鼠标|mousemove|移动或拖动鼠标
 |mousedown|按下鼠标
 |mouseup|释放鼠标按键
 |dblclick|双击
 |contextmenu|右键菜单
 |mouseover|悬停元素上(冒泡)
 |mouseout|不再悬停元素上(冒泡)
 |mouseenter|悬停元素(不冒泡)
 |mouseleave|不再悬停元素上(不冒泡)
 |mousewheel|滚动鼠标滚轮
键盘|keydown|按下键盘
 |keyup|释放键盘
 |keypress|keydown事件产生可打印字符

> 鼠标事件对象:  
> 1. clientX/clientY: 鼠标的位置;  
> 2. altkey、ctrlkey、metaKey、shiftKey 键盘辅助键状态

> 键盘事件对象:  
> 1. keyCode: 按下或释放的键是哪个
> 2. altkey、ctrlkey、metaKey、shiftKey 键盘辅助键状态

### 1.3 注册事件处理程序


## 2 DOM样式

1. 使用obj.className来修改样式表的类名
2. 使用obj.style.cssTest来修改嵌入式的css
3. 使用obj.style.xxx
4. 使用更改外联的css文件，从而改变元素的css

```javascript
obj.style.backgroundColor= "black";
obj.style.cssText = "display:block;color:White;"
obj.setAttribute("class", "style2");
obj.setAttribute("href","css2.css");
```