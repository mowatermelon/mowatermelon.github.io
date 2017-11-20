---
title: 西瓜有话说之js学习funciton篇
category: js_thinking
tags:
  - funciton
  - watermelon
  - js_thinking
date: 2017-10-10 00:00:00
---
# 1. 定义

构造函数，创建一个新的`function`对象。 在 javascript 中, 每个函数实际上都是一个`function`对象。

<!-- more -->

# 2 名词字典

> 本文中出现变量名词的解释

```javascript
    var oo = new Object();
    var oBool = new Boolean(true);
    var oNum = new Number(68);
    var oString = new String("hello world");
    var oArray = new Array("demo","melon","water");
    var oDate = new Date();

    function demoParent(){

    }

    function demoChildren(){

    }
```

|变量名|含义|举例|
|:---|:---|:---|
|objectName| 相关对象类型名称 |就像上面`js`代码中`Object`,`Boolean`,`Number`,`String`,`Array`,`Date`|
|varName| 相关对象类型实例化后的变量名 |就像上面`js`代码中`oo`,`oBool`,`oNum`,`oString`,`oArray`,`oDate`|
|param1,param2,param3,...,paramN|函数中需要传入第一个到第N个的参数值 |就像上面`js`代码中`true`,`68`,`hello world`|
|functionName|函数名称|就像上文的`demoParent`，`demoChildren`|

# 3. function的属性

## 3.1 继承对象的属性

## 3.2  函数的常用属性值

|属性名|描述|使用方法|
|:---|:---|:---|
|arguments| `不推荐使用`，属性代表传入函数的实参，它是一个类数组对象。已经被废弃很多年了，现在推荐的做法是使用函数内部可用的 `arguments` 对象来访问函数的实参。在函数递归调用的时候（在某一刻同一个函数运行了多次，也就是有多套实参），那么 `arguments` 属性的值是最近一次该函数调用时传入的实参。如果函数不在执行期间，那么该函数的 `arguments` 属性的值是 `null`。|functionName.arguments|
|arity|`已废弃`，返回一个函数的形参数量，是一个古老的已经没有浏览器支持的属性,你应该使用`length`属性来代替.。|functionName.arity|
|caller| `不推荐使用`，如果一个函数`functionName`是在`全局作用域`内被调用的,则`functionName.caller`为`null`,相反,如果一个函数是在另外一个函数作用域内被调用的,则`functionName.caller`指向调用它的`那个函数`，该属性的常用形式`arguments.callee.caller`替代了被废弃的`arguments.caller`。|functionName.caller|
|callee| `不推荐使用`，callee放回正在执行的函数本身的引用，它是`arguments`的一个属性。|arguments.callee|
|displayName| `不推荐使用`，获取函数的显示名称。|functionName.displayName|
|length|指明函数的形参个数，length 是函数对象的一个属性值，指该函数有多少个必须要传入的参数，即形参的个数。形参的数量不包括剩余参数个数，仅包括第一个具有默认值之前的参数个数。与之对比的是，arguments.length 是函数被调用时实际传参的个数。|functionName.length|
|name|返回一个函数声明的名称，使用`new Function(...)`语法创建的函数或只是 `Function(...)` create Function对象及其名称为`anonymous`。|functionName.name|
|prototype|函数对象具有属性`__proto__`，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型。|functionName.prototype|

## 3.3  注意

### 3.3.1 callee

- 这个属性只有在函数执行时才有效
- 它有一个length属性，可以用来获得形参的个数，因此可以用来比较形参和实参个数是否一致，即比较arguments.length是否等于arguments.callee.length
- 它可以用来递归匿名函数。

```javascript
  var a = function() {
      console.log("arguments.callee"); //  arguments.callee
      console.log(arguments.callee);
      //在浏览器控制台 打印效果
      // ƒ () {
      // console.log("arguments.callee");
      // console.log(arguments.callee);
      // console.log("arguments.callee.length");
      // console.log(arguments.callee.length);
      // }

      //在js文件以node的形式运行  打印效果
      //[Function: a]

      console.log("arguments.callee.length------a"); //arguments.callee.length
      console.log(arguments.callee.length);   // 0
  }
  var b = function(n,m) {
      a();
      console.log("arguments.callee.length------b"); //arguments.callee.length
      console.log(arguments.callee.length);   // 2
  }
  b();
```

### 3.3.2 length

- 请注意这个指的是形参的个数，如果参数在传入的时候是以已经定义的情况下，这个时候是不会被计算的

```javascript
    console.log(Function.length); /* 1 */

    console.log((function()        {}).length); /* 0 */
    console.log((function(a)       {}).length); /* 1 */
    console.log((function(a, b)    {}).length); /* 2 etc. */

    console.log((function(...args) {}).length);
    // 0, rest parameter is not counted


    console.log((function(a, b = 1, c) {}).length);
    // 1, only parameters before the first one with
    // a default value is counted

    console.log((function(a = 1, b, c) {}).length) // 0
    console.log((function(b, a = 1, c) {}).length) // 1
    console.log((function(b, c, a = 1) {}).length) // 2
```

# 4. function的方法

## 4.1 继承对象的方法

## 4.2 函数的常用方法
