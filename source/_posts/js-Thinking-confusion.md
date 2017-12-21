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

# 2 正则匹配

## 2.1 search

### 2.1.1 正则与undefined

其他特殊字面量明明都可以正常转成正则对象，但是`undefined`却会转成`/(?:)/`然后进行检测。

```javascript
var a = 4;
var b = 8;
var strString = "hello watermelon";
var oo = new Object();
var oString = new String("hello world");
var oBool = new Boolean(true);
var oNum = new Number(68);
var oArray = new Array("demo","melon","water");
var oDate = new Date();
var oString_1 = 'A \uD87E\uDC04 Z';
var tString_1 =`hello Template`;
var tString_2 =`hello line 1
				hello line 2`;
//`string text ${expression} string text`  在模版字符串中使用表达式
var tString_3 =`Fifteen is ${a + b} and\nnot ${2 * a + b}.`;
console.log(strString.search(undefined));//0
console.log(oString.search(undefined));//0
console.log(oString_1.search(undefined));//0
console.log(tString_1.search(undefined));//0
console.log(tString_2.search(undefined));//0
console.log(tString_3.search(undefined));//0

console.log(oString.search(true));//-1
console.log(oString.search(false));//-1
console.log(oString.search(null));//-1
console.log(oString.search(NaN));//-1

console.log(new RegExp(true));//  /true/

console.log(new RegExp(false));// /false/

console.log(new RegExp(undefined));// /(?:)/

console.log(new RegExp(null));// /null/

console.log(new RegExp(NaN));// /NaN/

```

### 2.1.2 正则与Object

`oo`是一个空对象，它的字面量是`{}`，但是传入`search方法`中确是`[object Object]`。

```javascript
var a = 4;
var b = 8;
var strString = "hello watermelon";
var oo = new Object();
var oString = new String("hello world");
var oBool = new Boolean(true);
var oNum = new Number(68);
var oArray = new Array("demo","melon","water");
var oDate = new Date();
var oString_1 = 'A \uD87E\uDC04 Z';
var tString_1 =`hello Template`;
var tString_2 =`hello line 1
				hello line 2`;
//`string text ${expression} string text`  在模版字符串中使用表达式
var tString_3 =`Fifteen is ${a + b} and\nnot ${2 * a + b}.`;
var tString_4 = "大吉大利今晚吃西瓜!";

console.log(strString.search(oo));//1   位置对应的字母是 e
console.log(strString.charAt(1));//e

console.log(oString.search(oo));//1   位置对应的字母是 e
console.log(oString.charAt(1));//e

console.log(oString_1.search(oo));//1   位置对应的字母是 空格
console.log(oString_1.charAt(1));//\s  位置对应的字母是 空格

console.log(tString_1.search(oo));//1   位置对应的字母是 e
console.log(tString_1.charAt(1));//e

console.log(tString_2.search(oo));//1   位置对应的字母是 e
console.log(tString_2.charAt(1));//e

console.log(tString_3.search(oo));//3   位置对应的字母是 t
console.log(tString_3.charAt(3));//t

console.log(tString_4.search(oo));//-1

console.log(strString.search(oBool));//-1
console.log(strString.search(oNum));//-1
console.log(strString.search(oArray));//-1
console.log(strString.search(oDate));//-1


console.log(new RegExp(oo));//  /[object Object]/

console.log(new RegExp(oString));// /hello world/

console.log(new RegExp(oBool));// /true/

console.log(new RegExp(oNum));// /68/

console.log(new RegExp(oArray));// /demo,melon,water/

console.log(new RegExp(oDate));// /Thu Dec 21 2017 19:39:40 GMT+0800 (中国标准时间)/


```