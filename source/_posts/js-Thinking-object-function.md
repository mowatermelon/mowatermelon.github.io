---
title: 西瓜有话说之js学习object方法总结
category: js_thinking
tags:
  - function
  - object  
  - watermelon
  - js_thinking
date: 2017-10-26 00:00:00
---
# 1 String

String引用类型方法速览表

<!-- more -->

## 1.1 柔和方法

|方法分类|含义|方法名|
|:---|:---|:---|
|编码| 返回字符串内容中对应位置的值或者编码单元 |charAt(index),charCodeAt(index),codePointAt(pos),normalize([form]),fromCharCode(num1, ..., numN),fromCodePoint(num1, …, numN)|
|检索| 将字符串中内容进行检索返回对应结果 |includes(),endsWith(),indexOf(),lastIndexOf(),startsWith()|
|比较| 将字符串中的内容进行比较返回对应值 |localeCompare(),match()|
|拼接| 将字符串和其他内容进行拼接 |concat(),padEnd(),padStart()|
|大小写转换| 将字符串中的字母进行大小写转换 |toLowerCase(),toLocaleLowerCase(),toUpperCase(),toLocaleUpperCase()|
|HTML相关方法| 将字符串转成对应的Dom内容 |big(),small(),blink(),bold(),italics(),strike(),fixed(),sub(),sup(),anchor(anchorname),link(url),fontcolor(color),fontsize(size)|

## 1.2 强硬方法

|方法分类|含义|方法名|
|:---|:---|:---|
|替换| 相关对象类型名称 |replace(),search()|
|分割| 相关对象类型名称 |slice(),split(),substr(),substring()|
|格式转化| 相关对象类型名称 |trim(),trimLeft(),trimRight()|
|对象通用方法| 相关对象类型名称 |valueOf(),hasOwnProperty(),isPrototypeOf(),setPrototypeOf(),unwatch(),watch(),propertyIsEnumerable()|

# 2 Array

Array引用类型方法速览表

# 3 Date

Date引用类型方法速览表

# 4 Number

Number引用类型方法速览表

# 5 Boolean

Boolean引用类型方法速览表
