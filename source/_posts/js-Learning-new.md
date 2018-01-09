---
title: js学习之new
category: js学习
tags:
  - prototype
  - __proto__
  - new  
  - js学习
date: 2017-11-02 00:00:00
---

> 一直不清楚显式声明和隐式原型的关系，整理了一下相关疑惑，并且整理了`new`和`instanceof`关于显式声明和隐式声明的相关知识

<!--more-->

# 1 概念

## 1.1 显式原型

prototype --- 显式原型 (explicit prototype property)，每一个`函数`在创建之后都会拥有一个名为`prototype`的属性，这个属性指向`函数`的`原型对象`。

请注意通过`Function.prototype.bind`方法构造出来的函数是个例外，它没有`prototype`属性。

> NOTE Function objects created using Function.prototype.bind do not have a prototype property or the [[Code]], [[FormalParameters]], and [[Scope]] internal properties. ----- ECMAScript Language Specification

这个属性是一个`指针`，指向一个`对象`，它是显示修改对象的原型的属性。

## 1.2 隐式原型

`__proto__` --- 隐式原型 (implicit prototype link)：JS中任意`对象`都有一个内置属性`[[prototype]]`，是JS内部使用寻找原型链的属性在`ES5`之前没有标准的方法访问这个`内置属性`，但是大多数浏览器都支持通过`__proto__`来访问。

`ES5`中有了对于这个`内置属性`标准的`Get`方法`Object.getPrototypeOf()`，即`Object.getPrototypeOf(obj)===obj.__proto__`，用`chrome`和`FF`都可以访问到对象的`__proto__`属性，`IE`不可以。

隐式原型指向创建这个对象的函数(`constructor`)的`prototype`。

但是请注意`Object.prototype.__proto__ //null`，即`Object`对象的显式原型的隐式原型是`null`，这个属于特例。

根据`ECMA`定义 `to the value of its constructor’s "prototype"`，指向创建这个对象的`函数`的`显式原型`。

所以关键的点在于找到创建这个对象的`构造函数`，接下来就来看一下`JS`中对象被创建的方式，一眼看过去似乎有三种方式：

- 对象字面量的方式
- `new` 的方式
- `ES5`中的`Object.create()`

但是本质上只有一种方式，也就是通过`new`来创建。为什么这么说呢，字面量的方式只是一种为了开发人员更方便创建对象的一个`语法糖`，本质就是 `var o = new Object(); o.xx = xx;o.yy=yy;`。

`Object.create()`是`ES5`中新增的方法，在这之前这被称为`原型式继承`。其实本质依然是通过`new`来创建的，如下面栗子中其实和`new Boolean()`，效果是比较相似的。

不同之处在于由 `Object.create()` 创建出来的对象没有`构造函数`，因为`create()`接收的就是一个`内建函数`的`显式声明`，如下栗子中，创建出来的对象的隐式声明其实是指向传入的实参，即`ss.__proto__===Boolean.prototype`。

```javascript
var ss =Object.create(Boolean.prototype)

console.log(typeof ss);//object
console.log(ss.prototype);//undefined
// console.log(ss.prototype.__proto__);//Cannot read property '__proto__' of undefined
console.log(ss.__proto__);//[Boolean: false]
console.log(ss.__proto__.prototype);//undefined
console.log(ss.constructor);//[Function: Boolean]
```

# 2 作用

## 2.1 显式原型

用来实现基于原型的继承与属性的共享。

ECMAScript does not use classes such as those in C++, Smalltalk, or Java. Instead objects may be created in various ways including via a literal notation or via constructors which create objects and then execute code that initialises all or part of them by assigning initial values to their properties. Each constructor is a function that has a property named “prototype” that is used to implement prototype-based inheritance and shared properties.Objects are created by using constructors in new expressions; for example, new Date(2009,11) creates a new Date object. ----ECMAScript Language Specification

## 2.2 隐式原型

构成原型链，同样用于实现基于原型的继承。

举个例子，当我们访问obj这个对象中的`x`属性时，如果在`obj`中找不到，那么就会沿着`__proto__`依次查找。

Every object created by a constructor has an implicit reference (called the object’s prototype) to the value of its constructor’s “prototype” ----ECMAScript Language Specification

# 3 联合案例

```javascript
//新建测试变量
var temp_O = new Object();
var temp_B = new Boolean();
var temp_N = new Number();
var temp_S = new String();
var temp_A = new Array();
var temp_D = new Date();
var temp_F = new Function();

```

## 3.1 显式声明的隐式声明

除了`undefined`和`null`对象类型之外，对象的隐式声明(`__proto__`)都是`{}`，因为内建对象(built-in object)的显式声明和实例对象的显式声明都是一个对象。比如`Array.prototype`和`temp_F.prototype`都是一个对象，所以它们的隐式声明都是`{}`，指向的都是`Object`这个构造体的显示声明，即`Object.prototype`。

请注意`Object.prototype.__proto__`和`Function.prototype.__proto__`是一个特例。

| 变量 | 使用方法 | 结果 |
|:---|:---|:---|
|Object|Object.prototype|{}|
|Boolean|Boolean.prototype|[Boolean: false]|
|Number|Number.prototype|[Number: 0]|
|String|String.prototype|[String: '']|
|Array|Array.prototype|[]|
|Date|Date.prototype|Date {}|
|Function|Function.prototype|[Function]|
|Object|`Object.prototype.__proto__`|null|
|Boolean|`Boolean.prototype.__proto__`|{}|
|Number|`Number.prototype.__proto__`|{}|
|String|`String.prototype.__proto__`|{}|
|Array|`Array.prototype.__proto__`|{}|
|Date|`Date.prototype.__proto__`|{}|
|Function|`Function.prototype.__proto__`|[Function]|
|temp_O|`temp_O.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_B|`temp_B.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_N|`temp_N.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_S|`temp_S.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_A|`temp_A.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_D|`temp_D.prototype.__proto__`|Cannot read property `__proto__` of undefined|
|temp_F|`temp_F.prototype.__proto__`|{}|

## 3.2 隐式声明的显式声明

除了`undefined`和`null`对象类型之外，所有对象的显式声明(prototype)都是`undefined`，因为内建对象(built-in object)的隐式声明和实例对象的隐式声明都是一个对象。比如`Array.__proto__`和`temp_F.__proto__`都是一个对象，所以它们的显示声明都是`undefined`。

构造函数因为都是`Function()`的实例，因此构造体的隐式声明也就都指向`Function.prototype`。

| 变量 | 使用方法 | 结果 |
|:---|:---|:---|
|Object|`Object.__proto__`|[Function]|
|Boolean|`Boolean.__proto__`|[Function]|
|Number|`Number.__proto__`|[Function]|
|String|`String.__proto__`|[Function]|
|Array|`Array.__proto__`|[Function]|
|Date|`Date.__proto__`|[Function]|
|Function|`Function.__proto__`|[Function]|
|Object|`Object.__proto__.prototype`|undefined|
|Boolean|`Boolean.__proto__.prototype`|undefined|
|Number|`Number.__proto__.prototype`|undefined|
|String|`String.__proto__.prototype`|undefined|
|Array|`Array.__proto__.prototype`|undefined|
|Date|`Date.__proto__.prototype`|undefined|
|Function|`Function.__proto__.prototype`|undefined|
|temp_O|`temp_O.__proto__.prototype`|undefined|
|temp_B|`temp_B.__proto__.prototype`|undefined|
|temp_N|`temp_N.__proto__.prototype`|undefined|
|temp_S|`temp_S.__proto__.prototype`|undefined|
|temp_A|`temp_A.__proto__.prototype`|undefined|
|temp_D|`temp_D.__proto__.prototype`|undefined|
|temp_F|`temp_F.__proto__.prototype`|undefined|

# 4 new

```javascript
var Person = function(){};
var p = new Person();
```

> new的过程拆分成以下三步：

- `var p={};` 也就是说，初始化一个空对象`p`。
- `p.__proto__ = Person.prototype;` 将临时对象的`隐式声明`指向构造体的`显式声明`上。
- `Person.call(p);` 也就是说构造`p`，也可以称之为初始化`p`。

关键在于第二步，我们来证明一下：

```javascript
var Person = function(){};
var p = new Person();
console.log(p.__proto__ === Person.prototype);//true
```

# 5 instanceof

## 5.1 定义

在 `JavaScript` 中，判断一个变量的类型常常会用 `typeof` 运算符，在使用 `typeof` 运算符时采用引用类型存储值会出现一个问题，无论引用的是什么类型的对象，它都返回 `object`。`ECMAScript` 引入了 `Java` 中的运算符 `instanceof` 来解决这个问题。`instanceof` 运算符与 `typeof` 运算符相似，用于识别正在处理的`对象`的类型。与 `typeof` 方法不同的是，`instanceof` 方法要求开发者明确地确认`对象`为某特定类型。

`instanceof` 运算符用来测试一个`对象`在其`原型链`中是否存在一个构造函数的 `prototype` 属性。请注意这个是检测的是`原型链`，不是单纯的只检测对象的`隐式声明`一次，是不断的在对象的`隐式声明`中去找构造体的`显式声明`，注意如果传入的第一个参数如果不是`对象`，会直接返回`false`。

## 5.2 用法

通常来讲，使用 `instanceof` 就是判断一个实例是否属于某种类型。

```javascript
// 判断 foo 是否是 Foo 类的实例
function Foo(){}
var foo = new Foo();
console.log(foo instanceof Foo)//true
```

另外，更重的一点是 `instanceof` 可以在继承关系中用来判断一个实例是否属于它的父类型。

```javascript
// 判断 foo 是否是 Foo 类的实例 , 并且是否是其父类型的实例
function Aoo(){}
function Foo(){}
Foo.prototype = new Aoo();//JavaScript 原型继承

var foo = new Foo();
console.log(foo instanceof Foo)//true
console.log(foo instanceof Aoo)//true
```

上面的代码中是判断了一层继承关系中的父类，在`多层继承`关系中，`instanceof` 运算符同样适用。

## 5.3 语言规范

`ECMAScript-262 edition 3` 中 关于 `instanceof` 运算符的定义

```text
11.8.6 The instanceof operator
 The production RelationalExpression:
     RelationalExpression instanceof ShiftExpression is evaluated as follows:

 1. Evaluate RelationalExpression.
 2. Call GetValue(Result(1)).// 调用 GetValue 方法得到 Result(1) 的值，设为 Result(2)
 3. Evaluate ShiftExpression.
 4. Call GetValue(Result(3)).// 同理，这里设为 Result(4)
 5. If Result(4) is not an object, throw a TypeError exception.// 如果 Result(4) 不是 object，
                                                                //抛出异常
 /* 如果 Result(4) 没有 [[HasInstance]] 方法，抛出异常。规范中的所有 [[...]] 方法或者属性都是内部的，
在 JavaScript 中不能直接使用。并且规范中说明，只有 Function 对象实现了 [[HasInstance]] 方法。
所以这里可以简单的理解为：如果 Result(4) 不是 Function 对象，抛出异常 */
 6. If Result(4) does not have a [[HasInstance]] method,
   throw a TypeError exception.
 // 相当于这样调用：Result(4).[[HasInstance]](Result(2))
 7. Call the [[HasInstance]] method of Result(4) with parameter Result(2).
 8. Return Result(7).

 // 相关的 HasInstance 方法定义
 15.3.5.3 [[HasInstance]] (V)
 Assume F is a Function object.// 这里 F 就是上面的 Result(4)，V 是 Result(2)
 When the [[HasInstance]] method of F is called with value V,
     the following steps are taken:
 1. If V is not an object, return false.// 如果 V 不是 object，直接返回 false
 2. Call the [[Get]] method of F with property name "prototype".// 用 [[Get]] 方法取
                                                                // F 的 prototype 属性
 3. Let O be Result(2).//O = F.[[Get]]("prototype")
 4. If O is not an object, throw a TypeError exception.
 5. Let V be the value of the [[Prototype]] property of V.//V = V.[[Prototype]]
 6. If V is null, return false. 
 // 这里是关键，如果 O 和 V 引用的是同一个对象，则返回 true；否则，到 Step 8 返回 Step 5 继续循环
 7. If O and V refer to the same object or if they refer to objects
   joined to each other (section 13.1.2), return true.
 8. Go to step 5.
```

上面的规范定义很晦涩，而且看起来比较复杂，涉及到很多概念，但把这段规范翻译成 `JavaScript` 代码却很简单，

```javascript

// object instanceof constructor

//instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。

//模拟instanceof 功能
function instance_of(L, R) {//L 表示左表达式，R 表示右表达式
 var O = R.prototype;// 取 R 的显示原型
 L = L.__proto__;// 取 L 的隐式原型
 //请注意这个判断条件，目的是无限循环，不断在L的隐式声明链中找R的显式说明，只有完全找不到的时候，才会返回false，
 //请注意undefined，null没有属性的，没有隐式声明的。
 while (true) {
   if (L === null){
    return false;
   }
   if (O === L)// 这里重点：当 O 严格等于 L 时，返回 true
   {
    return true;
   }
   L = L.__proto__;//L.__proto__.__proto__.__proto__.__proto__.__proto__..........
 }
}
```

# 6 参考网站

- [JavaScript instanceof 运算符深入剖析](https://www.ibm.com/developerworks/cn/web/1306_jiangjj_jsinstanceof/)