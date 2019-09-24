---
title: Object.create 详解
date: 2019-09-24 08:38:37
category: javaScipt
tags: note
---
> Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的 \_\_proto\_\_ 。
<!--more-->
```
const person = {
  isHuman: false,
  printIntroduction: function () {
    console.log(` 我的名字是 ${this.name}.我是人类吗? ${this.isHuman}`);
  }
};
var me = Object.create( person );
me.name = '周树人';      // 'name' 是设置在me上面的属性，而非 person；
me.isHuman = true;      // 继承的属性可以被覆盖。
me.printIntroduction(); //  我的名字是周树人.我是人类吗 ? true

```
### 语法
> Object.create(proto[, propertiesObject])

#### 参数

##### proto
 * 新创建对象的原型对象。
##### propertiesObject  ({})
 * 可选。如果没有指定为 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined "undefined是全局对象的一个属性。也就是说，它是全局作用域的一个变量。undefined的最初值就是原始数据类型undefined。")，则是要添加到新创建对象的可枚举属性（即其自身定义的属性，而不是其原型链上的枚举属性）对象的属性描述符以及相应的属性名称。这些属性对应[`Object.defineProperties()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties "Object.defineProperties() 方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。")的第二个参数。
#### 返回值
* 一个新对象，带着指定的原型对象和属性。
#### 兼容写法
```
Object.create = Object.create || function ( proto ){
  if (typeof proto !== 'object' && typeof proto !== 'function') {
    throw new TypeError('Object prototype may only be an Object: ' + proto);
   } else if (proto === null) {
    throw new Error("This browser's implementation of Object.create is a shim and doesn't support 'null' as the first argument.");
  }
  function F () {}
  F.prototype = proto;

  return new F();
}
```