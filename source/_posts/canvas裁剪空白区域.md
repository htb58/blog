---
title: canvas裁剪空白区域
date: 
category: javaScipt
tags: note
---

* 手绘签字裁剪canvas空白区域

<!--more-->
```javascript
cropSignatureCanvas: function(canvas) {
  // 复制画布 避免影响之前的画布
  var croppedCanvas = document.createElement('canvas'),
      croppedCtx    = croppedCanvas.getContext('2d');

      croppedCanvas.width  = canvas.width;
      croppedCanvas.height = canvas.height;
      croppedCtx.drawImage(canvas, 0, 0);

  // 处理画布空白
  var w         = croppedCanvas.width,
      h         = croppedCanvas.height,
      pix       = {x:[], y:[]},
      imageData = croppedCtx.getImageData(0,0,croppedCanvas.width,croppedCanvas.height), // 获取canvas像素数据
      x, y, index;
  for (y = 0; y < h; y++) {
      for (x = 0; x < w; x++) {
          index = (y * w + x) * 4 + 3;  //根据行、列读取某像素点的R/G/B/A值的公式：
          if (imageData.data[index] > 0) {
              pix.x.push(x);
              pix.y.push(y);
          }
      }
  }
      
  pix.x.sort(function(a,b){return a-b});
  pix.y.sort(function(a,b){return a-b});
  var n = pix.x.length-1;

  w = pix.x[n] - pix.x[0];
  h = pix.y[n] - pix.y[0];
  var cut = croppedCtx.getImageData(pix.x[0], pix.y[0], w, h);

  croppedCanvas.width = w;
  croppedCanvas.height = h;
  croppedCtx.putImageData(cut, 0, 0);

  return croppedCanvas.toDataURL("image/png");
}
```
[imageData 详解](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Pixel_manipulation_with_canvas)