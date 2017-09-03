---
title: js学习之js数据类型
category: js学习
tags:
  - 数据类型
  - js学习
date: 2017-05-04 00:00:00
---


> 前不久我了解了js数组相关操作，才发现我的js在`数据类型`这块的基础真的很薄弱，所以整理了些文档，重新学习了一下。

- ### 1 DEFINTION   
`数据类型`在`数据结构`中的定义是一个`值`的`集合`以及定义在这个`值集`上的一组`操作`。  
`变量`是用来`存储值`的`所在处`，它们有`名字`和``数据类型``。`变量`的`数据类型`决定了如何将代表这些`值`的`位存储`到计算机的`内存`中。在声明`变量`时也可指定它的`数据类型`。所有变量都具有`数据类型`，以决定能够存储`哪种数据`。  
`数据类型`包括`原始类型`、`多元组`、`记录单元`、`代数数据类型`、`抽象数据类型`、`参考类型`以及`函数类型`。
<!-- more -->
- ### 2 PARAMETER
在`JavaScript` 有 5 种原始类型（primitive type），即 `undefined`、`Null`、`Boolean`、`Number` 和 `String`。

在JavaScript中的数据类型主要有`数组`、`对象`。
并且JavaScript 拥有动态类型，这意味着相同的变量可用作不同的类型
```javascript
    console.log(typeof undefined)//输出  undefined
    console.log(typeof null)//输出  object
    console.log(typeof 1)//输出  number
    console.log(typeof "undefined")//输出  string!!!
    console.log(typeof "true")//输出  string
    console.log(typeof true)//输出  boolean
```

- #### 2.1 undefined
当声明的变量未初始化时，该变量的默认值是`undefined`，即该值的数据类型和数据内容都是`undefined`。  
```javascript
    var oTemp;
    alert(typeof oTemp); //输出  undefined 
    alert(oTemp ==undefined);//输出  true
```

但是，__值   `undefined` 并不同于`未定义的值`__，`typeof` 运算符会将`未定义`和`未声明`的变量数据类型都打印为`undefined`。

```javascript
    var oTemp;
    alert(typeof oTemp);  //输出  undefined 
    alert(typeof oTemp2);  //输出  undefined 
```
__请注意，对于`未声明的变量`使用除 `typeof` 之外的其他运算符的话，会引起错误，因为其他运算符只能用于`已声明`的变量上。__

例如，下面的代码将引发错误：
```javascript
    var oTemp;
    alert(oTemp2 == undefined);
```
当函数无明确返回值时，返回的也是值 `undefined`，如下所示：
```javascript
    function testFunc() {
    }

    alert(testFunc() == undefined);  //输出 "true"
```

- #### 2.2 Null
它只有一个专用值 `null`，即它的`字面量`。值 `undefined` 实际上是从值 `null` 派生来的，因此 `ECMAScript `把它们定义为相等的。
```javascript
    alert(null == undefined);  //输出 "true"
```
尽管这两个值相等，但它们的含义不同。`undefined` 是声明了变量但未对其初始化时赋予该变量的值，`null` 则用于表示`尚未存在`的对象（在讨论 typeof 运算符时，简单地介绍过这一点）。如果函数或方法要返回的是`对象`，那么找不到该对象时，返回的通常是 `null`。
```javascript
    alert(typeof null)// "object"
    alert(typeof {})// "object"
```
`typeof` 运算符对于 `null` 值会返回 `Object`，这实际上是 `JavaScript` 最初实现中的一个错误，然后被 `ECMAScript` 沿用了。现在，`null` 被认为是`对象的占位符`，从而解释了这一矛盾，但从技术上来说，它仍然是`原始值`。


```javascript
    alert(typeof !0)//boolean
    alert(!0)//true
```

- #### 2.1 字符串
字符串是存储字符（比如 "Bill Gates"）的变量。
字符串可以是引号中的任意文本。可以使用单引号或双引号，也可以在字符串中使用引号，只要不匹配包围字符串的引号即可。
```javascript
var answer="Nice to meet you!";
var answer="He is called 'Bill'";
var answer='He is called "Bill"';
```
- #### 2.2 数字
数字可以带小数点，也可以不带,极大或极小的数字可以通过科学（指数）计数法来书写。
```javascript
var x1=34.00;      //使用小数点来写
var x2=34;         //不使用小数点来写
var y=123e5;      // 12300000
var z=123e-5;     // 0.00123
```
- #### 2.3 布尔
布尔（逻辑）只能有两个值：true 或 false。

- #### 2.5 对象



- #### 2.4 数组
- #### 2.4.1 直接声明并赋值
```javascript
var cars=["Audi","BMW","Volvo"];
```
数组下标是基于零的，所以第一个项目是 [0]，第二个是 [1]，以此类推。
- #### 2.4.2 利用array新建数组对象
Array 对象用于在单个的变量中存储多个值。
创建 Array 对象的语法：
```javascript
new Array();
new Array(size);
new Array(element0, element1, ..., elementn);
```
> 参数

参数 size 是期望的数组元素个数。返回的数组，length 字段将被设为 size 的值。  
参数 element ..., elementn 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。  
> 返回值

返回新创建并被初始化了的数组。  
如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。  
当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为   `undefined` 的数组。  
当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。  
当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。