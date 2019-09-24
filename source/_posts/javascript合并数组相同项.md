---
title: javaScript 合并数组相同项
date: 2019-09-24 08:38:37
category: javaScipt
tags: note
---
* 用于合并当数组值是Object时处理数据

<!--more-->
```javaScript
var arr = [
    {sex: '男', age: 18 },
    {sex: '男', age: 20 },
    {sex: '女', age: 18 },
    {sex: '男', age: 18 },
    {sex: '女', age: 16 },
    {sex: '男', age: 25 }
   ];
   var  has={},res=[];
   for(var i = 0,len = arr.length;i<len;i++){
      var item = arr[i];
      if(!has[item.sex]){
         res.push({
            sex: item.sex,
            list: [item]
        });
        has[item.sex] = item;
      }else {
        for(var j = 0;j<res.length;j++){
          var sex = res[j];
          if(item.sex == sex.sex){
             sex.list.push(item);
             break;
           }
         }
      }
   }
```
```javaScript
console.log(res) // 最后的结果
```