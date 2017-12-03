---
title: 西瓜有话说之js对象学习string篇
category: js_thinking
tags:
  - string
  - watermelon
  - js_thinking
date: 2017-10-25 00:00:00
---
# 1. 定义

## 1.1 基本字符串

字符串字面量 (通过单引号或双引号定义) 和 直接调用 String方法(没有通过 new 生成字符串对象实例)的字符串都是基本字符串。基本字符串是没有相关扩展方法，只有将基本字符串可转化为字符串对象之后才可以使用字符串对象的方法，当基本字符串需要调用一个字符串对象才有的方法或者查询值的时候，JavaScript会自动将基本字符串转换为字符串对象，并且调用相应的方法或者执行查询。

<!-- more -->

## 1.2 字符串对象

一个用于字符串或一个字符序列的构造函数。字符串对于可以保存以文本形式表示的数据非常有用。 一些常用的字符串操作有：查询字符串长度，使用 `+` 和 `+=` 运算符来构建和连接字符串，使用 indexOf 方法检查某一子字符串在父字符串中的位置，又或是使用substring方法提取从父字符串中提取子字符串。

## 1.3 模板字符串

模板字面量/Template literals 是允许嵌入表达式的字符串字面量。你可以使用多行字符串和字符串插值功能。它们在ES2015规范的先前版本中被称为模板字符串/template strings。

模板字符串使用反引号 (\` \`) 来代替普通字符串中的用双引号和单引号。模板字符串可以包含特定语法(`${expression}`)的占位符。占位符中的表达式和周围的文本会一起传递给一个默认函数，该函数负责将所有的部分连接起来，如果一个模板字符串由表达式开头，则该字符串被称为带标签的模板字符串，该表达式通常是一个函数，它会在模板字符串处理后被调用，在输出最终结果前，你都可以通过该函数来对模板字符串进行操作处理。在模版字符串内使用反引号（\`）时，需要在它前面加转义符（\）。

```javascript
`\`` === "`" // --> true
```

# 2. 名词字典

> 本文中出现变量名词的解释

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
//D800-DBFF UTF-16的高半区 High-half zone of UTF-16
//DC00-DFFF UTF-16的低半区 Low-half zone of UTF-16
var oString_1 = 'A \uD87E\uDC04 Z';
var tString_1 =`hello Template`;
var tString_2 =`hello line 1
 hello line 2`;
//`string text ${expression} string text`  在模版字符串中使用表达式
var tString_3 =`Fifteen is ${a + b} and\nnot ${2 * a + b}.`;

function tag(strings, ...values) {
 //String存储的是非expression的字符串
 //values存储的是expression计算之后的值
  console.log(strings[0]); // "Hello "  在第一个expression前的值
  console.log(strings[1]); // " world " 在第二个expression前的值
  console.log(strings[2]); // "hahaha"  在第三个expression前的值
  console.log(strings[3]); // "" 在第三个expression后的值
  console.log(values[0]);  // 12  第一个expression的值
  console.log(values[1]);  // 32  第二个expression的值
  console.log(values[2]); // 0.5  第三个expression的值

  return "大吉大利今晚吃西瓜!";
}

console.log(strString);//hello watermelon
console.log(oString);//[String: 'hello world']
console.log(oString_1);//A 你 Z   中间不在BMP中的字符，会显示乱码
console.log(tString_1);//hello Template
//打印出来会保留原格式 比如原有的换行和缩进
console.log(tString_2);//hello Template line 1 \n \t hello Template line 2
// tag(tString_1);//h e l l undefined undefined undefined
// tag(tString_2);//h e l l undefined undefined undefined
// tag(tString_3);//F i f t undefined undefined undefined
console.log(tString_3);//Fifteen is 12 and \n  not 16.

//tag `string text ${expression} string text`  在模版字符串中使用tag方法
//在没有调用console之前，不会打印 大吉大利今晚吃西瓜!
//tString_4的值其实就是tag函数的返回值   大吉大利今晚吃西瓜!
var tString_4 = tag`Hello ${ a + b } world ${ a * b}hahaha ${ a / b}`;

```

|变量名|含义|举例|
|:---|:---|:---|
|objectName| 相关对象类型名称 |就像上面`js`代码中`String`|
|varName| 相关对象类型实例化后的变量名 |就像上面`js`代码中`strString`,`oString`,`tString_1`|
|varName_val| 相关对象类型实例化后的实际内容 |就像上面`js`代码中`hello watermelon`|
|functionName|函数名称|就像上文的`tag`|
|BMP|基本多文种平面（Basic Multilingual Plane），或称第0平面或0号平面（Plane 0），是`Unicode`中的一个编码区段。编码从`U+0000`至`U+FFFF`。
现版本为修订10.0.0版，2017年6月20日出版。|无举例|
|letter|字母|letter(8) 代表八个子母，一个字母长度为一|
|char|汉字|char(8) 代表八个汉字，一个汉字长度为一|
|num|数字|num(8) 代表八个数字，一个数字长度为一|
|sign|符号|sign(8) 代表八个符号，一个符号长度为一|
|\s|空格符|\s(8) 代表八个空格符，一个空格符长度为一|
|\t|缩进符|\t(8) 代表八个缩进符，一个缩进符长度为四|
|\n|换行符|\n(8) 代表八个换行符，一个换行符长度为一|
|\u|换行符|\u(8) 代表八个非BMP字符，一个非BMP字符长度为二|
|param1,param2,param3,...,paramN|函数中需要传入第一个到第N个的参数值 |就像上面`js`代码中`hello world`|
|柔和方法|不会改变字符串原始值|就是执行某个方法之后，`varName`原本所包含的内容不会变化|
|强硬方法|会改变字符串原始值|就是执行某个方法之后，`varName`原本所包含的内容会变化|
|父字符串|原始的对象内容|就像上面`js`代码中`strString`,`oString`,`tString_1`|
|子字符串|传入需要检索或者替换的参数值|就像上面`js`代码中`hello watermelon`|
|接受负值参|函数接受负值的参数，并且可以正常处理返回对应的值|如果方法的描述中出现这五个字，则代表这个方法接受负值参数，如果没有出现，则代表不接受，请注意|
|不推荐使用|该特性是非标准的，请尽量不要在生产环境中使用它。|如果下面属性和方法的描述中出现这五个字，意思最好不要使用这个属性或者这个方法。|
|已废弃|目前现行的几大主流浏览器都不支持了|如果下面属性和方法的描述中出现这三个字，意思你使用了这个一般会报错，或者直接返回undefined。|
|测试中|此功能某些浏览器尚在开发中，请参考浏览器兼容性表格以得到在不同浏览器中适合使用的前缀。由于该功能对应的标准文档可能被重新修订，所以在未来版本的浏览器中该功能的语法和行为可能随之改变。|如果下面属性和方法的描述中出现这三个字，意思你使用了这个不一定被所有浏览器都兼容，最好不要使用这个属性或者这个方法。|

# 3. 字符串的属性

## 3.1 继承对象的属性

|属性名|描述|使用方法|
|:---|:---|:---|
|constructor| 对创建对象的函数的引用（指针）。|varName.constructor|
|`__proto__`|对象具有属性`__proto__`，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型。|`varName.__proto__`|
|length|字符串的长度。|varName.length|
|`__count__`| `已废弃`，用来存放对象的可枚举的属性的个数|`varName.__count__`|
|`__noSuchMethod__`|`已废弃`，属性曾经是指当调用某个对象里不存在的方法时即将被执行的函数，在`__noSuchMethod__`属性被移除之后，`ECMAScript 2015 (ES6)` 规范转而采用 `Proxy` 对象。|`varName.__noSuchMethod__ = fun(id, args){}` @param1 id 调用的不存在的方法名 @param2 args 传递给该方法的参数数组|
|`__parent__`|`已废弃`，指向一个对象的上下文，对于最顶层对象来说,这个属性的值就是全局对象`window`。|`varName.__parent__`|

## 3.2 继承funciton的属性

|属性名|描述|使用方法|
|:---|:---|:---|
|arguments| `不推荐使用`，属性代表传入函数的实参，它是一个类数组对象。已经被废弃很多年了，现在推荐的做法是使用函数内部可用的 `arguments` 对象来访问函数的实参。在函数递归调用的时候（在某一刻同一个函数运行了多次，也就是有多套实参），那么 `arguments` 属性的值是最近一次该函数调用时传入的实参。如果函数不在执行期间，那么该函数的 `arguments` 属性的值是 `null`。|objectName.arguments or functionName.arguments|
|arity|`已废弃`，返回一个函数的形参数量，是一个古老的已经没有浏览器支持的属性,你应该使用`length`属性来代替.。|objectName.arity or functionName.arity|
|caller| `不推荐使用`，如果一个函数`functionName`是在`全局作用域`内被调用的,则`functionName.caller`为`null`,相反,如果一个函数是在另外一个函数作用域内被调用的,则`functionName.caller`指向调用它的`那个函数`，该属性的常用形式`arguments.callee.caller`替代了被废弃的`arguments.caller`。|objectName.caller or functionName.caller|
|displayName| `不推荐使用`，获取函数的显示名称。|objectName.displayName or functionName.displayName|
|length|指明函数的形参个数，length 是函数对象的一个属性值，指该函数有多少个必须要传入的参数，即形参的个数。形参的数量不包括剩余参数个数，仅包括第一个具有默认值之前的参数个数。与之对比的是，arguments.length 是函数被调用时实际传参的个数。|objectName.length or functionName.length|
|name|返回一个函数声明的名称，使用`new Function(...)`语法创建的函数或只是 `Function(...)` create Function对象及其名称为`anonymous`。|objectName.name or functionName.name|
|prototype|函数对象具有属性`__proto__`，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型。|objectName.prototype or functionName.prototype|

## 3.3  字符串的常用属性值

### 3.3.1 constructor

|变量名|调取方式|属性值|
|:---|:---|:---|
|strString| strString.constructor |[Function: String]|
|oString| oString.constructor |[Function: String]|
|`oString_1`| oString_1.constructor |[Function: String]|
|`tString_1`| tString_1.constructor |[Function: String]|
|`tString_2`| tString_2.constructor |[Function: String]|
|`tString_3`| tString_3.constructor |[Function: String]|
|`tString_4`| tString_4.constructor |[Function: String]|

### 3.3.2 __proto__

|变量名|调取方式|属性值|
|:---|:---|:---|
|strString| `strString.__proto__` |[String: '']|
|oString| `oString.__proto__` |[String: '']|
|`oString_1`| `oString_1.__proto__` |[String: '']|
|`tString_1`| `tString_1.__proto__` |[String: '']|
|`tString_2`| `tString_2.__proto__` |[String: '']|
|`tString_3`| `tString_3.__proto__` |[String: '']|
|`tString_4`| `tString_4.__proto__` |[String: '']|

### 3.3.3 length

|变量名|调取方式|属性值|解释|
|:---|:---|:---|:---|
|strString| strString.length |16|letter(15)+\s(1)|
|oString| oString.length |11|letter(10)+\s(1)|
|`oString_1`| oString_1.length |6|letter(2)+\s(2)+\u(1)|
|`tString_1`| tString_1.length |14|letter(13)+\s(1)|
|`tString_2`| tString_2.length |41|letter(18)+num(2)+\s(4)+\t(4)+\n(1)|
|`tString_3`| tString_3.length |25|letter(15)+num(4)+\s(4)+sign(1)+\n(1)|
|`tString_4`| tString_4.length |10|char(9)+sign(1)|

## 3.4 注意事项

|特性名称| 是否可修改|
|:---|:---|
|writable|false|
|enumerable|false|
|configurable|false|

> 提示

所有 `String` 的`实例`都继承自 `String.prototype`. 任何`String.prototype`上的改变都会影响到所有的 `String` 实例。

> 但是请注意由于每个`varName`的构造方法不同，所以在`instanceof`时候的结果不同，`instanceof` 运算符用来测试一个`对象`在其`原型链`中是否存在一个`构造函数`的 `prototype` 属性。

```javascript
//使用方法
object instanceof constructor
or object instanceof(constructor)
// @param1 object 要检测的对象.
// @param2 constructor 某个构造函数
//instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。
```

|变量名|调取方式|属性值|
|:---|:---|:---|
|strString| strString instanceof(String)|false|
|oString| oString instanceof(String)|true|
|`tString_1`| tString_1 instanceof(String)|false|
|`tString_2`| tString_2 instanceof(String)|false|
|`tString_3`| tString_3 instanceof(String)|false|
|`tString_4`| tString_4 instanceof(String)|false|

# 4. 字符串对象的柔和方法

## 4.1. HTML相关方法

### 4.1.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|big()|  `不推荐使用`，把字符串显示为大号字体，只在页面中才会有大两个字体号效果。|无|
|small()| `不推荐使用`， 把字符串显示为小号字体，只在页面中才会有小两个字体号效果。|无|
|blink()| `不推荐使用`， 把字符串显示闪动的字符串，目前没有看到有浏览器支持|无|
|bold()| `不推荐使用`， 把字符串显示粗体的字符串，只在页面中才会有粗体效果，IE不兼容。|无|
|italics()| `不推荐使用`，把字符串显示为斜体，只在页面中才会有效果。|无|
|strike()| `不推荐使用`， 把字符串显示为加了删除线的字符串，只在页面中才会有效果。|无|
|fixed()| `不推荐使用`， 把字符串显示为打字机文本显示的字符串，只在页面中才会有效果。|无|
|sub()|  `不推荐使用`，把字符串显示为下标，只在页面中才会有效果。|无|
|sup()| `不推荐使用`， 把字符串显示为上标，只在页面中才会有效果。|无|
|anchor(anchorname)|  `不推荐使用`，创建 `HTML` 锚。将字符串输出为有唯一标识的纯粹`a`标签，只在页面中才会有效果。| @para anchorname 必需，为锚定义名称。如果没有传入参数，则会输出一个`name`属性为`undefined`的`a`标签。|
|link(url)| `不推荐使用`， 把字符串显示为链接，只在页面中才会有效果。如果没有传入参数，则会输出一个href属性为`undefined`的a标签。| @para url必需，规定要链接的 URL。|
|fontcolor(color)| `不推荐使用`，返回指定的颜色的字符串。只在页面中才会有效果如果没有传入参数，则会输出一个`color`属性为`undefined`的font标签。| @para  color必需。为字符串规定 font-color。该值必须是颜色名(red)、RGB 值(rgb(255,0,0))或者十六进制数(#FF0000)。|
|fontsize(size)| `不推荐使用`， 返回指定的字体大小的字符串。只在页面中才会有效果。如果没有传入参数，则会输出一个`size`属性为`undefined`的`font`标签。|  @para size 参数必须是从 1 至 7 的数字，数字越大字体越大。|

### 4.1.2 详细

> 1 big()

|使用方法|结果|
|:---|:---|
|varName.big()|`<big>varName_val</big>`|

> 2 small()

|使用方法|结果|
|:---|:---|
|varName.small()|`<small>varName_val</small>`|

> 3 blink()

|使用方法|结果|
|:---|:---|
|varName.blink()|`<blink>varName_val</blink>`|

> 4 bold()

|使用方法|结果|
|:---|:---|
|varName.bold()|`<b>varName_val</b>`|

> 5 italics()

|使用方法|结果|
|:---|:---|
|varName.italics()|`<i>varName_val</i>`|

> 6 strike()

|使用方法|结果|
|:---|:---|
|varName.strike()|`<strike>varName_val</strike>`|

> 7 fixed()

|使用方法|结果|
|:---|:---|
|varName.fixed()|`<tt>varName_val</tt>`|

> 8 sub()

|使用方法|结果|
|:---|:---|
|varName.sub()|`<sub>varName_val</sub>`|

> 9 sup()

|使用方法|结果|
|:---|:---|
|varName.sup()|`<sup>varName_val</sup>`|

> 10 anchor(anchorname)

|使用方法|结果|
|:---|:---|
|varName.anchor(param1)|`<a name="param1">varName_val</a>`|

> 11 link(url)

|使用方法|结果|
|:---|:---|
|varName.link(param1)|`<a href="param1">varName_val</a>`|

> 12 fontcolor(color)

|使用方法|结果|
|:---|:---|
|varName.fontcolor(param1)|`<font color="param1">varName_val</font>`|

> 13 fontsize(size)

|使用方法|结果|
|:---|:---|
|varName.fontsize(param1)|`<font size="param1">varName_val</font>`|

## 4.2. 编码

### 4.2.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|charAt(index)|  返回特定位置的字符，不提供参数就返回第一个字符的字符，提供游标值，就返回指定游标的字符| @para index 非必需，一个介于0 和字符串长度减1之间的正整数。 (0~varName.length-1)，如果不是一个数值，则默认为 0。|
|charCodeAt(index)| 返回0到65535之间的整数，表示给定索引处的`UTF-16`代码单元 (在 `Unicode` 编码单元表示一个单一的 `UTF-16` 编码单元的情况下，`UTF-16` 编码单元匹配 `Unicode` 编码单元。但在——例如 `Unicode` 编码单元 > `0x10000` 的这种——不能被一个 `UTF-16` 编码单元单独表示的情况下，只能匹配 `Unicode` 代理对的第一个编码单元) 。|@para index 一个大于等于 0，小于字符串长度的整数。(0~varName.length-1)，如果不是一个数值，则默认为 0。|
|codePointAt()| `不推荐使用`， 返回使用UTF-16编码的给定位置的值的非负整数。|@para pos 这个字符串中需要转码的元素的位置。|
|normalize()| `不推荐使用`， 返回调用字符串值的Unicode标准化形式。|无|
|fromCharCode()| `不推荐使用`， 返回一个字符串，而不是一个 String 对象。由于 fromCharCode 是 String 的静态方法，所以应该像这样使用：String.fromCharCode()，而不是作为你创建的 String 对象的方法。|num1, ..., numN|
|fromCodePoint()| `不推荐使用`， 返回使用 Unicode 编码创建的字符串，如果传入无效的 Unicode 编码，将会抛出一个RangeError (例如： "RangeError: NaN is not a valid code point")。。|num1, ..., numN|

### 4.2.2 详细

> 1 charAt(index)

字符串中的字符从左向右索引，第一个字符的索引值为`0`，最后一个字符（假设该字符位于字符串 `varName` 中）的索引值为`varName.length - 1`。 如果指定的`index`值超出了该范围，则返回一个空字符串。而且本方法不管你传入多少参数，这边只会处理传入的第一个参数值，如果传进来为小数，这个方法是向上取整，举个栗子，你传入的值是`1.2`,这边就认为你传入的是`2`。

但是请注意，这个方法只能检测打印包含基本多文种平面（BMP）中的字符，如果字符串中包含的内容不在BMP中，打印的结果就会乱码。

|使用方法|结果|
|:---|:---|
|oString.charAt()|h|
|oString.charAt(oString.length-1)|d|

> 错误示例

|使用方法|结果|
|:---|:---|
|oString.charAt(1.2)|e|
|oString.charAt(1,2,3)|h|
|oString.charAt(-2)|空字符串|
|oString.charAt(oString)|h|
|oString.charAt(true)|e|
|oString.charAt(false)|h|
|oString.charAt(null)|h|
|oString.charAt(undefined)|h|
|oString.charAt(NaN)|h|
|oString.charAt(oo)|h|
|oString.charAt(oNum)|空字符串|
|oString.charAt(oArray)|h|
|oString.charAt(oDate)|空字符串|
|oString.charAt(oString.length)|空字符串|

> 2 charCodeAt()

Unicode 编码单元（code points）的范围从 0 到 1,114,111（0x10FFFF）。开头的 128 个 Unicode 编码单元和 ASCII 字符编码一样。关于 Unicode 的更多信息，可查看 JavaScript Guide。

注意，`charCodeAt` 总是返回一个小于 65,536 的值。这是因为高位编码单元（higher code point）使用一对（低位编码（lower valued））代理伪字符（"surrogate" pseudo-characters）来表示，从而构成一个真正的字符。因此，为了查看或复制（reproduce）65536 及以上编码字符的完整字符，需要在获取 `charCodeAt(i)` 的值的同时获取 `charCodeAt(i+1)` 的值（如同查看/reproducing 拥有两个字符的字符串一样），或者改为获取 codePointAt(i) 的值

如果指定的 index 小于 0 或不小于字符串的长度，则 `charCodeAt` 返回 `NaN`。返回值是一表示给定索引处（`varName`中`index`索引处）字符的 `UTF-16` 代码单元值的数字；如果索引超出范围，则返回 `NaN`。如果你想要整个代码点的值，使用 `codePointAt()`。

向后兼容：在历史版本中（如 JavaScript 1.2），`charCodeAt` 返回一个数字，表示给定 `index` 处字符的 `ISO-Latin-1` 编码值。`ISO-Latin-1`编码集范围从 0 到 255。开头的 0 到 127 直接匹配 `ASCII` 字符集。

|使用方法|结果|
|:---|:---|
|oString.charCodeAt()|104|
|oString.charCodeAt(oString.length-1)|d|

> 错误示例

|使用方法|结果|
|:---|:---|
|oString.charCodeAt(1.2)|101|
|oString.charCodeAt(1,2,3)|104|
|oString.charCodeAt(-2)|NaN|
|oString.charCodeAt(oString)|104|
|oString.charCodeAt(true)|101|
|oString.charCodeAt(false)|104|
|oString.charCodeAt(null)|104|
|oString.charCodeAt(undefined)|104|
|oString.charCodeAt(NaN)|104|
|oString.charCodeAt(oo)|104|
|oString.charCodeAt(oNum)|NaN|
|oString.charCodeAt(oArray)|104|
|oString.charCodeAt(oDate)|NaN|
|oString.charCodeAt(oString.length)|NaN|

> 常用的编码表

|字符|对应的unicode值|
|:---|:---|
|\t(水平制表符)|9|
|\n(换行符)|10|
|\s(空格)|32|
|\!(感叹号)|33|
|\"|34|
|\#|35|
|\$|36|
|\%|37|
|\&|38|
|\'|39|
|\(|40|
|\)|41|
|\*|42|
|+|43|
|,|44|
|-|45|
|.(英文句号)|46|
|/|47|
|0|48|
|1|49|
|2|50|
|3|51|
|4|52|
|5|53|
|6|54|
|7|55|
|8|56|
|9|57|
|:|58|
|;|59|
|<|60|
|=|61|
|>|62|
|?|63|
|@|64|
|A|65|
|Z|90|
|[|91|
|\|92|
|]|93|
|^|94|
|_|95|
|`|96|
|a|97|
|z|122|
|{|123|
|||124|
|}|125|
|~|126|
|;|127|

> 3 codePointAt()

|使用方法|结果|
|:---|:---|
|varName.codePointAt()||

> 4 normalize()

|使用方法|结果|
|:---|:---|
|varName.normalize()||

> 5 fromCharCode()

尽管绝大部分常用的 Unicode 值可以用一个 16-bit 数字表示（正如 JavaScript 标准化过程早期），并且对于绝大部分值 fromCharCode() 返回一个字符（即对于绝大部分字符 UCS-2 值是 UTF-16 的子集），但是为了处理所有的 Unicode 值（至 21 bits），只用 fromCharCode() 是不足的。
由于高位编码字符是用两个低位编码（lower value）表示形成的一个字符，因此String.fromCodePoint() （ES6 草案的一部分）被用来返回这样一对低位编码，从而可以完全表示这些高位编码字符。

|使用方法|结果|
|:---|:---|
|objectName.fromCharCode(num1[, ...[, numN]])||

> 6 fromCodePoint()

|使用方法|结果|
|:---|:---|
|objectName.fromCodePoint(num1[, ...[, numN]])||

## 4.3. 检索

### 4.3.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|includes()|  `不推荐使用`，判断一个字符串里是否包含其他字符串。|无|
|endsWith()| `不推荐使用`， 判断一个字符串的结尾是否包含其他字符串中的字符。|无|
|indexOf()| 从字符串对象中返回首个被发现的给定值的索引值，如果没有找到则返回-1。|无|
|lastIndexOf()|  从字符串对象中返回最后一个被发现的给定值的索引值，如果没有找到则返回-1。|无|
|startsWith()| `不推荐使用`，判断字符串的起始位置是否匹配其他字符串中的字符。|无|

### 4.3.2 详细

> 1 includes()

|使用方法|结果|
|:---|:---|
|varName.includes()||

> 2 endsWith()

|使用方法|结果|
|:---|:---|
|varName.endsWith()||

> 3 indexOf()

|使用方法|结果|
|:---|:---|
|varName.indexOf()||

> 4 lastIndexOf()

|使用方法|结果|
|:---|:---|
|varName.lastIndexOf()||

> 5 startsWith()

|使用方法|结果|
|:---|:---|
|varName.startsWith()||

## 4.4. 比较

### 4.4.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|localeCompare()|  返回一个数字表示是否引用字符串在排序中位于比较字符串的前面，后面，或者二者相同。|无|
|match()| 使用正则表达式与字符串相比较。|无|

### 4.4.2 详细

> 1 localeCompare()

|使用方法|结果|
|:---|:---|
|varName.localeCompare()||

> 2 match()

|使用方法|结果|
|:---|:---|
|varName.match()||

## 4.5. 拼接

### 4.5.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|concat()|  连接两个字符串文本，并返回一个新的字符串。|无|
|padEnd()| `不推荐使用`， 从给定字符串的末端填充当前字符串，以从给定长度创建新字符串。|无|
|padStart()| `不推荐使用`， 从一个给定字符串开始填充当前字符串，从给定长度创建一个新字符串。|无|
|repeat()| `不推荐使用`，返回指定重复次数的由元素组成的字符串对象。|无|
|quote()| `已废弃`，用双引号（“”）包装字符串。|无|

### 4.5.2 详细

> 1 concat()

|使用方法|结果|
|:---|:---|
|varName.concat()||

> 2 padEnd()

|使用方法|结果|
|:---|:---|
|varName.padEnd()||

> 3 padStart()

|使用方法|结果|
|:---|:---|
|varName.padStart()||

> 4 repeat()

|使用方法|结果|
|:---|:---|
|varName.repeat()||

> 5 quote()

|使用方法|结果|
|:---|:---|
|varName.quote()||

## 4.6. 大小写转换

### 4.6.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|toLowerCase()| 将字符串转换成小写并返回。|无|
|toLocaleLowerCase()|根据当前区域设置，将符串中的字符转换成小写。对于大多数语言来说，toLowerCase的返回值是一致的。|无|
|toUpperCase()| 将字符串转换成大写并返回。|无|
|toLocaleUpperCase()| 根据当前区域设置，将字符串中的字符转换成大写，对于大多数语言来说，toUpperCase的返回值是一致的。|无|

### 4.6.2 详细

> 1 toLowerCase()

|使用方法|结果|
|:---|:---|
|varName.toLowerCase()||

> 2 toLocaleLowerCase()

|使用方法|结果|
|:---|:---|
|varName.toLocaleLowerCase()||

> 3 toUpperCase()

|使用方法|结果|
|:---|:---|
|varName.toUpperCase()||

> 4 toLocaleUpperCase()

|使用方法|结果|
|:---|:---|
|varName.toLocaleUpperCase()||

# 5. 字符串对象的强硬方法

## 5.1. 强制类型转化

|方法名|描述|使用方法|
|:---|:---|:---|
|String|强制类型转化，将其他类型的变量转化成`String`类型|String(varName)|

|参数值|举例|转换结果|
|:---|:---|:---|
|负数|-1|-1|
|空|null|null|
|未定义|undefined|undefined|
|非数值|NaN|NaN|
|对象|new Object()|[object Object]|

```javascript
  //在大部分情况下String()和toString()效果相同
  //但是 对 null 和 undefined 值强制类型转换可以生成字符串而不引发错误
  // 而null 和 undefined 值强制使用toString()，却会引发错误
  console.log(String(-0))//0
  console.log(String(-1))//-1
  console.log(String(null))//null
  console.log(String(undefined))//undefined
  console.log(String(NaN))//NaN

  //将其他对象类型化成string类型的时候，其实传入String的值是每个对象原始的默认值
  //object对象的默认值是object
  //Boolean对象的默认值是false
  //Number对象的默认值是0
  //String对象的默认值是''
  //Array对象的默认值是[]
  //日期的默认值是当前日期
  console.log(String(new Object()))//[object Object]
  console.log(String(new Boolean()))//false
  console.log(String(new Number()))//0
  console.log(String(new String()))//""
  console.log(String(new Array()))//""
  console.log(String(new Date()))//Sat Nov 18 2017 15:45:07 GMT+0800 (CST)
```

## 5.2. 替换

### 5.2.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|replace()|  被用来在正则表达式和字符串直接比较，然后用新的子串来替换被匹配的子串。|无|
|search()| 对正则表达式和指定字符串进行匹配搜索，返回第一个出现的匹配项的下标。|无|

### 5.2.2 详细

> 1 replace()

|使用方法|结果|
|:---|:---|
|varName.replace()||

> 2 search()

|使用方法|结果|
|:---|:---|
|varName.search()||

## 5.3. 分割

### 5.3.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|slice()|  摘取一个字符串区域，返回一个新的字符串。|无|
|split()| 通过分离字符串成字串，将字符串对象分割成字符串数组。|无|
|substr()| 通过指定字符数返回在指定位置开始的字符串中的字符。|无|
|substring()| 返回在字符串中指定两个下标之间的字符。|无|

### 5.3.2 详细

> 1 slice()

|使用方法|结果|
|:---|:---|
|varName.slice()||

> 2 split()

|使用方法|结果|
|:---|:---|
|varName.split()||

> 3 substr()

|使用方法|结果|
|:---|:---|
|varName.substr()||

> 4 substring()

|使用方法|结果|
|:---|:---|
|varName.substring()||

## 5.4. 格式转化

### 5.4.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|trim()|  `不推荐使用`，从字符串的开始和结尾去除空格。参照部分 ECMAScript 5 标准。|无|
|trimLeft()| `不推荐使用`， 从字符串的左侧去除空格。|无|
|trimRight()| `不推荐使用`， 从字符串的右侧去除空格。|无|

### 5.4.2 详细

> 1 trim()

|使用方法|结果|
|:---|:---|
|varName.trim()||

> 2 trimLeft()

|使用方法|结果|
|:---|:---|
|varName.trimLeft()||

> 3 trimRight()

|使用方法|结果|
|:---|:---|
|varName.trimRight()||

## 5.5. 对象通用方法

### 5.5.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|toString()|  `不推荐使用`，返回用字符串表示的特定对象。重写 Object.prototype.toString 方法。|无|
|toLocaleString()|  `不推荐使用`，返回用字符串表示的特定对象。|无|
|valueOf()| `不推荐使用`， 返回特定对象的原始值。重写 Object.prototype.valueOf 方法。|无|
|toSource()| `测试中`，返回一个对象文字代表着特定的对象。你可以使用这个返回值来创建新的对象。重写 `Object.prototype.toSource` 方法。|无|
|`[@@iterator]()`| `不推荐使用`，返回一个新的迭代器对象遍历一个字符串值的代码，每个代码点返回一个字符串值。|无|
|`__defineGetter__()`|  `不推荐使用`|无|
|`__defineSetter__()`|  `不推荐使用`|无|
|`__lookupGetter__()`|  `不推荐使用`|无|
|`__lookupSetter__()`|   `不推荐使用`|无|
|hasOwnProperty()|   `不推荐使用`|无|
|isPrototypeOf()|   `不推荐使用`|无|
|setPrototypeOf()|   `不推荐使用`|无|
|unwatch()|   `不推荐使用`|无|
|watch()|   `不推荐使用`|无|
|propertyIsEnumerable()|   `不推荐使用`|无|

### 5.5.2 详细

> 1 toString()

|使用方法|结果|
|:---|:---|
|varName.toString()||

> 2 toLocaleString()

|使用方法|结果|
|:---|:---|
|varName.toLocaleString()||

> 3 valueOf()

|使用方法|结果|
|:---|:---|
|varName.valueOf()||

> 4 `[@@iterator]()`

|使用方法|结果|
|:---|:---|
|varName[0]||

> 5 toSource()

|使用方法|结果|
|:---|:---|
|varName.toSource()||

> 6 `__defineGetter__()`

|使用方法|结果|
|:---|:---|
|varName.toString()||

> 7 `__defineSetter__()`

|使用方法|结果|
|:---|:---|
|varName.valueOf()||

> 8 `__lookupGetter__()`

|使用方法|结果|
|:---|:---|
|varName[0]||

> 9 `__lookupSetter__()`

|使用方法|结果|
|:---|:---|
|varName.toSource()||

> 10 hasOwnProperty()

|使用方法|结果|
|:---|:---|
|varName.toString()||

> 11 isPrototypeOf()

|使用方法|结果|
|:---|:---|
|varName.valueOf()||

> 12 setPrototypeOf()

|使用方法|结果|
|:---|:---|
|varName[0]||

> 13 unwatch()

|使用方法|结果|
|:---|:---|
|varName.toSource()||

> 14 watch()

|使用方法|结果|
|:---|:---|
|varName[0]||

> 15 propertyIsEnumerable()

|使用方法|结果|
|:---|:---|
|varName.toSource()||

# 6. 字符串字面量的原型方法

## 6.1 概述

|方法名|描述|参数|
|:---|:---|:---|
|raw()|  一个模板字符串的标签函数，它的作用类似于 Python 中的字符串前缀 r 和 C# 中的字符串前缀 @，是用来获取一个模板字符串的原始字面量值的。|@param1 callSite 一个模板字符串的`调用点对象`。@param2 ...substitutions 任意个可选的参数，表示任意个内插表达式对应的值。|

## 6.2 详细

> 1 raw()

如果第一个参数没有传入一个格式良好的调用点对象，则会抛出 TypeError 异常。

|使用方法|结果|
|:---|:---|
|objectName.raw(callSite, ...substitutions)||

# 7 总结

## 7.1 返回值为`string`的方法

|方法名|描述|参数|
|:---|:---|:---|
|big()|  `不推荐使用`，把字符串显示为大号字体，只在页面中才会有大两个字体号效果。|无|
|small()| `不推荐使用`， 把字符串显示为小号字体，只在页面中才会有小两个字体号效果。|无|
|blink()| `不推荐使用`， 把字符串显示闪动的字符串，目前没有看到有浏览器支持|无|
|bold()| `不推荐使用`， 把字符串显示粗体的字符串，只在页面中才会有粗体效果，IE不兼容。|无|
|italics()| `不推荐使用`，把字符串显示为斜体，只在页面中才会有效果。|无|
|strike()| `不推荐使用`， 把字符串显示为加了删除线的字符串，只在页面中才会有效果。|无|
|fixed()| `不推荐使用`， 把字符串显示为打字机文本显示的字符串，只在页面中才会有效果。|无|
|sub()|  `不推荐使用`，把字符串显示为下标，只在页面中才会有效果。|无|
|sup()| `不推荐使用`， 把字符串显示为上标，只在页面中才会有效果。|无|
|anchor(anchorname)|  `不推荐使用`，创建 `HTML` 锚。将字符串输出为有唯一标识的纯粹`a`标签，只在页面中才会有效果。| @para anchorname 必需，为锚定义名称。如果没有传入参数，则会输出一个`name`属性为`undefined`的`a`标签。|
|link(url)| `不推荐使用`， 把字符串显示为链接，只在页面中才会有效果。如果没有传入参数，则会输出一个href属性为`undefined`的a标签。| @para url必需，规定要链接的 URL。|
|fontcolor(color)| `不推荐使用`，返回指定的颜色的字符串。只在页面中才会有效果如果没有传入参数，则会输出一个`color`属性为`undefined`的font标签。| @para  color必需。为字符串规定 font-color。该值必须是颜色名(red)、RGB 值(rgb(255,0,0))或者十六进制数(#FF0000)。|
|fontsize(size)| `不推荐使用`， 返回指定的字体大小的字符串。只在页面中才会有效果。如果没有传入参数，则会输出一个`size`属性为`undefined`的`font`标签。|  @para size 参数必须是从 1 至 7 的数字，数字越大字体越大。|
|charAt(index)|  返回特定位置的字符，不提供参数就返回第一个字符的字符，提供游标值，就返回指定游标的字符| @para index 非必需，一个介于0 和字符串长度减1之间的正整数。 (0~varName.length-1)。|

## 7.2 返回值为`int`的方法

|方法名|描述|参数|
|:---|:---|:---|
|charCodeAt(index)| 返回0到65535之间的整数，表示给定索引处的`UTF-16`代码单元 (在 `Unicode` 编码单元表示一个单一的 `UTF-16` 编码单元的情况下，`UTF-16` 编码单元匹配 `Unicode` 编码单元。但在——例如 `Unicode` 编码单元 > `0x10000` 的这种——不能被一个 `UTF-16` 编码单元单独表示的情况下，只能匹配 `Unicode` 代理对的第一个编码单元) 。|@para index 一个大于等于 0，小于字符串长度的整数。(0~varName.length-1)，如果不是一个数值，则默认为 0。|

# 8 参考网站

- [MDN-String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)

- [MDN-模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings)

- [MDN-String-prototype](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/prototype)

- [Unicode字符平面映射](https://zh.wikipedia.org/wiki/Unicode%E5%AD%97%E7%AC%A6%E5%B9%B3%E9%9D%A2%E6%98%A0%E5%B0%84#.E5.9F.BA.E6.9C.AC.E5.A4.9A.E6.96.87.E7.A7.8D.E5.B9.B3.E9.9D.A2)

- [ASCII码查询](http://www.asciima.com/)
