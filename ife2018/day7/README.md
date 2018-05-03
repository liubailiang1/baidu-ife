[1 实现一个两栏布局，左侧占30%宽度，右侧占70%宽度](#%e5%ae%9e%e7%8e%b0%e4%b8%80%e4%b8%aa%e4%b8%a4%e6%a0%8f%e5%b8%83%e5%b1%80%ef%bc%8c%e5%b7%a6%e4%be%a7%e5%8d%a030%25%e5%ae%bd%e5%ba%a6%ef%bc%8c%e5%8f%b3%e4%be%a7%e5%8d%a070%25%e5%ae%bd%e5%ba%a6)

  [1.1 双float](#%e5%8f%8cfloat)
  
  [1.2 绝对定位](#绝对定位)
  
  [1.3 flex](#flex)

## 实现一个两栏布局，左侧占30%宽度，右侧占70%宽度

### 双float

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

### 绝对定位

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

### flex

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



