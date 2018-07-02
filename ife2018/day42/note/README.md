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
缺点: 属性定义不灵活

#### 原型对象

> 让所有对象实例共享它所包含的属性和方法（用于存放希望被原型链下游的对象继承的属性和方法）

![img](https://mdn.mozillademos.org/files/13891/MDN-Graphics-person-person-object-2.png)

![img](https://upload-images.jianshu.io/upload_images/1829401-046fd13950ea5891.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

prototype属性：指向其原型对象。

通过`__proto__`(`[[prototype]]`)查找对象的原型对象

```javascript
//__proto__
person1.__proto__ == Person.prototype;
//isPrototypeOf()
Person.prototype.isPrototypeOf(person1) == true;
//Object.getPrototypeOf()
Object.getPrototypeOf(person1) == Person.prototype;
```