---
title: 西瓜有话说之js对象学习强制类型转换篇
category: js_thinking
tags:
  - instanceof
  - watermelon
  - 强制类型转换  
  - js_thinking
date: 2017-10-22 00:00:00
---
# 1 js中强制类型转换

在 JavaScript 中，大多数事物都是对象, 从作为核心功能的字符串和数组，到建立在 JavaScript 之上的浏览器 API。今天主要是学习六大基本对象数据类型之间的强制类型转化，将其他类型的对象实例转化成规定的`数据对象类型。

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

  var ooo = Object(oo);
  var ooString = Object(oString);
  var ooBool = Object(oBool);
  var ooNum = Object(oNum);
  var ooArray = Object(oArray);
  var ooDate = Object(oDate);

  var soo = String(oo);
  var soString = String(oString);
  var soBool = String(oBool);
  var soNum = String(oNum);
  var soArray = String(oArray);
  var soDate = String(oDate);

  var boo = Boolean(oo);
  var boString = Boolean(oString);
  var boBool = Boolean(oBool);
  var boNum = Boolean(oNum);
  var boArray = Boolean(oArray);
  var boDate = Boolean(oDate);

  var noo = Number(oo);
  var noString = Number(oString);
  var noBool = Number(oBool);
  var noNum = Number(oNum);
  var noArray = Number(oArray);
  var noDate = Number(oDate);

  var aoo = Array(oo);
  var aoString = Array(oString);
  var aoBool = Array(oBool);
  var aoNum = Array(oNum);
  var aoArray = Array(oArray);
  var aoDate = Array(oDate);

  var doo = Date(oo);
  var doString = Date(oString);
  var doBool = Date(oBool);
  var doNum = Date(oNum);
  var doArray = Date(oArray);
  var doDate = Date(oDate);

  function demoo(){}
```

|变量名|含义|举例|
|:---|:---|:---|
|objectName| 相关对象类型名称 |就像上面`js`代码中`Object`,`Boolean`,`Number`,`String`,`Array`,`Date`|
|varName| 相关对象类型实例化后的变量名 |就像上面`js`代码中`oo`,`oBool`,`oNum`,`oString`,`oArray`,`oDate`|
|param1,param2,param3,...,paramN|函数中需要传入第一个到第N个的参数值 |就像上面`js`代码中`true`,`68`,`hello world`|
|functionName|函数名称|就像上文的`demoo`|

# 3 varName转换前的信息

## 3.1  打印原本相关数据

> 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|oo| {}|oo.constructor|
|oBool| [Boolean: true] |oBool.constructor|
|oNum| [Number: 68] |oNum.constructor|
|oString| [String: 'hello world'] |oString.constructor|
|oArray| [ 'demo', 'melon', 'water' ] |oArray.constructor|
|oDate| 2017-11-18T14:01:15.443Z |oDate.constructor|

> constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|oo| [Function: Object] |oo.constructor|
|oBool| [Function: Boolean] |oBool.constructor|
|oNum| [Function: Number] |oNum.constructor|
|oString| [Function: String] |oString.constructor|
|oArray| [Function: Array] |oArray.constructor|
|oDate| [Function: Date] |oDate.constructor|

> __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|oo| {} |`oo.__proto__`|
|oBool| [Boolean: false] |`oBool.__proto__`|
|oNumber| [Number: 0] |`oNum.__proto__`|
|oString| [String: ''] |`oString.__proto__`|
|oArray| [] |`oArray.__proto__`|
|oDate| Date {} |`oDate.__proto__`|

> 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| true |oo instanceof Object |
|oBool| true |oBool instanceof Object |
|oNumber| true |oNum instanceof Object |
|oString| true |oString instanceof Object |
|oArray| true |oArray instanceof Object |
|oDate| true |oDate instanceof Object |

> 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| false |oo instanceof String |
|oBool| false |oBool instanceof String |
|oNumber| false |oNum instanceof String |
|oString| true |oString instanceof String |
|oArray| false |oArray instanceof String |
|oDate| false |oDate instanceof String |

> 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| false |oo instanceof Boolean |
|oBool| true |oBool instanceof Boolean |
|oNumber| false |oNum instanceof Boolean |
|oString| false |oString instanceof Boolean |
|oArray| false |oArray instanceof Boolean |
|oDate| false |oDate instanceof Boolean |

> 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| false |oo instanceof Number |
|oBool| false |oBool instanceof Number |
|oNumber| true |oNum instanceof Number |
|oString| false |oString instanceof Number |
|oArray| false |oArray instanceof Number |
|oDate| false |oDate instanceof Number |

> 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| false |oo instanceof Array |
|oBool| false |oBool instanceof Array |
|oNumber| false |oNum instanceof Array |
|oString| false |oString instanceof Array |
|oArray| true |oArray instanceof Array |
|oDate| false |oDate instanceof Array |

> 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|oo| false |oo instanceof Date |
|oBool| false |oBool instanceof Date |
|oNumber| false |oNum instanceof Date |
|oString| false |oString instanceof Date |
|oArray| false |oArray instanceof Date |
|oDate| true |oDate instanceof Date |

## 3.2  强制类型转换列表

|方法名|解释|使用方法|
|:---|:---|:---|
|Object|将其他类型的对象转换成Object类型对象 |Object(varName)|
|String| 将其他类型的对象转换成String类型对象 |String(varName)|
|Boolean| 将其他类型的对象转换成Boolean类型对象 |Boolean(varName)|
|Number| 将其他类型的对象转换成Number类型对象 |Number(varName)|
|Array| 将其他类型的对象转换成Array类型对象 |Array(varName)|
|Date| 将其他类型的对象转换成Date类型对象 |Date(varName)|

## 3.3 instanceof用法

> 语法

```Javascript
object instanceof constructor
```

> 参数

- @param1 object 要检测的对象.
- @param2 constructor 某个构造函数

> 描述

`instanceof` 运算符用来检测 `constructor.prototype` 是否存在于参数 `object` 的`原型链`上。

> 注意事项

- 请注意方法接受传入的构造体包括六个数据对象类型名，还有函数方法名，如果传入其他则会报错，比如如果传入`varName`，会报错`Expecting a function in instanceof check, but got #<C>`。
- 五大基本数据类型（null，undefined，String，Number，Boolean），即隐式声明变量，没有通过`new`关键字或者`强制类型转换`的变量，默认的`原型链`是未定义的
- 通过`new`关键词实例化`functionName`的时候，使用`instanceof`检测是否包含`object`原型链会返回`true`。
- `objectName instanceof functionName`的值为`false`，不代表`functionName instanceof objectName`的值也为`false`
- 存在父子关系的两个对象或者函数，实例化子对象或着子方法之后，在没有修改父级和子级的原型链前提下，使用`instanceof`检测子级或者父级的对象或者方法的时候，都会返回`true`。
- 需要注意的是，如果表达式 `varName instanceof functionName` 返回`true`，则并不意味着该表达式会永远返回`true`。
- 因为`functionName.prototype`属性的值有可能会改变，改变之后的值很有可能不存在于`varName`的原型链上，这时原表达式的值就会成为`false`。
- 另外一种情况下，原表达式的值也会改变，就是改变对象`varName`的`原型链`的情况，虽然在目前的`ES规范`中，我们只能读取对象的`原型`而不能改变它，但借助于非标准的`__proto__`魔法属性，是可以实现的，比如执行`varName.__proto__ = {}`之后，`varName instanceof functionName`就会返回`false`了。

# 4 强制转换结果

## 4.1 Object强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|ooo| {}|ooo.constructor|
|ooBool| [Boolean: true] |ooBool.constructor|
|ooNum| [Number: 68] |ooNum.constructor|
|ooString| [String: 'hello world'] |ooString.constructor|
|ooArray| [ 'demo', 'melon', 'water' ] |ooArray.constructor|
|ooDate| 2017-11-18T14:01:15.443Z |ooDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|ooo| [Function: Object] |ooo.constructor|
|ooBool| [Function: Boolean] |ooBool.constructor|
|ooNum| [Function: Number] |ooNum.constructor|
|ooString| [Function: String] |ooString.constructor|
|ooArray| [Function: Array] |ooArray.constructor|
|ooDate| [Function: Date] |ooDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|ooo| {} |`ooo.__proto__`|
|ooBool| [Boolean: false] |`ooBool.__proto__`|
|ooNumber| [Number: 0] |`ooNum.__proto__`|
|ooString| [String: ''] |`ooString.__proto__`|
|ooArray| [] |`ooArray.__proto__`|
|ooDate| Date {} |`ooDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| true |ooo instanceof Object |
|ooBool| true |ooBool instanceof Object |
|ooNumber| true |ooNum instanceof Object |
|ooString| true |ooString instanceof Object |
|ooArray| true |ooArray instanceof Object |
|ooDate| true |ooDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| false |ooo instanceof String |
|ooBool| false |ooBool instanceof String |
|ooNumber| false |ooNum instanceof String |
|ooString| true |ooString instanceof String |
|ooArray| false |ooArray instanceof String |
|ooDate| false |ooDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| false |ooo instanceof Boolean |
|ooBool| true |ooBool instanceof Boolean |
|ooNumber| false |ooNum instanceof Boolean |
|ooString| false |ooString instanceof Boolean |
|ooArray| false |ooArray instanceof Boolean |
|ooDate| false |ooDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| false |ooo instanceof Number |
|ooBool| false |ooBool instanceof Number |
|ooNumber| true |ooNum instanceof Number |
|ooString| false |ooString instanceof Number |
|ooArray| false |ooArray instanceof Number |
|ooDate| false |ooDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| false |ooo instanceof Array |
|ooBool| false |ooBool instanceof Array |
|ooNumber| false |ooNum instanceof Array |
|ooString| false |ooString instanceof Array |
|ooArray| true |ooArray instanceof Array |
|ooDate| false |ooDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|ooo| false |ooo instanceof Date |
|ooBool| false |ooBool instanceof Date |
|ooNumber| false |ooNum instanceof Date |
|ooString| false |ooString instanceof Date |
|ooArray| false |ooArray instanceof Date |
|ooDate| true |ooDate instanceof Date |

## 4.2 String强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|soo| [object Object]|soo.constructor|
|soBool| true |soBool.constructor|
|soNum| 68 |soNum.constructor|
|soString| hello world |soString.constructor|
|soArray| demo,melon,water |soArray.constructor|
|soDate| Sat Nov 18 2017 22:01:15 GMT+0800 (CST) |soDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|soo| [Function: String] |soo.constructor|
|soBool| [Function: String] |soBool.constructor|
|soNum| [Function: String] |soNum.constructor|
|soString| [Function: String] |soString.constructor|
|soArray| [Function: String] |soArray.constructor|
|soDate| [Function: String] |soDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|soo| [String: ''] |`soo.__proto__`|
|soBool| [String: ''] |`soBool.__proto__`|
|soNumber| [String: ''] |`soNum.__proto__`|
|soString| [String: ''] |`soString.__proto__`|
|soArray| [String: ''] |`soArray.__proto__`|
|soDate| [String: ''] |`soDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof Object |
|soBool| false |soBool instanceof Object |
|soNumber| false |soNum instanceof Object |
|soString| false |soString instanceof Object |
|soArray| false |soArray instanceof Object |
|soDate| false |soDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof String |
|soBool| false |soBool instanceof String |
|soNumber| false |soNum instanceof String |
|soString| false |soString instanceof String |
|soArray| false |soArray instanceof String |
|soDate| false |soDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof Boolean |
|soBool| false |soBool instanceof Boolean |
|soNumber| false |soNum instanceof Boolean |
|soString| false |soString instanceof Boolean |
|soArray| false |soArray instanceof Boolean |
|soDate| false |soDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof Number |
|soBool| false |soBool instanceof Number |
|soNumber| false |soNum instanceof Number |
|soString| false |soString instanceof Number |
|soArray| false |soArray instanceof Number |
|soDate| false |soDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof Array |
|soBool| false |soBool instanceof Array |
|soNumber| false |soNum instanceof Array |
|soString| false |soString instanceof Array |
|soArray| false |soArray instanceof Array |
|soDate| false |soDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|soo| false |soo instanceof Date |
|soBool| false |soBool instanceof Date |
|soNumber| false |soNum instanceof Date |
|soString| false |soString instanceof Date |
|soArray| false |soArray instanceof Date |
|soDate| false |soDate instanceof Date |

## 4.3 Boolean强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|boo| true|boo.constructor|
|boBool| true |boBool.constructor|
|boNum| true |boNum.constructor|
|boString| true |boString.constructor|
|boArray| true |boArray.constructor|
|boDate| true |boDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|boo| [Function: Boolean] |boo.constructor|
|boBool| [Function: Boolean] |boBool.constructor|
|boNum| [Function: Boolean] |boNum.constructor|
|boString| [Function: Boolean] |boString.constructor|
|boArray| [Function: Boolean] |boArray.constructor|
|boDate| [Function: Boolean] |boDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|boo| [Boolean: false] |`boo.__proto__`|
|boBool| [Boolean: false] |`boBool.__proto__`|
|boNumber| [Boolean: false] |`boNum.__proto__`|
|boString| [Boolean: false] |`bobString.__proto__`|
|boArray| [Boolean: false] |`boArray.__proto__`|
|boDate| [Boolean: false] |`boDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof Object |
|boBool| false |boBool instanceof Object |
|boNumber| false |boNum instanceof Object |
|boString| false |boString instanceof Object |
|boArray| false |boArray instanceof Object |
|boDate| false |boDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof String |
|boBool| false |boBool instanceof String |
|boNumber| false |boNum instanceof String |
|boString| false |boString instanceof String |
|boArray| false |boArray instanceof String |
|boDate| false |boDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof Boolean |
|boBool| false |boBool instanceof Boolean |
|boNumber| false |boNum instanceof Boolean |
|boString| false |boString instanceof Boolean |
|boArray| false |boArray instanceof Boolean |
|boDate| false |boDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof Number |
|boBool| false |boBool instanceof Number |
|boNumber| false |boNum instanceof Number |
|boString| false |boString instanceof Number |
|boArray| false |boArray instanceof Number |
|boDate| false |boDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof Array |
|boBool| false |boBool instanceof Array |
|boNumber| false |boNum instanceof Array |
|boString| false |obString instanceof Array |
|boArray| false |boArray instanceof Array |
|boDate| false |boDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|boo| false |boo instanceof Date |
|boBool| false |boBool instanceof Date |
|boNumber| false |boNum instanceof Date |
|boString| false |boString instanceof Date |
|boArray| false |boArray instanceof Date |
|boDate| false |boDate instanceof Date |

## 4.4 Number强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|noo| NaN|noo.constructor|
|noBool| 1 |noBool.constructor|
|noNum| 68 |noNum.constructor|
|noString| NaN |noString.constructor|
|noArray| NaN |noArray.constructor|
|noDate| 1511022672428 |noDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|noo| [Function: Number] |noo.constructor|
|noBool| [Function: Number] |noBool.constructor|
|noNum| [Function: Number] |noNum.constructor|
|noString| [Function: Number] |noString.constructor|
|noArray| [Function: Number] |noArray.constructor|
|noDate| [Function: Number] |noDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|noo| [Number: 0] |`noo.__proto__`|
|noBool| [Number: 0] |`noBool.__proto__`|
|noNumber| [Number: 0] |`noNum.__proto__`|
|noString| [Number: 0] |`noString.__proto__`|
|noArray| [Number: 0] |`noArray.__proto__`|
|noDate| [Number: 0] |`noDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof Object |
|noBool| false |noBool instanceof Object |
|noNumber| false |noNum instanceof Object |
|noString| false |noString instanceof Object |
|noArray| false |noArray instanceof Object |
|noDate| false |noDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof String |
|noBool| false |noBool instanceof String |
|noNumber| false |noNum instanceof String |
|noString| false |noString instanceof String |
|noArray| false |noArray instanceof String |
|noDate| false |noDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof Boolean |
|noBool| false |noBool instanceof Boolean |
|noNumber| false |noNum instanceof Boolean |
|noString| false |noString instanceof Boolean |
|noArray| false |noArray instanceof Boolean |
|noDate| false |noDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof Number |
|noBool| false |noBool instanceof Number |
|noNumber| false |noNum instanceof Number |
|noString| false |noString instanceof Number |
|noArray| false |noArray instanceof Number |
|noDate| false |noDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof Array |
|noBool| false |noBool instanceof Array |
|noNumber| false |noNum instanceof Array |
|noString| false |noString instanceof Array |
|noArray| false |noArray instanceof Array |
|noDate| false |noDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|noo| false |noo instanceof Date |
|noBool| false |noBool instanceof Date |
|noNumber| false |noNum instanceof Date |
|noString| false |noString instanceof Date |
|noArray| false |noArray instanceof Date |
|noDate| false |noDate instanceof Date |

## 4.5 Array强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|aoo| [ {} ]|aoo.constructor|
|aoBool| [ [Boolean: true] ] |aoBool.constructor|
|aoNum| [ [Number: 68] ] |aoNum.constructor|
|aoString| [ [String: 'hello world'] ] |aoString.constructor|
|aoArray| [ [ 'demo', 'melon', 'water' ] ] |aoArray.constructor|
|aoDate| [ 2017-11-18T16:35:16.315Z ] |aoDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|aoo| [Function: Array] |aoo.constructor|
|aoBool| [Function: Array] |aoBool.constructor|
|aoNum| [Function: Array] |aoNum.constructor|
|aoString| [Function: Array] |aoString.constructor|
|aoArray| [Function: Array] |aoArray.constructor|
|aoDate| [Function: Array] |aoDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|aoo| [] |`aoo.__proto__`|
|aoBool| [] |`aoBool.__proto__`|
|aoNumber| []|`aoNum.__proto__`|
|aoString| [] |`aoString.__proto__`|
|aoArray| [] |`aoArray.__proto__`|
|aoDate| [] |`aoDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| true |aoo instanceof Object |
|aoBool| true |aoBool instanceof Object |
|aoNumber| true |aoNum instanceof Object |
|aoString| true |aoString instanceof Object |
|aoArray| true |aoArray instanceof Object |
|aoDate| true |aoDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| false |aoo instanceof String |
|aoBool| false |aoBool instanceof String |
|aoNumber| false |aoNum instanceof String |
|aoString| false |aoString instanceof String |
|aoArray| false |aoArray instanceof String |
|aoDate| false |aoDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| false |aoo instanceof Boolean |
|aoBool| false |aoBool instanceof Boolean |
|aoNumber| false |aoNum instanceof Boolean |
|aoString| false |aoString instanceof Boolean |
|aoArray| false |aoArray instanceof Boolean |
|aoDate| false |aoDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| false |aoo instanceof Number |
|aoBool| false |aoBool instanceof Number |
|aoNumber| false |aoNum instanceof Number |
|aoString| false |aoString instanceof Number |
|aoArray| false |aoArray instanceof Number |
|aoDate| false |aoDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| true |aoo instanceof Array |
|aoBool| true |aoBool instanceof Array |
|aoNumber| true |aoNum instanceof Array |
|aoString| true |aoString instanceof Array |
|aoArray| true |aoArray instanceof Array |
|aoDate| true |aoDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|aoo| false |aoo instanceof Date |
|aoBool| false |aoBool instanceof Date |
|aoNumber| false |aoNum instanceof Date |
|aoString| false |aoString instanceof Date |
|aoArray| false |aoArray instanceof Date |
|aoDate| false |aoDate instanceof Date |

## 4.6 Date强制转换

- 原始值

|实例名|原始值|使用方法|
|:---|:---|:---|
|doo| Sun Nov 19 2017 01:39:06 GMT+0800 (CST)|doo.constructor|
|doBool| Sun Nov 19 2017 01:39:06 GMT+0800 (CST) |doBool.constructor|
|doNum| Sun Nov 19 2017 01:39:06 GMT+0800 (CST) |doNum.constructor|
|doString| Sun Nov 19 2017 01:39:06 GMT+0800 (CST) |doString.constructor|
|doArray| Sun Nov 19 2017 01:39:06 GMT+0800 (CST) |doArray.constructor|
|doDate| Sun Nov 19 2017 01:39:06 GMT+0800 (CST) |doDate.constructor|

- constructor

|实例名|构造体|使用方法|
|:---|:---|:---|
|doo| [Function: String] |doo.constructor|
|doBool| [Function: String] |doBool.constructor|
|doNum| [Function: String] |doNum.constructor|
|doString| [Function: String] |doString.constructor|
|doArray| [Function: String] |doArray.constructor|
|doDate| [Function: String] |doDate.constructor|

- __proto__

|实例名|默认值|使用方法|
|:---|:---|:---|
|doo| [String: ''] |`doo.__proto__`|
|doBool| [String: ''] |`doBool.__proto__`|
|doNumber| [String: ''] |`doNum.__proto__`|
|doString| [String: ''] |`doString.__proto__`|
|doArray| [String: ''] |`doArray.__proto__`|
|doDate| [String: ''] |`doDate.__proto__`|

- 实例对象原型链中是否包含Object的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof Object |
|doBool| false |doBool instanceof Object |
|doNumber| false |doNum instanceof Object |
|doString| false |doString instanceof Object |
|doArray| false |doArray instanceof Object |
|doDate| false |doDate instanceof Object |

- 实例对象原型链中是否包含String的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof String |
|doBool| false |doBool instanceof String |
|doNumber| false |doNum instanceof String |
|doString| false |doString instanceof String |
|doArray| false |doArray instanceof String |
|doDate| false |doDate instanceof String |

- 实例对象原型链中是否包含Boolean的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof Boolean |
|doBool| false |doBool instanceof Boolean |
|doNumber| false |doNum instanceof Boolean |
|doString| false |doString instanceof Boolean |
|doArray| false |doArray instanceof Boolean |
|doDate| false |doDate instanceof Boolean |

- 实例对象原型链中是否包含Number的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof Number |
|doBool| false |doBool instanceof Number |
|doNumber| false |doNum instanceof Number |
|doString| false |doString instanceof Number |
|doArray| false |doArray instanceof Number |
|doDate| false |doDate instanceof Number |

- 实例对象原型链中是否包含Array的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof Array |
|doBool| false |doBool instanceof Array |
|doNumber| false |doNum instanceof Array |
|doString| false |doString instanceof Array |
|doArray| false |doArray instanceof Array |
|doDate| false |doDate instanceof Array |

- 实例对象原型链中是否包含Date的原型链

|实例名|属性值|使用方法|
|:---|:---|:---|
|doo| false |doo instanceof Date |
|doBool| false |doBool instanceof Date |
|doNumber| false |doNum instanceof Date |
|doString| false |doString instanceof Date |
|doArray| false |doArray instanceof Date |
|doDate| false |doDate instanceof Date |

# 5 总结

## 5.1 object 强制类型转换

- 不会所有修改对象内容
- 所有对象的`__proto__`也不会改变
- 所有对象的`构造体`也不会改变
- 所有对象的`原型链`都包含object的`原型链`
- 除此之外，所有对象的原型链判断都和非强制转换前一样，原本是什么`构造体`生成的，现在对哪个构造体`原型链`的值就为真，比如`oNumber`原本是实例化的`Number`对象，所以在判断原型链包含情况的时候，只会在判断时候包含`Number`构造体原型链的时候是`true`，对于剩下的四种构造体原型链判断，都是`false`。

## 5.2 String强制类型转换

- 所有对象的内容展示形式会有不同

  - 原本`object`的展示为`[object Object]`
  - 原本`Strin`g的展示没有变化
  - 原本`Boolean`的展示为字符串类型的boolean值
  - 原本`Number`的展示为字符串类型的Number值
  - 原本`Array`的展示为字符串类型的Array值，原数组中每个数值，都以逗号拼接起来
  - 原本`Date`的展示为默认日期类型（显示了所有时间信息并且有时区之类）

- 所有对象的`__proto__`全部变成了`[String: '']`
- 所有对象的构造体全部变成了`[Function: String]`
- 所有对象的原型链和六大数据类型的原型链都不匹配

## 5.3 Boolean强制类型转换

- 所有对象的内容都变成了true
- 所有对象的`__proto__`全部变成了`[Boolean: false]`
- 所有对象的构造体全部变成了`[Function: Boolean]`
- 所有对象的原型链和六大数据类型的原型链都不匹配

## 5.4 Number强制类型转换

- 所有对象的内容展示形式会有不同
  - 原本`object`的展示为`NaN`
  - 原本`String`的展示没有变化
  - 原本`Boolean`的展示为`1`
  - 原本`Number`的展示为`68`
  - 原本`Array`的展示为`NaN`
  - 原本`Date`的展示为`1511025092414`，不清楚这个转换规则
- 所有对象的`__proto__`全部变成了`[Number: 0]`
- 所有对象的`构造体`全部变成了`[Function: Number]`
- 所有对象的`原型链`和六大数据类型的`原型链`都不匹配

## 5.5 Array强制类型转换

- 所有对象的内容展示形式会有不同，就是在原始内容外层套了一层`中括号`，比如 原本Array的内容为`[ 'demo', 'melon', 'water' ]` ，转换之后成了`[ [ 'demo', 'melon', 'water' ] ]`

- 所有对象的`__proto__`全部变成了`[]`
- 所有对象的构造体全部变成了`[Function: Array]`
- 所有对象的原型链都包含`object`的原型链和`Array`的原型链
- 所有对象的`原型链`和剩下的四个数据类型的`原型链`都不匹配

## 5.6 Date强制类型转换

- 所有对象的内容都变成了`Sun Nov 19 2017 01:39:06 GMT+0800 (CST)`默认日期类型（显示了所有时间信息并且有时区之类）

- 所有对象的`__proto__`全部变成了`[String: '']`
- 所有对象的构造体全部变成了`[Function: String]`
- 所有对象的`原型链`和六大数据类型的`原型链`都不匹配

## 5.6 强制类型转换共同点

- 所有对象通过`Object`或`Array`类型强制转换之后，原型链上都可以找到`object`构造体原型链
- 所有对象通过`String`或`Date`类型强制转换之后，对象的`__proto__`都是`[String: '']`，对象的构造体都变成了`[Function: String]`。
- 除了`Object`和`Array`类型强制转换之外，其他强制类型转换之后，所有对象的`原型链`和六大数据类型的`原型链`都不匹配

# 6 学习源码地址

[learnInstanceof](https://mowatermelon.github.io/demoArray/basejs/learnInstanceof.js)