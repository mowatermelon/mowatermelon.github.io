---
title: 西瓜有话说之js对象学习初始篇
category: js_thinking
tags:
  - object
  - watermelon
  - js_thinking
date: 2017-10-16 00:00:00
---
# 1 js中何为对象

在 `JavaScript` 中，大多数事物都是`对象`, 从作为核心功能的`字符串`和`数组`，到建立在 JavaScript 之上的`浏览器 API`。你甚至可以自己创建`对象`，将相关的`函数`和`变量`封装打包成便捷的数据容器。理解这种`面向对象` (object-oriented, OO) 的特性对于进一步学习 JavaScript 语言知识是`必不可少`的。

<!-- more -->

`引用类型`通常叫做类（`class`），也就是说，遇到引用值，所处理的就是对象。

注意：从传统意义上来说，`ECMAScript` 并不真正具有`类`。事实上，除了说明不存在类，在 `ECMA-262` 中根本没有出现`类`这个词。`ECMAScript` 定义了`对象定义`，逻辑上`等价于`其他程序设计语言中的`类`。

对象是由 `new 运算符`加上要`实例化`的`对象的名字`创建的，一个`对象`是一个包含相关`资料`和`功能`的集体（通常由一些`变量`和`函数`组成，我们称之为对象里面的`属性`和`方法`）。这种语法与 `Java` 语言的相似，不过当有不止一个参数时，`ECMAScript` 要求使用`括号`。

如果没有参数，括号可以省略，注意：尽管括号不是必需的，但是为了避免混乱，最好使用括号。

# 2 名词字典

> 本文中出现变量名词的解释

```javascript
    var oo = new Object();
    var oBool = new Boolean(true);
    var oNum = new Number(68);
    var oString = new String("hello world");
    var oArray = new Array("demo","melon","water");
    var oDate = new Date();
```

|变量名|含义|举例|
|:---|:---|:---|
|objectName| 相关对象类型名称 |就像上面`js`代码中`Object`,`Boolean`,`Number`,`String`,`Array`,`Date`|
|varName| 相关对象类型实例化后的变量名 |就像上面`js`代码中`oo`,`oBool`,`oNum`,`oString`,`oArray`,`oDate`|
|param1,param2,param3,...,paramN|函数中需要传入第一个到第N个的参数值 |就像上面`js`代码中`true`,`68`,`hello world`|

# 3 js中对象的公有属性

|属性名|描述|使用方法|
|:---|:---|:---|
|constructor| 对创建对象的函数的引用（指针）。|varName.constructor|
|proto|对象具有属性`__proto__`，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型。|`varName.__proto__`|

> constructor

|对象名|属性值|使用方法|
|:---|:---|:---|
|Object| [Function: Object] |oo.constructor|
|Boolean| [Function: Boolean] |oBool.constructor|
|Number| [Function: Number] |oNum.constructor|
|String| [Function: String] |oString.constructor|
|Array| [Function: Array] |oArray.constructor|
|Date| [Function: Date] |oDate.constructor|

> __proto__

|对象名|属性值|使用方法|
|:---|:---|:---|
|Object| {} |`oo.__proto__`|
|Boolean| [Boolean: false] |`oBool.__proto__`|
|Number| [Number: 0] |`oNum.__proto__`|
|String| [String: ''] |`oString.__proto__`|
|Array| [] |`oArray.__proto__`|
|Date| Date {} |`oDate.__proto__`|

# 4 js中对象的公有方法

|方法名|描述|使用方法|
|:---|:---|:---|
|typeof| 判断该对象的类型，无论引用的是什么类型的对象，它都返回 `object`|typeof(varName)|
|instanceof| 判断该对象的实例化原型是不是某个对象类型，返回值是`true`或`false`|varName.instanceof(objectName)|
|isPrototypeOf| 判断该对象是否为另一个对象的原型，返回值是`true`或`false`。|varName.isPrototypeOf(objectName)|
|propertyIsEnumerable|判断给定的属性是否可以用 `for...in` 语句进行枚举，返回值是`true`或`false`。|varName.propertyIsEnumerable()|
|hasOwnProperty|判断对象是否有某个特定的属性，必须用字符串指定该属性，返回值是`true`或`false`。|varName.hasOwnProperty(param1)|
|toString| 返回对象的原始字符串表示|varName.toString(param1)|
|toLocaleString| 返回对象的值转化为本地原始字符串表示|varName.toLocaleString(param1)|
|valueOf|返回最适合该对象的原始值。|varName.valueOf()|

# 5 js中string和array类的公有方法

|方法名|描述|使用方法|
|:---|:---|:---|
|indexOf| 返回某个指定的字符串值在字符串中首次出现的位置，对大小写敏感|varName.indexOf(param1,param2)|
|lastIndexOf| 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索，对大小写敏感。|varName.lastIndexOf(param1,param2)|
|concat| 连接两个或多个字符串，可以接受传入多个参数，字符串返回值是拼接之后变量值，数组返回的是插入值之后数组，每传入一个参数|varName.concat(param1,param2,param3,...,paramN)|
