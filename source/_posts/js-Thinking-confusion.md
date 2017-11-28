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
//默认String和Date没什么关系
var oDate = new Date();
console.log(oDate instanceof String);//false
console.log(String instanceof Date);//false
console.log(Date instanceof String);//false

//----------------------------------------但是请注意
console.log(String().constructor);//[Function: String]
console.log(Date().constructor);//[Function: String]
console.log(String().constructor===Date().constructor);//true
console.log(String().__proto__);//[String: '']
console.log(Date().__proto__);//[String: '']
console.log(String().__proto__===Date().__proto__);//true

//----------------------------------------举个实际的例子
var oArr = new Array(68);
var noArr = Number(oArr);
var doArr = Date(oArr);
console.log(doArr.constructor);//[Function: String]  为何啊
console.log(doArr.__proto__); //[String: '']  为何啊  明明这两个数据类型没什么关联

//其他类型强转之后，实例的构造体都是正常修改为强转的对象类名
console.log(noArr.constructor);//[Function:Number]
console.log(noArr.__proto__); //[Number: 0]
```