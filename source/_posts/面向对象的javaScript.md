---
title: 面向对象的javaScript
date: 2019-09-24 08:38:37
category: javaScipt
tags: note
---
#### 1.1 动态类型语言和鸭子类型
* 编程语言按照数据类型大体可以分为两类：静态类型语言、动态类型语言。
> javascript在对变量赋值时。不需要考虑它的类型。因此，javascript是一门典型的动态类型语言。动态类型语言由于无需进行类型检测，我们可以尝试调用任何对象的任意方法，而无需考虑它原本是否被设计为拥有该方法。
这一切都建立在 **鸭子类型** 的概念上，鸭子类型的通俗说法是：”如果它走起路来像鸭子，叫起来也像鸭子、那么他就是鸭子。“
<!--more-->

eg:
```
var duck = {
  duckSinging: function(){
    console.log("嘎嘎嘎")
  }
};
var chicken = {
  duckSinging: function(){
    console.log("嘎嘎嘎")
  }
}
var choir = []; // 合唱团
var joinChoir = function ( animal ){
  if( animal && typeof animal.duckSinging === 'function' ){
    choir.push( animal );
    console.log( '恭喜加入合唱团' )
  }
};
joinChoir( duck );
joinChoir( chicken );
```
只要存在这个方法，那么就可以加入到这个集合中，并不需要检测他们的类型
#### 1.2 多态
> 含义： 同一操作作用于不同德对象上面，可以产生不同的解释和不同的执行结果。换句话说，给不同的对象发送同一消息的时候，这些对象会根据这个消息分别出不同的反馈。