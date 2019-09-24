---
title: 诗
date: 2019-09-24 08:38:37
tags: note
toc: true
---

[**丑奴儿·书博山道中壁**](https://so.gushiwen.org/shiwenv_2ee36eb2ccf7.aspx)

[宋代](https://so.gushiwen.org/shiwen/default.aspx?cstr=%e5%ae%8b%e4%bb%a3)：[辛弃疾](https://so.gushiwen.org/authorv_a7900666497f.aspx)

少年不识愁滋味，爱上层楼。爱上层楼，为赋新词强说愁。
而今识尽愁滋味，欲说还休。欲说还休，却道天凉好个秋。
<!--more-->

阿里图表插件    ：[dataV](http://datav.jiaminghi.com/guide/percentPond.html#%E5%AE%9A%E5%88%B6%E5%9D%97%E9%9A%99%E9%95%BF%E5%BA%A6)

```javascript
function getMonthLength(date) {
  let d = new Date(date)
  // 将日期设置为下月一号
  d.setMonth(d.getMonth()+1)
  d.setDate('1')
  // 获取本月最后一天
  d.setDate(d.getDate()-1)
  return d.getDate()
}
```