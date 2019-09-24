---
title: vue路由的两种模式，hash与history原理
date: 2019-09-24 08:38:37
category: vue
tags: note
---

>1. hash —— 即地址栏 URL 中的 # 符号（此 hash 不是密码学里的散列运算）。
比如这个 URL：http://www.abc.com/#/hello，hash 的值为 #/hello。它的特点在于：hash 虽然出现在 URL 中，但不会被包括在 HTTP 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面。
<!--more-->
>2. history —— 利用了 HTML5 History Interface 中新增的 pushState() 和 replaceState() 方法。（需要特定浏览器支持）
这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。
因此可以说，hash 模式和 history 模式都属于浏览器自身的特性，Vue-Router 只是利用了这两个特性（通过调用浏览器提供的接口）来实现前端路由。
### 错误
 >1、hash模式下，仅hash符号之前的内容会被包含在请求中，如 http://www.abc.com, 因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回404错误；

>2、history模式下，前端的url必须和实际向后端发起请求的url 一致，如http://www.abc.com/book/id 。如果后端缺少对/book/id 的路由处理，将返回404错误。刷新也会报404因为会实际去请求数据。 （需要后端进行配置。vue官网有介绍）

>前端路由中我们主要是利用history.replaceState() history.pushState或者改变hash值不会使页面重新加载，然后监听路由的变化来做到触发对应时间加载对应资源来重新绘制页面。
这里比较重要的点是，监听hash模式用的是hashchange，history模式用的是popstate
