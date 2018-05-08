# day12~15 2018.5.8~2018.5.9

## 遇到的问题

### css 实现div内显示两行或三行，超出部分用省略号显示

一、div内显示一行，超出部分用省略号显示

```css
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

二、div内显示两行或三行，超出部分用省略号显示

```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;（行数）
-webkit-box-orient: vertical;
```

### 实现中间有文字的分割线效果

```html
<div class="box">
  <span class="line"></span>
  <span class="text">我的文字</span>
  <span class="line"></span>
</div>
```
```css
.box {
  height: 40px;
  width: 300px;
  background-color: wheat;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.line {
  height: 2px;
  flex-grow: 1;
  background-color: red;
}
```