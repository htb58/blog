---
title: javascript 实现点击复制文本
date: 
category: javaScipt
tags: note
---
* javascript 实现点击复制文本

<!--more-->
```javascript
function copyToClipboard( txt ){
  var s = "txt";
    if(window.clipboardData){
      window.clipboardData.setData('text',s);
    }else{
      document.oncopy=function(e){
          e.clipboardData.setData('text',s);
          e.preventDefault();
          document.oncopy=null;
      }
      document.execCommand('Copy');
    }
}
copyToClipboard('复制')
```