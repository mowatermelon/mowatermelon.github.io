---
title: 西瓜有话说之js对象学习初始篇
category: js_thinking
tags:
  - object
  - watermelon
  - js_thinking
date: 2017-10-20 00:00:00
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
|不推荐使用|该特性是非标准的，请尽量不要在生产环境中使用它。|如果下面属性和方法的描述中出现这五个字，意思最好不要使用这个属性或者这个方法。|
|已废弃|目前现行的几大主流浏览器都不支持了|如果下面属性和方法的描述中出现这三个字，意思你使用了这个一般会报错，或者直接返回undefined。|
|测试中|此功能某些浏览器尚在开发中，请参考浏览器兼容性表格以得到在不同浏览器中适合使用的前缀。由于该功能对应的标准文档可能被重新修订，所以在未来版本的浏览器中该功能的语法和行为可能随之改变。|如果下面属性和方法的描述中出现这三个字，意思你使用了这个不一定被所有浏览器都兼容，最好不要使用这个属性或者这个方法。|

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
|concat| 连接两个或多个字符串，可以接受传入多个参数，字符串返回值是拼接之后变量值，数组返回的是插入值之后数组。|varName.concat(param1,param2,param3,...,paramN)|
|slice| 返回对应字符串或者数组中下标从param1到param2的的元素|varName.slice(param1,param2)|

# 6 标准对象分类

## 6.1 值属性

这些全局属性返回一个简单的值；他们没有属性和方法。

- Infinity
- NaN
- undefined
- null 字面量

## 6.2 函数属性

这些全局函数 - 被称为全局而不是对象的函数 - 直接将其结果返回给调用者。

- eval()
- uneval() `测试中`
- isFinite()
- isNaN()
- parseFloat()
- parseInt()
- decodeURI()
- decodeURIComponent()
- encodeURI()
- encodeURIComponent()
- escape() `已废弃`
- unescape() `已废弃`

## 6.3 基本对象

这些是所有其他对象所基于的基本对象。这包括表示一般对象，函数和错误的对象。

- Object
- Function
- Boolean
- Symbol
- Error
- EvalError
- InternalError
- RangeError
- ReferenceError
- SyntaxError
- TypeError
- URIError

## 6.4 数字和日期

这些是表示数字，日期和数学计算的基础对象。

- Number
- Math
- Date

## 6.5 文本处理

这些对象表示字符串并支持操作它们。

- String
- RegExp

## 6.6 索引集合

这些对象表示由索引值排序的数据集合。这包括（类型）数组和类数组构造器。

- Array
- Int8Array
- Uint8Array
- Uint8ClampedArray
- Int16Array
- Uint16Array
- Int32Array
- Uint32Array
- Float32Array
- Float64Array

## 6.7 键的集合

这些对象表示使用键的集合；这些包含按插入顺序迭代的元素。

- Map
- Set
- WeakMap
- WeakSet

## 6.8 矢量集合

SIMD 矢量数据类型可以把数据整合到一个序列中。

- SIMD `不推荐使用`
- SIMD.Float32x4 `不推荐使用`
- SIMD.Float64x2 `不推荐使用`
- SIMD.Int8x16 `不推荐使用`
- SIMD.Int16x8 `不推荐使用`
- SIMD.Int32x4 `不推荐使用`
- SIMD.Uint8x16 `不推荐使用`
- SIMD.Uint16x8 `不推荐使用`
- SIMD.Uint32x4 `不推荐使用`
- SIMD.Bool8x16 `不推荐使用`
- SIMD.Bool16x8 `不推荐使用`
- SIMD.Bool32x4 `不推荐使用`
- SIMD.Bool64x2 `不推荐使用`

## 6.9 结构化数据

这些对象表示结构化数据缓冲区与使用 JSON 编码的数据进行交互。

- ArrayBuffer
- SharedArrayBuffer `不推荐使用`
- Atomics `不推荐使用`
- DataView
- JSON

## 6.10 控制抽象对象

- Promise
- Generator
- GeneratorFunction
- AsyncFunction `不推荐使用`

## 6.11 反射

- Reflect
- Proxy

## 6.12 国际化

增加ECMAScript核心的语言相关功能。

- Intl
- Intl.Collator
- Intl.DateTimeFormat
- Intl.NumberFormat

## 6.13 WebAssembly

- WebAssembly
- WebAssembly.Module
- WebAssembly.Instance
- WebAssembly.Memory
- WebAssembly.Table
- WebAssembly.CompileError
- WebAssembly.LinkError
- WebAssembly.RuntimeError

## 6.14 其他

- arguments