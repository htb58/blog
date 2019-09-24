---
title: 字符串借用数组方法
date: 2019-09-24 08:38:37
category: javaScipt
tags: note
---

* javaScript 中的字符串是不可变的，而数组是可变的。

>字符串不可变是指字符串的成员函数不会改变其原始值，而是创建并返回一个新的字符串。而数组的成员函数都是在其原始值上进行操作。

<!--more-->

```javaScript
var  a = "foo";
var  b = ['f','o','o'];
c = a.toUpperCase();
a === c;   // false
a;         //  "foo"
c;         //  "FOO"

b.push( '!' );
b;         // ['f','o','o','!'];
```

* 字符串”借用“数组的非变更方法来处理字符串
```javascript
a.join      // undefined
a.map       // undefined

var  c = Array.prototype.join.call( a, "-" );
var  d = Array.prototype.map.call( a, function(v){
       return  v.toUpperCase() + ".";
}).join( "" );
c;    // "f-o-o"
d;    //  "F.O.O"
```
* 不同点在于字符串反转。数组有一个字符串没有的可变更成员函数 reverse(); 我们无法”借用“数组的可变更成员函数。因为字符串是不可变的。
 >通过一个变通，现将字符串转换为数组，待处理完成后在将结果转换回字符串：
```javascript
var c = a.split( "" ).reverse().join( "" );
c;  // "oof"

```