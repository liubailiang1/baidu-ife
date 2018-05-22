# day22~24 2018.5.21

## 1. 基本数据类型

> ECMAScript共有5种简单的数据类型: `Undefined`、`Null`、`Boolean`、`Number`、`String`  
> **基本类型是按值访问的**

### 1.1 `Undefined`

> 在使用var声明变量但为对其初始化时，这个变量就是undefined

Undefined 和 not defined 的区别:

1. Undefined 为声明了但为初始化； not defined 为尚未声明的报错。
2. 两者使用`typeof`的结果都为 "undefined"

### 1.2 `Null`

> 空对象指针。如果一个变量意在保存对象, 建议用`null`初始化

```javascript
typeof null == "object";  //true
```

undefined 派生自 null，所以 undefined == null

### 1.3 `Boolean`

> true false

转型函数 Boolean():

数据类型|转换为true|转换为false
---|---|---
Boolean|true|false
String|非空字符串|""
Number|非零数字|0/NaN
Object|任何对象|null
Undefined||undefined

### 1.4 `Number`

#### 1.4.1 表示
八进制: 0*  
十六进制: 0x*  
科学计数法: *e\*   e等同于10^

#### 1.4.2 注意点
浮点数相加会溢出

#### 1.4.3 无限
当超出数值范围时，将会转换为infinity/-infinity  
可用`isFinite()`函数判断是否为*有限*

#### 1.4.4 `NaN`

> 表示本应返回数值的操作数未返回数值

* 任何涉及NaN的操作都会返回NaN
* NaN与任何值都不相等

可用`isNaN()`函数判断是否为NaN。会*类型转换*。

#### 1.4.5 转为Number

##### 1.4.5.1 `Number()`

数据类型|转换
---|---
Boolean|true->1; false->0
String|""->0;
 |只包含数字/浮点数/十六进制->对应的十进制/浮点数(忽略前导的0)
 |其他->NaN
Object|先调用`valueOf()`，若结果为NaN，继续调用`toString()`
 |null->0
Undefined|NaN

##### 1.4.5.2 `parseInt()`

> 专用于字符串的处理

1. 忽略掉前面的空格。  
2. 若第一个非空格字符不为有效数字/ "" -> NaN  
3. 若第一个非空格字符为有效数字，继续解析第二个字符，直到解析所有字符，或遇到了非数字字符  
4. 遇到八进制、十六进制也能识别并解析为十进制
5. 可用第二个参数，指明第一个参数是什么进制

##### 1.4.5.3 `parseFloat()`

> 专用于字符串的处理

类似于`parseInt()`。只用于解析十进制，十六进制将被解析为0

### 1.5 `String`

"" / ''  
`length`属性可知道字符串长度

#### 转为String:

①数值/布尔值/对象/字符串(除null/undefined)都有 `toString()`方法:
数值使用时，可传入参数决定输出字符串的进制

②`String()`函数 <=> `toString()`方法 + null + undefined

③ + ""

### 1.6 `Object`

所有实例均有的属性

属性/方法|说明
---|---
constructor|创建当前对象的函数
hasOwnProperty  (propertyName)|给定属性(字符串)是否在对象实例
isPrototypeOf(object)|传入对象是否是当前对象原型
propertyIsEnumerable  (propertyName)|给定属性是否能用for-in列举
toLocaleString()|对象的字符串表示（地区）
toString()|对象的字符串表示
valueOf()|对象的字符串、数值、布尔值表示

## 2. 引用类型

> **引用类型是按引用访问的**


## 3. 基本类型与引用类型的区别