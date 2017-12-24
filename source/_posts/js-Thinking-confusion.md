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
//原意
//(?:pattern) 匹配`pattern`但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。
//因为上面的pattern值为空，所以上面正则的意思是匹配所有

console.log(new RegExp(null));// /null/

console.log(new RegExp(NaN));// /NaN/

```

### 2.1.2 正则与Object

`oo`是一个空对象，它的字面量是`{}`，但是传入`search方法`中却是`[object Object]`。

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
//中括号的意思是    匹配中括号的任意一个字符
// 所以对应正则的意思是只要字符串中存在object这几个字母和空格都会被匹配

console.log(new RegExp(oString));// /hello world/

console.log(new RegExp(oBool));// /true/

console.log(new RegExp(oNum));// /68/

console.log(new RegExp(oArray));// /demo,melon,water/

console.log(new RegExp(oDate));// /Thu Dec 21 2017 19:39:40 GMT+0800 (中国标准时间)/


```

# 3 localeCompare

## 3.1 localeCompare与正则参数

就目前测试的相关数据结果表现，不管字符串中是什么内容，传入什么样的正则值，或者传入`制表符`，`空格`，和`换行符`等等`特殊字符`，`localeCompare`都会返回正值。

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
var tString_4 = "大吉大利今晚吃西瓜!"
console.log("-------------------测试/\s/");

console.log(strString.localeCompare(/\s/));//1
console.log(oString.localeCompare(/\s/));//1
console.log(oString_1.localeCompare(/\s/));//1
console.log(tString_1.localeCompare(/\s/));//1
console.log(tString_2.localeCompare(/\s/));//1
console.log(tString_3.localeCompare(/\s/));//1
console.log(tString_4.localeCompare(/\s/));//1

console.log("-------------------测试/\o/");

console.log(strString.localeCompare(/\o/));//1
console.log(oString.localeCompare(/\o/));//1
console.log(oString_1.localeCompare(/\o/));//1
console.log(tString_1.localeCompare(/\o/));//1
console.log(tString_2.localeCompare(/\o/));//1
console.log(tString_3.localeCompare(/\o/));//1
console.log(tString_4.localeCompare(/\o/));//1

console.log("-------------------测试/\n/");

console.log(strString.localeCompare(/\n/));//1
console.log(oString.localeCompare(/\n/));//1
console.log(oString_1.localeCompare(/\n/));//1
console.log(tString_1.localeCompare(/\n/));//1
console.log(tString_2.localeCompare(/\n/));//1
console.log(tString_3.localeCompare(/\n/));//1
console.log(tString_4.localeCompare(/\n/));//1
console.log(tString_4.localeCompare(/\o/));//1

console.log("-------------------测试/helllo world/");

console.log(strString.localeCompare(/helllo world/));//1
console.log(oString.localeCompare(/helllo world/));//1
console.log(oString_1.localeCompare(/helllo world/));//1
console.log(tString_1.localeCompare(/helllo world/));//1
console.log(tString_2.localeCompare(/helllo world/));//1
console.log(tString_3.localeCompare(/helllo world/));//1
console.log(tString_4.localeCompare(/helllo world/));//1
console.log(tString_4.localeCompare(/helllo world/));//1

console.log("-------------------测试/大吉大利/");
console.log(/大吉大利/);
console.log(strString.localeCompare(/大吉大利/ig));//1
console.log(oString.localeCompare(/大吉大利/ig));//1
console.log(oString_1.localeCompare(/大吉大利/ig));//1
console.log(tString_1.localeCompare(/大吉大利/ig));//1
console.log(tString_2.localeCompare(/大吉大利/ig));//1
console.log(tString_3.localeCompare(/大吉大利/ig));//1
console.log(tString_4.localeCompare(/大吉大利/ig));//1

console.log(tString_2);//hello line 1\n\t\t\t\thello line 2
console.log(tString_2.localeCompare("  "));//1
console.log(tString_2.localeCompare("    "));//1
console.log(tString_2.localeCompare("     "));//1
console.log(tString_2.localeCompare("	"));//1
console.log(tString_2.localeCompare("		"));//1

```

## 3.2 localeCompare判断

目前看来不管传入的`子字符串`和`原始字符串`是否存在包含关系，结果都不一定是`正值`,在测试数据结果中不发现是单纯的通过两个字符串首字母进行对比。

### 3.2.1 两个字符串的首字母相同

首字母相同，但是得到的结果却不一定是正值，会根据子字符串的长度还有包含的字母不同，返回不同的值，但是这个具体处理逻辑我不太懂。

```javascript
console.log(strString);//hello watermelon
console.log(strString.localeCompare("h"));//1
console.log(strString.localeCompare("H"));//1
console.log(strString.localeCompare("hello watermelon1"));//-1   修改了原有字符串的长度，返回 -1  这个我可以理解

//不是递归对比每一个字母在字母表中的位置，返回总的对比结果吗，
//还是递归对比每一个字母在ACSII码表中的值进行排序对比，返回总的对比结果
// a 不是比原有的 l在字母表中的位置高很多吗？
// z 不是比原有的 l在字母表中的位置低很多吗？
// 而且我子字符串长度的值比原始字符串长度还要多一位，为何还是会存在返回正值的情况
console.log(strString.localeCompare("healo watermelon1"));//1   修改了原有字符串的一个字母为 a 作为子字符串，返回 1
console.log(strString.localeCompare("hezlo watermelon1"));//-1   修改了原有字符串的一个字母为 z 作为子字符串，返回 -1，

console.log(oString_1);//A 你 Z
console.log(oString_1.localeCompare("a"));//1
console.log(oString_1.localeCompare("A"));//1
console.log(oString_1.localeCompare("A 你 Z。"));//-1

console.log(tString_3);//Fifteen is 12 and\nnot 16.
console.log(tString_3.localeCompare("fifteen"));//1
console.log(tString_3.localeCompare("Fifteen"));//1
console.log(tString_3.localeCompare("Fifteen is 12 and\nnot 16.。"));//1

console.log(tString_3.localeCompare("Fiftaen"));//1 修改了原有字符串的一个字母为 a 作为子字符串，返回 1
console.log(tString_3.localeCompare("Fiftzen"));//-1 修改了原有字符串的一个字母为 z 作为子字符串，返回 -1

console.log("-------------------测试num");
console.log(oString.localeCompare(1));//1
console.log(oString.localeCompare(1.1));//1
console.log(oString.localeCompare(1.5));//1
console.log(oString.localeCompare(1.8));//1
console.log(oString.localeCompare(-1));//1

```

### 3.2.2 原始字符串包含子字符串

传入的`子字符串`是完全被包含于`原始字符串`的，但是结果不一定都是返回`正值`，子字符串长度不是一个参考值？

```javascript
console.log(strString);//hello watermelon
console.log(strString.localeCompare("h"));//1
console.log(strString.localeCompare("llo"));//-1

console.log(oString_1);//A 你 Z
console.log(oString_1.localeCompare("A"));//1
console.log(oString_1.localeCompare("\uD87E\uDC04"));//-1
console.log(oString_1.localeCompare("你"));//-1
console.log(oString_1.normalize().localeCompare("你"));//-1
console.log(oString_1.localeCompare("你"));//-1

console.log(tString_2);//hello line 1\n\t\t\t\thello line 2
console.log(tString_2.localeCompare("line"));//-1

console.log(tString_3);//Fifteen is 12 and\nnot 16.
console.log(tString_3.localeCompare("Fifteen"));//1

console.log(tString_4);//大吉大利今晚吃西瓜!
console.log(tString_4.localeCompare("吃西瓜"));//1
console.log(tString_4.localeCompare("大吉大利今晚吃西瓜"));//1
console.log(tString_4.localeCompare("大吉大利今晚吃西瓜 "));//1
console.log(tString_4.localeCompare("大吉大利今晚吃西瓜."));//-1

```

### 3.2.3 localeCompare与特殊值

```javascript
console.log("-------------------测试undefined");
//除了undefined本身，所有字符串与undefined做对比，都返回了-1 ，undefined不应该是一个比较小的值吗
console.log("true".localeCompare(undefined));//-1
console.log("false".localeCompare(undefined));//-1
console.log("null".localeCompare(undefined));//-1
console.log("undefined".localeCompare(undefined));//0
console.log("NaN".localeCompare(undefined));//-1
console.log(strString.localeCompare(undefined));//-1
console.log(oString.localeCompare(undefined));//-1
console.log(oString_1.localeCompare(undefined));//-1
console.log(tString_1.localeCompare(undefined));//-1
console.log(tString_2.localeCompare(undefined));//-1
console.log(tString_3.localeCompare(undefined));//-1
console.log(tString_4.localeCompare(undefined));//-1

console.log("-------------------测试true");
//除了true本身和完全是中文字符构成的字符串，所有字符串与true做对比，都返回了-1 ，这又是为何？
console.log(strString.localeCompare(true));//-1
console.log(oString.localeCompare(true));//-1
console.log(oString_1.localeCompare(true));//-1
console.log(tString_1.localeCompare(true));//-1
console.log(tString_2.localeCompare(true));//-1
console.log(tString_3.localeCompare(true));//-1
console.log(tString_4.localeCompare(true));//1

console.log("-------------------测试false");

console.log(strString.localeCompare(false));//1
console.log(oString.localeCompare(false));//1
console.log(oString_1.localeCompare(false));//-1   不懂为何结果是  -1
console.log(tString_1.localeCompare(false));//1
console.log(tString_2.localeCompare(false));//1
console.log(tString_3.localeCompare(false));//1
console.log(tString_4.localeCompare(false));//1

console.log("-------------------测试null");
//除了null本身和完全是中文字符构成的字符串，所有字符串与null做对比，都返回了-1 ，null不应该是一个比较小的值吗
console.log(strString.localeCompare(null));//-1
console.log(oString.localeCompare(null));//-1
console.log(oString_1.localeCompare(null));//-1
console.log(tString_1.localeCompare(null));//-1
console.log(tString_2.localeCompare(null));//-1
console.log(tString_3.localeCompare(null));//-1
console.log(tString_4.localeCompare(null));//1

console.log("-------------------测试NaN");
//除了NaN本身和完全是中文字符构成的字符串，所有字符串与NaN做对比，都返回了-1 ，NaN不应该是一个比较小的值吗
console.log(strString.localeCompare(NaN));//-1
console.log(oString.localeCompare(NaN));//-1
console.log(oString_1.localeCompare(NaN));//-1
console.log(tString_1.localeCompare(NaN));//-1
console.log(tString_2.localeCompare(NaN));//-1
console.log(tString_3.localeCompare(NaN));//-1
console.log(tString_4.localeCompare(NaN));//1

console.log("-------------------测试oo");

console.log(strString.localeCompare(oo));//1
console.log(oString.localeCompare(oo));//1
console.log(oString_1.localeCompare(oo));//1
console.log(tString_1.localeCompare(oo));//1
console.log(tString_2.localeCompare(oo));//1
console.log(tString_3.localeCompare(oo));//1
console.log(tString_4.localeCompare(oo));//1
```