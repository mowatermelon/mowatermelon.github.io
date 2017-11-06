---
title: js学习之js数据类型
category: js学习
tags:
  - 数据类型
  - js学习
date: 2017-05-04 00:00:00
---

> 前不久我了解了js数组相关操作，才发现我的js在`数据类型`这块的基础真的很薄弱，所以整理了些文档，重新学习了一下。

# 1 DEFINTION

`数据类型`在`数据结构`中的定义是一个`值`的`集合`以及定义在这个`值集`上的一组`操作`。

<!--more-->

`变量`是用来`存储值`的`所在处`，它们有`名字`和``数据类型``。`变量`的`数据类型`决定了如何将代表这些`值`的`位存储`到计算机的`内存`中。在声明`变量`时也可指定它的`数据类型`。所有变量都具有`数据类型`，以决定能够存储`哪种数据`。

`数据类型`包括`原始类型`、`多元组`、`记录单元`、`代数数据类型`、`抽象数据类型`、`参考类型`以及`函数类型`。

# 2 PARAMETER

## 2.1 primitive type

在`JavaScript` 有 5 种原始类型（primitive type），即 `undefined`、`Null`、`Boolean`、`Number` 和 `String`。

并且JavaScript 拥有动态类型，这意味着相同的变量可用作不同的类型

```javascript
    var temp = undefined;
    console.log(typeof temp)//输出  undefined
    temp = null;
    console.log(typeof null)//输出  object
    temp = 1;
    console.log(typeof temp)//输出  number
    temp = "undefined";
    console.log(typeof "undefined")//输出  string!!!
    temp = "true";
    console.log(typeof temp)//输出  string
    temp = true;
    console.log(typeof true)//输出  boolean
```

### 2.1.1 undefined

当声明的变量未初始化时，该变量的默认值是`undefined`，即该值的数据类型和数据内容都是`undefined`。

```javascript
    var oTemp;
    console.log(typeof oTemp); //输出  undefined 
    console.log(oTemp ==undefined);//输出  true
```

但是，__值   `undefined` 并不同于`未定义的值`__，`typeof` 运算符会将`未定义`和`未声明`的变量数据类型都打印为`undefined`。

```javascript
    var oTemp;
    console.log(typeof oTemp);  //输出  undefined 
    console.log(typeof oTemp2);  //输出  undefined 
```
__请注意，对于`未声明的变量`使用除 `typeof` 之外的其他运算符的话，会引起错误，因为其他运算符只能用于`已声明`的变量上。__

例如，下面的代码将引发错误：

```javascript
    var oTemp;
    console.log(oTemp2 == undefined);
```

当函数无明确返回值时，返回的也是值 `undefined`，如下所示：

```javascript
    function testFunc() {
    }

    console.log(testFunc() == undefined);  //输出 "true"
```

### 2.1.2 Null

它只有一个专用值 `null`，即它的`字面量`。值`undefined`实际上是从值`null`派生来的，因此`ECMAScript`把它们定义为相等的。

```javascript
    console.log(null == undefined);  //输出 "true"
```

尽管这两个值相等，但它们的含义不同。`undefined` 是声明了变量但未对其初始化时赋予该变量的值，`null` 则用于表示`尚未存在`的对象（在讨论 typeof 运算符时，简单地介绍过这一点）。如果函数或方法要返回的是`对象`，那么找不到该对象时，返回的通常是 `null`。

```javascript
    console.log(typeof null)// "object"
    console.log(typeof {})// "object"
```

`typeof` 运算符对于 `null` 值会返回 `Object`，这实际上是 `JavaScript` 最初实现中的一个错误，然后被 `ECMAScript` 沿用了。现在，`null` 被认为是`对象的占位符`，从而解释了这一矛盾，但从技术上来说，它仍然是`原始值`。

也可以通过将变量的值设置为 null 来清空变量。

```javascript
    var temp ="";
    console.log(typeof temp);//string
    temp=null;
    console.log(typeof temp);//object
```

### 2.1.3 Boolean

`Boolean` 类型是 `ECMAScript` 中`最常用`的类型之一。它有两个值 `true` 和 `false` （即两个 `Boolean` `字面量`）。
即使 `false` 不等于 `0`，`0` 也可以在必要时被转换成 `false`，这样在 `Boolean` 语句中使用两者都是安全的。

```javascript
    var temp = true;
    console.log(typeof temp);//boolean
    temp = !0;
    console.log(typeof temp)//boolean
    console.log(temp)//true
```

### 2.1.4 Number

`ECMA-262` 中定义的最特殊的类型是 `Number` 类型。这种类型既可以表示 `32 位`的`整数`，还可以表示 `64 位`的`浮点数`。
直接输入的（而不是从另一个变量访问的）任何数字都被看做 `Number` 类型的`字面量`。例如，下面的代码声明了存放整数值的变量，它的值由`字面量` 86 定义：

```javascript
    var temp = 86;
    console.log(typeof temp);//number
    console.log(temp);//86
```

> 八进制数和十六进制数
  ___
整数也可以被表示为`八进制`（以 8 为底）或`十六进制`（以 16 为底）的`字面量`。尽管所有整数都可以表示为八进制或十六进制的字面量，但所有数学运算返回的都是十进制结果。

`八进制`的`字面量`的`首数字`必须是 `0`，其后的数字可以是任何`八进制数字`（0-7），如下面的代码所示：

```javascript
    var temp = 070;
    console.log(typeof temp);//number
    console.log(temp);//打印出来是显示十进制的56
```

要创建`十六进制`的`字面量`，`首位数字`必须为`0`，后面接`字母 x`(不分大小写)，然后是任意的`十六进制数字`（0 到 9 和 A 到 F）。这些字母可以是`大写`的，也可以是`小写`的。例如：

```javascript
    var temp = 0x1f;
    console.log(temp);//打印出来是显示十进制的31
    temp = 0xAB;
    console.log(temp);//打印出来是显示十进制的171
```

> 浮点数
  ___
要定义浮点值，必须包括小数点和小数点后的一位数字（例如，用 1.0 而不是 1）。这被看作浮点数字面量。例如：

```javascript
    var temp = 5.0;
    console.log(temp);//显示整数  5
    temp = 5.5;
    console.log(temp);//显示浮点数  5.5
    temp = 5.5+"";
    console.log(typeof temp);//string
```

对于浮点字面量的有趣之处在于，用它进行计算前，真正存储的是`字符串`。

> 科学计数法
  ___
对于`非常大`或`非常小`的数，可以用`科学计数法`表示`浮点数`，可以把一个数表示为数字（包括十进制数字）加 `e`（或 `E`），后面加乘以 `10` 的倍数。对于极小值的浮点可以通过`toFixed(number)`将指定数字截取小数点后`number`位，或者是利用`Math.round()`方法将一个数字舍入为最接近的整数,但是对于正整数，需要使用`toPrecision(number)`将整个数字截取指定`number`长度。

```javascript
    var temp = 5.618e7;
    console.log(temp);
    //显示整数  56180000  5.618 x 10^7
    temp = 8e-17;
    console.log(temp);//8e-17

    temp = 0.000000000000000000000000000001245893576484897879;
    console.log(temp);//1.2458935764848978e-30
    //请注意只显示小数点位后十六位，之后会省略
    console.log(temp.toFixed(2));//0.00
    console.log(temp.toPrecision(2));//1.2e-30
    console.log(Math.round(temp));//0

    temp = 124589357648489787900000000000000000000000000000;
    console.log(temp);//1.245893576484898e+47
    //请注意只显示小数点位后十五位，之后会省略
    console.log(temp.toFixed(2));//1.245893576484898e+47
    console.log(temp.toPrecision(2));//1.2e+47
    console.log(Math.round(temp));//1.245893576484898e+47
```
`ECMAScript` 默认把具有__6 个或 6 个以上__前导 0 的`浮点数`转换成`科学计数法`。也可用 基于`IEEE 754`标准的`64 位`形式存储`浮点值`，这意味着`十进制`值最多可以有 `17` 个`十进制位`。`17 位`之后的值将被`裁去`，从而造成一些小的`数学误差`。

```text
IEEE 754 标准是IEEE二进位浮点数算术标准（IEEE Standard for Floating-Point Arithmetic）的标准编号[1]  ，等同于国际标准ISO/IEC/IEEE 60559。该标准由美国电气电子工程师学会（IEEE）计算机学会旗下的微处理器标准委员会（Microprocessor Standards Committee, MSC）发布。

这个标准定义了表示浮点数的格式（包括负零-0）与反常值（denormal number），一些特殊数值（无穷（Inf）与非数值（NaN）），以及这些数值的「浮点数运算子」；它也指明了四种数值修约规则和五种例外状况（包括例外发生的时机与处理方式）
该标准的全称为IEEE二进位浮点数算术标准（ANSI/IEEE Std 754-1985），又称IEC 60559:1989，微处理器系统的二进位浮点数算术（本来的编号是IEC 559:1989）。

后来还有「与基数无关的浮点数」的「IEEE 854-1987标准」，有规定基数为2跟10的状况。现在最新标准是「IEEE 854-2008标准」。

IEEE 754 标准规定了计算机程序设计环境中的二进制和十进制的浮点数自述的交换、算术格式以及方法。
```

> 特殊的 Number 值
  ___
几个特殊值也被定义为 `Number` 类型。前两个是 `Number.MAX_VALUE` 和 `Number.MIN_VALUE`，它们定义了 `Number` 值集合的`外边界`。所有 `ECMAScript` 数都必须在这两个值之间。不过计算生成的数值结果可以不落在这两个值之间。
当计算生成的数大于 `Number.MAX_VALUE` 时，它将被赋予值 `Number.POSITIVE_INFINITY`，意味着不再有`数字值`。同样，生成的数值小于 `Number.MIN_VALUE` 的计算也会被赋予值 `Number.NEGATIVE_INFINITY`，也意味着不再有`数字值`。如果计算返回的是`无穷大值`，那么生成的结果不能再用于其他计算。
事实上，有专门的值表示`无穷大`，（如你猜到的）即 `Infinity`。`Number.POSITIVE_INFINITY` 的值为 `Infinity`。`Number.NEGATIVE_INFINITY` 的值为 `-Infinity`。
由于`无穷大数`可以是`正数`也可以是`负数`，所以可用一个方法判断一个数是否`是有穷的`（而不是单独测试每个无穷数）。可以对任何数调用`isFinite()`方法，以确保该数不是无穷大。对于数字可以调用`Number.isInteger()`验证数据是否是整型数据。

```javascript
var temp = Number.POSITIVE_INFINITY;
console.log(isFinite(temp));//false
var temp = 5;
console.log(isFinite(temp));//true
console.log(Number.isInteger("0.55"))//false
```

最后一个特殊值是 `NaN`，表示`非数`（Not a Number）。`NaN`是个奇怪的`特殊值`。一般说来，这种情况发生在类型（`String`、`Boolean` 等）转换失败时。例如，要把单词 blue 转换成数值就会失败，因为没有与之等价的数值。与无穷大一样，NaN 也不能用于算术计算。`NaN` 的另一个奇特之处在于，它与自身`不相等`。

```javascript
    var temp =  NaN;
    console.log(NaN == temp);  //输出 "false"
    //出于这个原因，不推荐使用 NaN 值本身。函数 isNaN() 会做得相当好
    temp =  NaN;
    console.log(isNaN(temp));  //输出 "true"
    temp =  666;
    console.log(isNaN(temp));  //输出 "false"
```

> Number 对象
  ___
Number 对象是原始数值的包装对象。

  - 创建 Number 对象的语法：

  ```javascript
  var temp=new Number("a");
  console.log(temp);
  /*
  Number {[[PrimitiveValue]]: NaN}
      __proto__:Number
      constructor:ƒ Number()
      toExponential:ƒ toExponential()
      toFixed:ƒ toFixed()
      toLocaleString:ƒ toLocaleString()
      toPrecision:ƒ toPrecision()
      toString:ƒ toString()
      valueOf:ƒ valueOf()
      __proto__:Object
      [[PrimitiveValue]]:0
  [[PrimitiveValue]]:NaN
  */
  var tmp=Number("b");
  console.log(tmp);//NaN
  tmp=Number("");
  console.log(tmp);//0
  ```

  - 参数

  参数 `value` 是要创建的 `Number` 对象的数值，或是要`转换成数字`的值。

  - 返回值

  当 `Number()` 和运算符 `new` 一起作为构造函数使用时，它返回一个新创建的 `Number` 对象。如果不用 `new` 运算符，把 `Number()` 作为一个`函数`来调用，它将把自己的参数转换成一个原始的数值，并且返回这个值（如果转换失败，则返回 `NaN`）。

  - Number 对象属性

|属性|描述|
|:-------|:-------|
|constructor|返回对创建此对象的 Number 函数的引用。|
|MAX_VALUE|可表示的最大的数。|
|MIN_VALUE|可表示的最小的数。|
|NaN|非数字值。|
|NEGATIVE_INFINITY|负无穷大，溢出时返回该值。|
|POSITIVE_INFINITY|正无穷大，溢出时返回该值。|
|prototype|使您有能力向对象添加属性和方法。|

  - Number 对象方法

|方法|描述|
|:-------|:-------|
|toString|把数字转换为字符串，使用指定的基数。|
|toLocaleString|把数字转换为字符串，使用本地数字格式顺序。|
|toFixed|把数字转换为字符串，结果的小数点后有指定位数的数字。|
|toExponential|把对象的值转换为指数计数法。|
|toPrecision|把数字格式化为指定的长度。|
|valueOf|返回一个 Number 对象的基本数字值。|

### 2.1.5 string

字符串是存储字符（比如 "Bill Gates"）的变量。
字符串可以是引号中的任意文本。可以使用单引号或双引号，也可以在字符串中使用引号，只要不匹配包围字符串的引号即可。
```javascript
var answer="Nice to meet you!";
var answer="He is called 'Bill'";
var answer='He is called "Bill"';
```

## 2.2 衍生 type

### 2.2.1 对象

### 2.2.2 数组

- 直接声明并赋值

```javascript
var cars=["Audi","BMW","Volvo"];
```

数组下标是基于零的，所以第一个项目是 [0]，第二个是 [1]，以此类推。

- 利用array新建数组对象

Array 对象用于在单个的变量中存储多个值。
创建 Array 对象的语法：

```javascript
new Array();
new Array(size);
new Array(element0, element1, ..., elementn);
```

- 参数

参数 size 是期望的数组元素个数。返回的数组，length 字段将被设为 size 的值。  
参数 element ..., elementn 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。
> 返回值

返回新创建并被初始化了的数组。
如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。
当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为   `undefined` 的数组。
当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。  
当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。