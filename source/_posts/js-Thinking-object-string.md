---
title: 西瓜有话说之js对象学习string篇
category: js_thinking
tags:
  - string
  - watermelon
  - js_thinking
date: 2017-10-21 00:00:00
---
# 1. 定义

> 基本字符串

字符串字面量 (通过`单引号`或`双引号`定义) 和 直接调用 `String` 方法(没有通过 `new` 生成字符串对象实例)的字符串都是`基本字符串`。`基本字符串`是没有相关扩展方法，只有将`基本字符串`可转化为`字符串对象`之后才可以使用`字符串对象`的方法，当`基本字符串`需要调用一个`字符串对象`才有的`方法`或者查询`值`的时候，`JavaScript`会自动将`基本字符串`转换为`字符串对象`，并且调用相应的`方法`或者执行`查询`。

<!-- more -->

> 字符串对象

一个用于`字符串`或一个`字符序列`的`构造函数`。`字符串`对于可以保存以文本形式表示的数据非常有用。 一些常用的`字符串`操作有：查询字符串长度，使用 `+` 和 `+=` 运算符来`构建`和`连接字符串`，使用 `indexOf` 方法检查某一`子字符串`在`父字符串`中的位置，又或是使用 `substring` 方法提取从`父字符串`中提取`子字符串`。

> 模板字符串

`模板字面量`/`Template literals` 是允许嵌入表达式的`字符串字面量`。你可以使用`多行字符串`和`字符串插值`功能。它们在`ES2015`规范的先前版本中被称为`模板字符串`/`template strings`。

`模板字符串`使用反引号 (\` \`) 来代替`普通字符串`中的用`双引号`和`单引号`。`模板字符串`可以包含特定语法(`${expression}`)的`占位符`。`占位符`中的`表达式`和周围的`文本`会一起传递给一个`默认函数`，该函数负责将所有的部分连接起来，如果一个模板字符串由`表达式`开头，则该字符串被称为`带标签`的`模板字符串`，该表达式通常是一个`函数`，它会在模板字符串处理后被调用，在输出最终结果前，你都可以通过该`函数`来对模板字符串进行操作处理。在`模版字符串`内使用`反引号`（`）时，需要在它前面加`转义符`（\）。

```javascript
`\`` === "`" // --> true
```

# 2. 名词字典

> 本文中出现变量名词的解释

```javascript
    var a = 4;
    var b = 8;
    var strString = "hello watermelon";
    var oString = new String("hello world");
    var tString_1 =`hello Template`;
    var tString_2 =`hello Template line 1
                    hello Template line 2`;
    //`string text ${expression} string text`  在模版字符串中使用表达式
    var tString_3 =`Fifteen is ${a + b} and\nnot ${2 * a + b}.`;

    //tag `string text ${expression} string text`  在模版字符串中使用tag方法
    var tString_4 = tag`Hello ${ a + b } world ${ a * b}`;
    function tag(strings, ...values) {
      console.log(strings[0]); // "Hello "
      console.log(strings[1]); // " world "
      console.log(strings[2]); // ""
      console.log(values[0]);  // 15
      console.log(values[1]);  // 50

      return "大吉大利今晚吃西瓜!";
    }
```

|变量名|含义|举例|
|:---|:---|:---|
|objectName| 相关对象类型名称 |就像上面`js`代码中`String`|
|varName| 相关对象类型实例化后的变量名 |就像上面`js`代码中`strString`,`oString`,`tString_1`,`tString_2`,`tString_3`,`tString_4`|
|letter|字母|letter(8) 代表八个子母，一个字母长度为一|
|char|汉字|char(8) 代表八个汉字，一个汉字长度为一|
|num|数字|num(8) 代表八个数字，一个数字长度为一|
|sign|符号|sign(8) 代表八个符号，一个符号长度为一|
|\s|空格符|\s(8) 代表八个空格符，一个空格符长度为一|
|\t|缩进符|\t(8) 代表八个缩进符，一个缩进符长度为四|
|\n|换行符|\n(8) 代表八个换行符，一个换行符长度为一|
|param1,param2,param3,...,paramN|函数中需要传入第一个到第N个的参数值 |就像上面`js`代码中`hello watermelon`,`hello world`,`hello Template`|
|柔和方法|不会改变字符串原始值|就是执行某个方法之后，`varName`原本所包含的内容不会变化|
|强硬方法|会改变字符串原始值|就是执行某个方法之后，`varName`原本所包含的内容会变化|
|父字符串|原始的对象内容|就像上面`js`代码中`strString`,`oString`,`tString_1`,`tString_2`,`tString_3`,`tString_4`|
|子字符串|传入需要检索或者替换的参数值|就像上面`js`代码中`hello watermelon`,`hello world`,`hello Template`|

# 3. 字符串的原生属性

|特性名称| 是否可修改|
|:---|:---|
|writable|false|
|enumerable|false|
|configurable|false|

|属性名|描述|使用方法|
|:---|:---|:---|
|constructor| 对创建对象的函数的引用（指针）。|varName.constructor|
|proto|对象具有属性`__proto__`，可称为隐式原型，一个对象的隐式原型指向构造该对象的构造函数的原型。|`varName.__proto__`|
|length|字符串的长度。|varName.length|

> constructor

|变量名|调取方式|属性值|
|:---|:---|:---|
|strString| strString.constructor |[Function: String]|
|oString| oString.constructor |[Function: String]|
|`tString_1`| tString_1.constructor |[Function: String]|
|`tString_2`| tString_2.constructor |[Function: String]|
|`tString_3`| tString_3.constructor |[Function: String]|
|`tString_4`| tString_4.constructor |[Function: String]|

> __proto__

|变量名|调取方式|属性值|
|:---|:---|:---|
|strString| `strString.__proto__` |[String: '']|
|oString| `oString.__proto__` |[String: '']|
|`tString_1`| `tString_1.__proto__` |[String: '']|
|`tString_2`| `tString_2.__proto__` |[String: '']|
|`tString_3`| `tString_3.__proto__` |[String: '']|
|`tString_4`| `tString_4.__proto__` |[String: '']|

> length

|变量名|调取方式|属性值|解释|
|:---|:---|:---|:---|
|strString| strString.length |16|letter(15)+\s(1)|
|oString| oString.length |11|letter(10)+\s(1)|
|`tString_1`| tString_1.length |14|letter(13)+\s(1)|
|`tString_2`| tString_2.length |41|letter(18)+num(2)+\s(4)+\t(4)+\n(1)|
|`tString_3`| tString_3.length |25|letter(15)+num(4)+\s(4)+sign(1)+\n(1)|
|`tString_4`| tString_4.length |10|char(9)+sign(1)|

# 4. 字符串的柔和方法

## 4.1. 强制类型转化

|方法名|描述|使用方法|
|:---|:---|:---|
|String|强制类型转化，将其他类型的变量转化成`String`类型|String(varName)|

## 4.2. HTML相关方法

|方法名|描述|参数|使用方法|
|:---|:---|:---|:---|
|big()| 把字符串显示为大号字体，只在页面中才会有大两个字体号效果。|无|varName.big()|
|small()| 把字符串显示为小号字体，只在页面中才会有小两个字体号效果。|无|varName.small()|
|blink()| 把字符串显示闪动的字符串，目前没有看到有浏览器支持|无|varName.blink()|
|bold()| 把字符串显示粗体的字符串，只在页面中才会有粗体效果，IE不兼容。|无|varName.bold()|
|italics()|把字符串显示为斜体。只在页面中才会有效果。|无|varName.italics()|
|strike()| 把字符串显示为加了删除线的字符串。只在页面中才会有效果。|无|varName.strike()|
|sub()| 把字符串显示为下标。只在页面中才会有效果。|无|varName.sub()|
|sup()| 把字符串显示为上标。只在页面中才会有效果。|无|varName.sup()|
|anchor(anchorname)| 创建 `HTML` 锚。将字符串输出为有唯一标识的纯粹`a`标签，只在页面中才会有效果。| @para anchorname 必需，为锚定义名称。如果没有传入参数，则会输出一个`name`属性为`undefined`的`a`标签。|varName.anchor(param1)|
|link(url)| 把字符串显示为链接，只在页面中才会有效果。如果没有传入参数，则会输出一个href属性为`undefined`的a标签。| @para url	必需，规定要链接的 URL。|varName.link(param1)|
|fontcolor(color)| 返回指定的颜色的字符串。只在页面中才会有效果如果没有传入参数，则会输出一个`color`属性为`undefined`的font标签。| @para  color	必需。为字符串规定 font-color。该值必须是颜色名(red)、RGB 值(rgb(255,0,0))或者十六进制数(#FF0000)。|varName.fontcolor(param1)|
|fontsize(size)| 返回指定的字体大小的字符串。只在页面中才会有效果。如果没有传入参数，则会输出一个`size`属性为`undefined`的`font`标签。|  @para size 参数必须是从 1 至 7 的数字，数字越大字体越大。|varName.fontsize(param1)|

## 4.3. 数据比较相关方法

# 5. 字符串的强硬方法

|方法名|描述|使用方法|
|:---|:---|:---|
|slice| 返回对应字符串或者数组中下标从param1到param2的的元素|varName.slice(param1,param2)|

6 参考网站

- [MDN-String](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)

- [MDN-模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/template_strings)

- [MDN-String-prototype](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/prototype)
