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
