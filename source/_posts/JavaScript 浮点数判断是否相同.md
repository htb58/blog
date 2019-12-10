---
title: JavaScript 浮点数判断是否相同
date: 
category: javaScipt
tags: note
---

在JavaScript中处理二进制浮点数最大的问题会出现如下情况：
```javaScript
 0.1 + 0.2 === 0.3;  // false
```
<!--more-->
>在数学角度 上面的判断应该为true，可结果为什么为false？
二进制浮点数中0.1和0.2并不是十分精确，它们相加等于一个比较接近的数字 0.30000000000000004 ，所以结果为false。

* 我最常见的处理 0.1 + 0.2 和  0.3 是否相等的方法就是去设置一个误差范围值，通常称为 **”机器精度“**，对javaScript数字来说，这个值通常是 2.220446049250313e-16 。
>从es6开始，该值定义在Number.EPSILON中。
```javascript
if( !Number.EPSILON ){
  Number.EPSILON = Math.pow( 2, -52 );
}
function numbersEqual ( n1, n2 ) {
  return Math.abs( n1 - n2 ) < Number.EPSILON;
}
var a = 0.1 + 0.2;
var b = 0.3
numbersEqual( a, b );  // true 
numbersEqual( 0.000001, 0.000002 );  // false
```
- Number.MAX_VALUE  // js 中最大的数    **1.7976931348623157e+308**
- Number.MIN_VALUE  // js 中最小的数 (无限接近于0的非负数)  **5e-324**
