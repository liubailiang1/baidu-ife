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
march()|包含匹配结果的数组|若不是一个全局检索，a[n]就为&#36;n存放的内容
search()|第一个匹配【参数】的子串开始位置 / -1|不支持全局检索，自动转为RegExp对象
replace()|匹配【参数1】的所有地方替换为【参数2】|不自动转为RegExp对象，可用 &#36; 引用
split()|以【参数】分隔后的字符串|参数可用正则
localeCompare()|字符串排在【参数】前: -1; 等于: 0; 后: 1|中国以首字母拼音
fromCharCode()|所有参数编码转换后的字符串|


### 2.5 正则(RegExp类型)

#### 2.5.1 创建

```javascript
/* pattern: 模式; flags: 标志 */
var expression = / pattern / flags;  //推荐
var expression = new RegExp(pattern, flags);
```

#### 2.5.2 pattern模式

直接量字符:

字符|匹配
---|---
字符和数字字符|自身
\o|NUL字符
\t|制表符
\n|换行符
\v|垂直制表符
\f|换页符
\r|回车符
\xnn|十六进制nn指定的拉丁字符
\uxxxx|十六进制xxxx指定的Unicode字符
\cX|控制字符

字符类:

字符|匹配
---|---
[...]|方框内的任意字符
[^...]|不在方框内的任意字符
.|除换行符和其他Unicode行终止符之外的任意字符
\w|任何ASCII字符组成的单词([a-zA-Z0-9])
\W|任何不适ASCII字符组成的单词([!a-zA-Z0-9])
\s|任何Unicode空白符
\S|任何非Unicode空白符
\d|任何ASCII数字([0-9])
\D|任何ASCII数字之外的字符([^0-9])
[\b]|退格直接量

重复:

字符|含义
---|---
{n,m}|匹配前一项[n, m]次
{n,}|匹配前一项[n, +∞)次
{n}|匹配前一项n次
?|匹配前一项0/1次 ( {0,1} )
+|匹配前一项1/多次 ( {1,} )
*|匹配前一项0/多次 ( {0,} )

> 直接使用重复是贪婪的匹配，匹配得越多越好，且可继续匹配;  
> 非贪婪匹配在待匹配的字符后跟随一个问号即可 尽可能少的匹配(可能匹配不到最少匹配)

选择、分组、引用:

字符|含义
---|---
&#124;|选择
(...)|组合, 将几个项合为一个单元, 而且可以记住和这个组合相匹配的字符串供此后的引用使用
(?:...)|只组合, 将几个项合为一个单元, 不记忆字符
\n|和第n个分组的第一次匹配字符相匹配

字符|含义
---|---
^|匹配开头
$|匹配结尾
\b|匹配一个单词的边界，即\w和\W直接的位置，或\w和字符串开头或者结尾之间的位置（[\b]是退格符）
\B|匹配非单词边界的位置
(?=p)|接下来的字符都与p匹配,但不能包括匹配p的那些字符
(?!p)|接下来的字符不与p匹配

#### 2.5.3 flags标志

字符|含义
---|---
i|执行不区分大小写匹配
g|执行一个全局匹配, 找到所有匹配
m|多行匹配

#### 2.5.4 RegExp属性方法

属性:

属性|说明
---|---
source|只读，正则表达式文本
global/ignoreCase/mulitiline|只读，是否是g/i/m
lastIndex|g标志下, 下次检索的开始位置

方法:

方法|返回
---|---
exec()|数组(总是返回一个匹配结果且提供本次匹配的完整信息, 每次调用都从lastIndex开始)/null
test()|包含匹配结果返回true
valueOf()|本身
toString()/toLocaleString()|字面量字符串

#### 2.5.5 构造函数属性

属性|说明
---|---
&#36;1|第一个引用
&#36;_|最近一次要匹配的字符串
&#36;&|最近一次的匹配项
&#36;+|最近一次的引用
&#36;`|匹配项之前的文本
&#36;'|匹配项之后的文本

### 2.6 单体内置对象

> 由ECMAScript实现提供的、不依赖于宿主环境的对象

#### 2.6.1 Global对象

> 不属于任何其他对象的属性和方法，最终都是它的属性和方法

方法|说明
---|---
isNaN()/isFinite()  /parseInt()/parseFloat()|
encodeURL()|对整个URL编码，不处理冒号、正斜杠、问号、井号
encodeURLComponent()|对URL某一段编码
decodeURL()|对encodeURL()替换的字符解码
decodeURLComponent()|解码
eval()|把【参数】字符串代码进行编译，作用域为调用他的变量作用域; 严格模式下外部不可访问内部定义的变量函数

> 在全局作用域中声明的所有变量函数都成为**window对象**的属性

#### 2.6.2 Math对象

方法:

方法|说明
---|---
min()/max()|最大最小值
ceil()|向上舍入
floor()|向下舍入
round()|四舍五入
random()|[0, 1)的随机数; 值 = Math.floor(Math.random() * 可能值的总数 + 第一个可能的值)

## 3. 基本类型与引用类型的值

### 3.1 区别

区别|基本类型|引用类型
---|---|---
存储方式|简单的数据段|由多个值构成的对象
动态属性|不可填加|可以填加
复制|副本, 不相互影响|引用, 相互影响

> 在传递参数时, 参数都是**按值传递**, 在局部作用域中修改的对象*不会*在全局作用域中反映

### 3.2 检测

基本类型:`typeof`

引用类型:`instanceof`

```javascript
console.log(typeof s);
console.log(person instanceof Object)
```