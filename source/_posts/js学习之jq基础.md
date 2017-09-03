---
title: js学习之jq基础
category: js学习
tags:
  - jq基础
  - js学习
date: 2017-05-01 00:00:00
---

> ## 相关节点操作

`jQuery.parent(expr)` 找父亲节点，可以传入`expr`进行过滤，比如`$("span").parent()`或者`$("span").parent(".class")`

`jQuery.parents(expr)`,类似于`jQuery.parents(expr)`,但是是查找所有祖先元素，不限于父元素

`jQuery.children(expr)`.返回所有子节点，这个方法只会返回直接的孩子节点，不会返回所有的子孙节点

`jQuery.contents()`,返回下面的所有内容，包括节点和文本。这个方法和children()的区别就在于，包括空白文本，也会被作为一个

`jQuery`对象返回，`children()`则只会返回节点

<!-- more -->

`jQuery.prev()`，返回上一个兄弟节点，不是所有的兄弟节点

`jQuery.prevAll()`，返回所有之前的兄弟节点

`jQuery.next()`,返回下一个兄弟节点，不是所有的兄弟节点

`jQuery.nextAll()`，返回所有之后的兄弟节点

`jQuery.siblings()`,返回兄弟姐妹节点，不分前后

`jQuery.find(expr)`,跟`jQuery.filter(expr)`完全不一样。`jQuery.filter()`是从初始的`jQuery`对象集合中筛选出一部分，而`jQuery.find()`的返回结果，不会有初始集合中的内容，比如`$("p")`,`find("span")`,是从元素开始找,等同于$`("p span")`


> ## jquery判断子元素是否存在

### 1 判断子元素是否存在

```javascript
//一级子元素 if($("#specialId>img").length==0)
if ($( "#specialId:has(img)" ).length==0)
{
//-----没有img子标记-----
}
else
{
//-------有img子标记------
}
```

### 2 选择特定id元素下的特定id子元素

```javascript
$("#form" ).children( "#t" ) 
```

### 3 选择特定id元素下的子元素

```javascript
$("ul#u>li:nth-child(2)" ) 
```

### 4 判断某个元素是否存在

```javascript
if ($( "#myId" ).length>0)
{
//存在
}
```

> ## jquery样式移除

```javascript
$(this).children(".glyphicon-chevron-up")
        .addClass("glyphicon-chevron-down")
        .removeClass("glyphicon-chevron-up");
```

 在选择器使用上面，通过某个样式进行选择，但是`同时需要`移除该样式，添加新样式，可以先`添加`新样式，再`移除`样式
> ## 按钮禁用

```javascript
    $("#btnBack").addClass("disabled hidden");
    $('#btnBack').prop('disabled', true);
```

> ## 监听回车事件
```javascript
$(function () {  
            //定义回车事件  
            if (document.addEventListener) {//如果是Firefox  
                document.addEventListener("keypress", fireFoxHandler, true);  
            }  
            else {  
                document.attachEvent("onkeypress", ieHandler);  
            }  

            function fireFoxHandler(evt) {  

                if (evt.keyCode == 13) {  

                    $("#btnLogin")[0].click();  
                }  
            }  
            function ieHandler(evt) {  

                if (evt.keyCode == 13) {  
                    $("#btnLogin")[0].click();  
                }  
            }  
        });  

 </script>
```
