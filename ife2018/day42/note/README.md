# 1 面向对象

## 1.1 创建对象

### 1.1.1 工厂模式

```javascript
function createNewPerson(name) {
    var obj = {};
    obj.name = name;
    obj.greeting = function () {
        alert('Hi! I\'m ' + this.name + '.');
    }
    return obj;
}
var person = createNewPerson("Lee");
```

缺点: 不能识别对象

### 1.1.2 构造函数模式

```javascript
function Person(name) {  //构造函数用大写开头
  this.name = name;
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
  };
}
var person1 = new Person("Lee");  
//若不使用new，this将会指向window
```

使用 `new` 时:

1. 创建新对象;
2. this指向新对象; 
3. 为新对象增加属性
4. 返回新对象

> `constructor`属性: 标识对象类型(指向创建该实例的构造器函数)  
> 但是一般还是使用`instanceof`验证  
> PS: instanceName.constructor.name 构造器的名字

缺点: 每个方法都要在每个实例上重新创建一遍

### 1.1.3 原型模式

```javascript
function Person() {
}
Person.prototype.name = "Lee";  //属性定义不灵活
Person.prototype.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
};
var person1 = new Person();
```

优点: 动态更新  
缺点: 属性定义不灵活/所有实例共享属性

#### 原型对象

> 让所有对象实例共享它所包含的属性和方法（用于存放希望被原型链下游的对象继承的属性和方法）

![img](https://mdn.mozillademos.org/files/13891/MDN-Graphics-person-person-object-2.png)

![img](https://upload-images.jianshu.io/upload_images/1829401-046fd13950ea5891.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

prototype属性：指向其原型对象。

通过`__proto__`(`[[prototype]]`)查找对象的原型对象

```javascript
//__proto__
person1.__proto__ == Person.prototype;
//isPrototypeOf()  原型对象和实例的关系
Person.prototype.isPrototypeOf(person1) == true;
//Object.getPrototypeOf()
Object.getPrototypeOf(person1) == Person.prototype;
```

#### 判断访问的是实例属性还是原型属性

`hasOwnProperty()`方法

```javascript
person1.hasOwnProperty("name");
//true为实例, false为原型
```

#### 重写原型对象的问题

1. 重写了默认的prototype对象，constructor属性变为了新的对象的constructor属性
2. 切断了现有原型与任何之前已经存在的对象实例之间的联系

### 1.1.4 组合使用构造函数模式和原型模式

> 使用最广泛、认同度最高的创建自定义类型的方法

```javascript
function Person(name) {
	this.name = name;
}
Person.prototype.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
};
var person1 = new Person("Lee");
```

## 1.2 继承

### 1.2.1 原型链

> 原型链: 让一个引用类型继承另一个引用类型的属性和方法

```javascript
function SuperType() {
	this.property = true;
}
SuperType.prototype.getSuperType = function() {
	return this.property;
}
function SubType() {
	this.subproperty = false;
}
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function () {
	return this.subproperty;
}
var instance = new SubType();
```

实质: 重写原型对象，代之以一个新类型的实例

#### 注意

1. 上述的property属性将会位于SubType.prototype中, 因为他是一个实例属性; 而getSuperType()原型方法还在SuperType.prototype中
2. instance.constructor == SubType.prototype.constructor == SuperType
3. 所有的函数原型都是Object的实例
4. `instance`和`isPrototypeOf()`可用于判断原型和实例的关系

缺点: 原先的实例类型将会变为原型类型(被共享); 不能向超类型构造函数传递参数

### 1.2.2 借用构造函数

```javascript
function SuperType() {
	this.colors = ["red", "blue"];
}
function SubType() {
	SuperType.call(this);
}
var instance = new SubType();
```

#### `call()`:

调用一个在文件别处定义的函数, 第一个参数是运行该函数的this值

优点: 可以传递参数

### 1.2.3 原型式继承

```javascript
var person = {
	name: "Nicholas",
	friends: ["Van", "Lee"];
}

var anthorPerson = Object.create(person);
anthorPerson.name = "Greg";
```

优点: 不用创建构造函数

### 1.2.4 寄生组合式继承

```javascript
// 定义Person构造器
function Person(firstName) {
  this.firstName = firstName;
}

// 在Person.prototype中加入方法
Person.prototype.walk = function(){
  alert("I am walking!");
};
Person.prototype.sayHello = function(){
  alert("Hello, I'm " + this.firstName);
};

// 定义Student构造器
function Student(firstName, subject) {
  // 调用父类构造器, 确保(使用Function#call)"this" 在调用过程中设置正确
  Person.call(this, firstName);

  // 初始化Student类特有属性
  this.subject = subject;
};

// 建立一个由Person.prototype继承而来的Student.prototype对象.
// 注意: 常见的错误是使用 "new Person()"来建立Student.prototype.
// 这样做的错误之处有很多, 最重要的一点是我们在实例化时
// 不能赋予Person类任何的FirstName参数
// 调用Person的正确位置如下，我们从Student中来调用它
Student.prototype = Object.create(Person.prototype); // See note below

// 设置"constructor" 属性指向Student
Student.prototype.constructor = Student;

// 更换"sayHello" 方法
Student.prototype.sayHello = function(){
  console.log("Hello, I'm " + this.firstName + ". I'm studying " + this.subject + ".");
};

// 加入"sayGoodBye" 方法
Student.prototype.sayGoodBye = function(){
  console.log("Goodbye!");
};

```