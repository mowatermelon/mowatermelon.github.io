---
title: js学习之js函数hacker
category: js学习
tags:
  - hacker
  - js学习
date: 2017-05-03 00:00:00
---

- # 1 定义式函数与赋值式函数

```javascript
    Fn();  //执行结果：console.log在控制台打印提示
    function Fn(){   //声明式函数
        console.log("执行了定义式函数");
    }

    Fun();  //执行结果：程序报错，提示函数未定义
    var Fun= function(){   //赋值式函数
        console.log("执行了赋值式函数");
    }
```

JS的解析过程分为两个阶段：`预编译期(预处理)`与`执行期`，页面加载过程中，浏览器会对页面上或载入的每个js代码块(或文件)进行扫描，如果遇到`定义式函数`，则进行`预处理`(类似于C等的编译)，处理完成之后再开始`由上至下`执行；遇到`赋值式函数`，则只是将`函数`赋给一个`变量`，不进行`预处理`，待调用到的时候才进行处理。

<!-- more -->

- # 2 代码块及js文件的处理

`代码块`是指一对`<script type="text/javascript"></script>`标签包裹着的`JS`代码，`文件`就是指通过`src`导入页面的`JS文件`。
浏览器对每个`代码块`或`文件`进行独立的扫描，然后对全局的代码进行`顺序执行`。所以，在一个`代码块`(`文件`)中，`函数`可以在调用之后进行`定义式`定义(如案例一中的`Fn()`),但在两个独立的`代码块`中，`定义函数`所在的`代码块`必须在函数`被调用`的`代码块`之前。

```javascript
<script type="text/javascript">
function Fun(){
    console.log("Hello World!");
}
</script>
```

```javascript
<script type="text/javascript">
Fun();//控制台顺利打印，因为函数所在代码块在上一个代码块
Fn(); //报错，提示函数未定义，因为函数所在代码块在下一个代码块
</script>
```

```javascript
<script type="text/javascript">
function Fn(){
    console.log("Hello World!");
}
</script>
```

- # 3 重复定义函数会覆盖前面的定义

因为在`JS`中重名的函数，`后定义`的会覆盖`前面定义`的函数，这种策略和`JS`的顺序执行也是有关系的。

```javascript
fn(); //控制台打印提示 2
function fn(){
    console.log(1);
}
function fn(){
    console.log(2);
}
fn(); //控制台打印提示 2
```

- # 4 body的onload函数与body内部函数的执行

`body`中`内部的函数`会先于`onload`的函数执行,`body`的`onload`事件触发条件是`body`内容加载完成，而`body`中的`JS`代码会在这一事件触发之前运行。

```javascript
function fnOnLoad(){
    console.log("I am outside the Wall!");
}
window.onload = fnOnLoad;
console.log("I am inside the Wall..");
//先在控在控制台打印"I am inside the Wall.."
//后在控制台打印"I am outside the Wall!"
```

- # 5 JS是多线程or单线程？

严格来说，`JS`是没有`多线程`概念的，所有的程序都是`单线程`依次执行的。  `延时执行`、`Ajax异步加载`只是看起来像`多线程`。

```javascript
function fn1(){
    setTimeout(function(){
        console.log("我先调用")
    },1000);
}
function fn2(){
    console.log("我后调用");
}
fn1();
fn2();
// 先在控制台打印：“我后调用”，
// 1秒后在控制台打印：“我先调用”
```

看上去，`fn2()`和延时程序是分`两个过程`再走，但其实，这是`JS`中的`回调机制`在起作用，类似于操作系统中的`中断和响应` —— 延时程序设置一个`中断`，然后执行`fn2()`，待1000毫秒时间到后，再回调执行`fn1()`。
同样，4中`body`的`onload`事件调用的函数，也是利用了回调机制——body加载完成之后，回调执行`fnOnLoad()`函数。
`Ajax请求`中的数据处理函数也是一样的道理。

- # 6 引入js中文乱码

在调用外部js进行相关验证的时候，中间会包涵部分中文，但是由于页面一般是使用`utf-8`作为编码，但是中文在`utf-8`显示乱码，成了一串乱七八糟的东西，所以在页面引用的时候，请加上编码格式。

```javascript

// charset="gbk"
// charset="gb2312"

//举个例子
<script src="js/XXXX.js" type="text/javascript" charset="gb2312"></script>
```

> 参考网站
- [js 程序执行与顺序实现详解](http://www.jb51.net/article/36755.htm)
- [JS——声明式函数与赋值式函数](http://blog.csdn.net/hao134838/article/details/51778750)