# day22~24 2018.5.21/5.30

## 1. 基本数据类型

> ECMAScript共有5种简单的数据类型: `Undefined`、`Null`、`Boolean`、`Number`、`String`  
> **基本类型是按值访问的**

### 1.1 `Undefined`

> 在使用var声明变量但未对其初始化时，这个变量就是`undefined`

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

 |Number()|parseInt()|parseFloat()
---|---|---|---
十进制|√|√|√
八进制|×|√(带参数)|×
十六进制|√|√|0

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

> **引用类型(类、对象定义)**是一种数据结构，将数据和功能组织在一起  
> **引用类型的值(对象)**是引用类型的实例

创建对象: **new** + 构造函数

### 2.1 Object类型

#### 2.1.1 创建
 
```javascript
var person = new Object();  //new方法
var person = {};  //字面量表示法(推荐)
```

> 使用字面量表示法时，各属性名都会被自动转换为字符串

#### 2.1.2 访问

```javascript
person["name"];  //方括号,可处理变量/有特殊字符的属性
person.name;  //点表示法(推荐)
```

### 2.2 Array类型

> 与其他语言的区别:  
> ①可以保存任何类型数据; ②大小是动态调整的

#### 2.2.1 数组创建

```javascript
var color = new Array();
var color = new Array(3);
var color = new Array("red", "blue", "green");
var color = [];
```

#### 2.2.2 数组读取

```javascript
color[2] = "green";
```

使用方括号，并提供响应值的基于0的索引；当设置的索引超出现有项数，自动增加到该索引值加1的长度

#### 2.2.3 数组长度

`length`属性:  
不是只读的，可以通过设置，从末位移除或添加新项

```javascript
color[color.length] = "red";  //末位添加新项
```

#### 2.2.4 数组判断

方法|适用情况
---|---
value instanceof Array|一个全局作用域/一个网页
Array.isArray(value)|ES5

#### 2.2.5 数组方法

方法|功能|返回
---|---|---
valueOf()|n/a|本身
toString()|n/a|以逗号分隔每一项的字符串
toLocaleString()|n/a|同toString()
join()|n/a|以参数分隔每一项的字符串
push()|末尾加参数|修改后的length
pop()|去末尾，长度减1|移除的项
shift()|去前端，长度减1|移除的项
unshift()|前端加参数|修改后length
reverse()|反转数组|反转后的数组
sort()|有参数:根据比较函数(小于负数, 等于0, 大于正数)参数决定排序；无参数:toString()后字符串排序|排序后的数组
concat()|n/a|当前数组副本，副本末位添加参数后的数组
slice()|n/a|[参数1, 参数2/末位)区间元素构成的数组
splice()|删除【参数一】位置开始的 前【参数二】个项，并添加【其余参数】|被删除掉的项
indexOf()|n/a|从左到右，从【参数二(可选)】索引开始查找的【参数一】所指定的项的位置索引/-1
lastIndexOf()|n/a|从右到左，从【参数二(可选)】索引开始查找的【参数一】所指定的项的位置索引/-1

##### ES5定义的迭代方法:

方法|返回|功能
---|---|---
every()|函数对每一项都返回true->true|对所有项都运行给定函数
some()|对任一项返回true->true|对所有项都运行给定函数
filter()|函数会返回true的项组成的数组|对所有项都运行给定函数
forEach()|n/a|对所有项都运行给定函数
map()|每次调用结果返回的数组|对所有项都运行给定函数


```javascript
var num = [1, 2, 3];
num.every(function(item, index, array)){};
/*item:数组项的值  index:该项在数组的位置  array:数组对象*/
```

##### ES5定义的归并方法:

> 每次函数返回值将作为第一个参数传给下一项  
> ruduce()为从左至右; reduceRight()为从右至左

```javascript
var num = [1, 2, 3];
num.reduce(function(prev, cur, index, array)) {
	return prev + cur;
};
/*prev:前一个值  cur:当前值  index:该项在数组的位置  array:数组对象*/
```

### 2.3 Date类型

> 自UTC1970年1月1日零时开始的毫秒数

#### 2.3.1 创建日期对象

```javascript
var now = new Date();
```

#### 2.3.2 获得UTC毫秒数

```javascript
//将字符串转为毫秒数的方法
//无法表示则为NaN。new Date()时会直接转换
Date.parse("May 25, 2004")
//参数: 年份(必须)、基于0的月份(必须)、月中的天数、小时、分钟、秒、毫秒。new Date()时会以本地时区创建
Date.UTC(2000,0):
```

> 月份表示是基于 0 的月份!

```javascript
Date.Now();  //调用方法时的日期和毫秒数
```

#### 2.3.3 日期方法

方法|返回
---|---
toString()|带有时区信息的日期和时间字符串
toLocaleString()|本地格式的字符串
valueOf()|毫秒数
toDateString()|年、月、日、星期几
toTimeString()|时、分、秒、时区
toLocaleDateString()|本地年、月、日、星期几
toLocaleTimeString()|本地时、分、秒、时区
toUTCString()|完整的UTC日期
……|[其他方法](http://www.w3school.com.cn/jsref/jsref_obj_date.asp)

### 2.4 基本包装类型(Boolean、Number、String)

1. 每当读取一个基本类型时，后台都会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据（只存在于**一行代码**的执行瞬间）:  
①创建Boolean、Number、String类型的一个实例   
②在实例上调用方法  
③销毁实例
2. 基本包装类型的实例调用typeof都会返回"object"，Boolean()都为true

#### 2.4.1 Boolean类型

方法:

方法|返回
---|---
valueOf()|true/false
toString() / toLocaleString()|"true"/"false"

#### 2.4.2 Number类型

方法:

方法|返回
---|---
valueOf()|数值
toString() / toLocaleString()|字符串数值
toFixed()|按参数指定的小数位返回*字符串*(四舍五入)
toExponential()|按参数指定的小数位返回指数字符串
toPrecision()|按参数指定共N位数字的最合适格式

#### 2.4.3 String类型

取字符:

charAt() / 方括号

属性:

方法|说明
---|---
length|总字符数

方法:

方法|返回|备注
---|---|---
charAt()|字符串的第【参数】个字符|
charCodeAt()|字符串的第【参数】个字符的编码|
concat()|原本字符串加每个参数连接组成的新字符串|不如使用`+`操作符
slice()|[【参数1】,【参数2(可选)】)区间的字符串|负值与字符串长度相加
substr()【弃用】|【参数1】开始，长度为【参数二(可选)】的字符串|负的第一个参数加字符串长度，负的第二个参数转为0
substring()|[【参数1】,【参数2(可选)】)区间的字符串|负参转为0
indexOf()|从左到右，从【参数二(可选)】索引开始查找的【参数一】所指定的子字符串的位置索引/-1|
lastIndexOf()|从右到左，从【参数二(可选)】索引开始查找的【参数一】所指定的子字符串的位置索引/-1|
trim()|删掉前置后置空格后的字符串|
toUpperCase()/  toLocaleUpperCase()|大写|
toLowerCase()/  toLocaleLowerCase()|小写|
march()|包含匹配结果的数组|
search()|第一个匹配【参数】的子串开始位置 / -1|
split()|以【参数】分隔后的字符串
localeCompare()|字符串排在【参数】前: -1; 等于: 0; 后: 1|中国以首字母拼音
fromCharCode()|所有参数编码转换后的字符串|


----

### 正则(待看)

p127

## 3. 基本类型与引用类型的区别