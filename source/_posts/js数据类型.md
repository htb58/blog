---
title: 精确判断 js 数据类型
date: 2019-09-24 08:38:37
category: javaScipt
tags: note
---
> 每个对象都有一个 toString() 方法，当该对象被表示为一个文本值时，或者一个对象以预期的字符串方式引用时自动调用。默认情况下，toString() 方法被每个 Object 对象继承。如果此方法在自定义对象中未被覆盖，toString() 返回 "[object type]"，其中 type 是对象的类型。

<!--more-->

```javascript
Object.prototype.toString.call('123')       //"[object String]"
Object.prototype.toString.call(123)         //"[object Number]"
Object.prototype.toString.call(true)        //"[object Boolean]"
Object.prototype.toString.call(undefined)   //"[object undefined]"
Object.prototype.toString.call(null)        //"[object Null]"

Object.prototype.toString.call([1,2,3])     //"[object Array]"
Object.prototype.toString.call(()=>{})      //"[object Function]"
Object.prototype.toString.call({a})         //"[object Object]"
````