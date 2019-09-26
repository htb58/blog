---
title: this、call 和 apply
date: 2019-09-24 08:38:37
category: vue
tags: js
---

# this

> javascript的this总是指向一个对象，而具体指向那个对象是在运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境。

## this 的指向

* 除去不常用的with 和 eval 的情况，this 指向大致分为四种。

1. 作为对象的方法调用
2. 作为普通函数调用
3. 构造器调用
4. Function.prototype.call或 Function.prototype.apply调用。

### **作为对象的方法调用**

* 当函数作为对象的方法时，this 指向该对象

<!--more-->
```javascript
var obj = {
  a: 1,
  getA: function(){
    console.log( this == obj ) // true
    console.log( this.a )      // 1
  }
};
obj.getA();
```
### **作为普通函数调用**

* 当函数不作为对象的属性被调用时，也就是普通函数的方式，此时的this总是指向全局对象（window）；

```javaScript
window.name = 'globalName';
var getName = function () {
  return this.name;
}
console.log(getName()) // globalName

var obj = {
  name: 'objName',
  getName: function(){
    return this.name;
  }
};
var getName = obj.getName;
console.log(getName()) // globalName
```

### **构造器调用**

* JavaScript 中可以从构造器中创建对象。同时提供了new运算符。
* 除了宿主(由ECMAScript实现的宿主环境提供的对象，可以理解为：浏览器提供的对象。所有的BOM和DOM都是宿主对象。)提供的一些内置函数，大部分JavaScript函数都可以当做构造器使用。

- 通常情况，构造器里的this 就指向返回的这个对象。-
```javaScript
var myClass = funtion(){
  this.name = 'class'
}
var obj = new myClass();
console.log(obj.name) // class
```
- 但如果构造器显式的返回了一个object类型的对象，那么运算结果最终会返回这个对象，this 也将指向这个对象。

```javaScript
var myClass = funtion(){
  this.name = 'class';
  return {
    name: 'name'
  }
}
var obj = new myClass();
console.log(obj.name) // name
```
- 但如果构造器不显式的返回了任何数据，或者返回一个非object类型的对象，就不会出现上述问题。

```javaScript
var myClass = funtion(){
  this.name = 'class';

  return 'name';
};
var obj = new myClass();
console.log(obj.name) // class
```

### Function.prototype.call或 Function.prototype.apply调用。

* 跟普通的函数调用相比，用 call 或 apply 可以动态的改变传入函数的this

```javascript
var obj1 = {
  name: 'obj1',
  getName: function(){
    return this.name;
  }
};
var obj2 = {
  name: 'obj2'
}
console.log( obj1.getName() ); // obj1
console.log( obj1.getName.call(obj2)) // obj2
```

# call 和 apply

> ECAMScript 3 给 Function 的原型定义了两个方法，它们是 Function.prototype.call 和 Function.prototype.apply。

# call 和 apply 的区别

> Function.prototype.call 和 Function.prototype.apply 它们的作用是一摸一样的，区别仅在于传入的参数形式的不同。

## apply 
> apply 接受两个参数，第一个参数指定了函数体内this 对象的指向，第二个参数为一个带下标的集合，这个集合可以为数组，也可以为类数组,apply方法把这个集合中的元素作为参数传递给被调用的函数：

```javascript
var func = function( a, b, c ){
  console.log( [a, b, c] ); // [1, 2, 3]
};
func.apply( null , [1, 2, 3])
```

## call 
> call 传入的参数的数量不固定，跟apply相同的是，第一个参数也是代表函数体内的this的指向，从第二个参数开始往后，每个参数依次传入函数：

```javascript
var func = function( a, b, c ){
  console.log( [a, b, c] ); // [1, 2, 3]
};
func.call( null , 1, 2, 3)
```

> 当使用call 或者 apply 的时候，如果我们传入的第一个参数为null，函数体内的 this 会指向默认的宿主对象，在浏览器中则是window。

```javaScript

var func = function( a, b, c ){
  console.log( this == window ); // true
};
func.call( null , 1, 2, 3)

```

>但如果在严格模式下，函数体内的 this 还是null。

```javaScript

  var func = function( a, b, c ){
    "use strict"
    console.log( this == null ); // true
  };
  func.call( null , 1, 2, 3)
```

# call 和 apply 的用途

### 改变this的指向

```javaScript
  var obj1 = {
    name: 'obj1'
  };
  var obj2 = {
    name: 'obj2'
  };
  window.name = 'window'

  var getName = function() {
    console.log(this.name)
  }

  getName();  // window
  getName.call(obj1) // obj1
  getName.call(obj2) // obj2

```

### Function.prototype.bind
 
* 模拟Function.prototype.bind 实现

```javascript
Function.prototype.bind = function( context ){
  var self = this;
  return function(){
    return self.apply(context,arguments)
  }
}
var obj = {
  name: 'obj'
}
var func = function(){
  console.log(this.name)
}.bind( obj );
func();
```
### 借用其他对象的方法