---
title: 西瓜有话说之js学习疑惑篇
category: js_thinking
tags:
  - confusion
  - watermelon
  - js_thinking
date: 2017-10-23 00:00:00
---
# 1 js类型强制转化

## 1.1 Date强转

为何Date强转之后构造体成了String？

<!-- more -->

```javascript
var oDate = new Date();
console.log(oDate instanceof String);//false
console.log(String instanceof Date);//false

var oNum = new Number(68);
var aoNum = Array(oNum);
var doNum = Date(oNum);
console.log(doNum.constructor);//[Function: String]  为何啊
console.log(doNum.__proto__); //[String: '']  为何啊  明明这两个数据类型没什么关联

//其他类型强转之后，实例的构造体都是正常修改为强转的对象类名
console.log(aoNum.constructor);//[Function:Array]
console.log(aoNum.__proto__); //[]
```