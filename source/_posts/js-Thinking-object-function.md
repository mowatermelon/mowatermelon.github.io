---
title: 西瓜有话说之js学习object方法总结
category: js_thinking
tags:
  - function
  - object  
  - watermelon
  - js_thinking
date: 2017-10-27 00:00:00
---
# 1 String

String引用类型方法速览表

<!-- more -->

## 1.1 柔和方法

|方法分类|含义|方法名|
|:---|:---|:---|
|编码| 返回字符串内容中对应位置的值或者编码单元 | - charAt(index) - charCodeAt(index) - codePointAt(pos) - normalize([form]) - fromCharCode(num1, ..., numN) - fromCodePoint(num1, …, numN)|
|检索| 将字符串中内容进行检索返回对应结果 | - indexOf(searchValue[, fromIndex]) - lastIndexOf(searchValue[, fromIndex]) - search(regexp) - includes(searchString[, position]) - startsWith(searchString [, position]) - endsWith(searchString [, position]) - match(regexp)|
|对比| 返回一个数字，表示是否引用字符串在排序中位于比较字符串的前面，后面，或者二者相同。 |localeCompare(stringExp[, locales][, options])|
|拼接| 将字符串和其他内容进行拼接 | - concat() - padEnd() - padStart()|
|大小写转换| 将字符串中的字母进行大小写转换 | - toLowerCase() - toLocaleLowerCase() - toUpperCase() - toLocaleUpperCase()|
|HTML相关方法| 将字符串转成对应的Dom内容 | - big() - small() - blink() - bold() - italics() - strike() - fixed() - sub() - sup() - anchor(anchorname) - link(url) - fontcolor(color) - fontsize(size)|

## 1.2 强硬方法

|方法分类|含义|方法名|
|:---|:---|:---|
|替换| 相关对象类型名称 |replace()|
|分割| 相关对象类型名称 | - slice() - split() - substr() - substring()|
|格式转化| 相关对象类型名称 | - trim() - trimLeft() - trimRight()|
|对象通用方法| 相关对象类型名称 | - valueOf() - hasOwnProperty() - isPrototypeOf() - setPrototypeOf() - unwatch() - watch() - propertyIsEnumerable()|

## 1.3 相似函数

### 1.3.1 编码

> 将BMP字符进行转码

- charCodeAt(index)
- fromCharCode(num1, ..., numN)

> 能够将非BMP字符也可以进行转码

- codePointAt(pos)
- normalize([form])
- fromCodePoint(num1, …, numN)

### 1.3.2 正则相关

- search(regexp)
- match(regexp)
- replace(regexp,str)
- split(regexp)

### 1.3.3 检索包含

> 与正则无关的，可以指定检测位置的

- indexOf(searchValue[, fromIndex])，返回值为`int数字`或者`-1`。
- lastIndexOf(searchValue[, fromIndex])，返回值为`int数字`或者`-1`。
- includes(searchString[, position])，返回值为`true`或者`false`。

> 只检测首尾匹配包含，不可以指定检测位置的

- startsWith(searchString [, position])，返回值为`true`或者`false`。
- endsWith(searchString [, position])，返回值为`true`或者`false`。

> 与正则有关的

- search(regexp)，返回值为`int数字`或者`-1`。
- match(regexp)，返回值为`字符串`或者`null`。

### 1.3.4 数据拼接

- 赋值操作符（+, +=），`string1 += string2+ string2 + string3`，运算速度是concat的二十倍左右，是join的两百七十倍左右。
- str.concat(string2, string3[, ..., stringN])，运算速度是join的十倍左右。
- arr.join(separator)。

# 2 Array

Array引用类型方法速览表

# 3 Date

Date引用类型方法速览表

# 4 Number

Number引用类型方法速览表

# 5 Boolean

Boolean引用类型方法速览表
