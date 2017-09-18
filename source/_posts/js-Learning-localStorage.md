---
title: js学习之html5本地存储学习
category: js学习
tags:
  - html5
  - localStorage
  - js学习
date: 2017-04-25 00:00:00
---


参考网站[博客园--谢灿勇](http://www.cnblogs.com/st-leslie/p/5617130.html),[developer.mozilla](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage)
localStorage只支持string类型的存储,

<!-- more -->

```javascript
// 保存数据到localStorage
window.localStorage.setItem('key', 'value');

// 从localStorage获取数据
var data = window.localStorage.getItem('key');

// 从localStorage删除保存的数据
window.localStorage.removeItem('key');

// 从localStorage删除所有保存的数据
window.localStorage.clear();

// 保存数据到sessionStorage
window.sessionStorage.setItem('key', 'value');

// 从sessionStorage获取数据
var data = window.sessionStorage.getItem('key');

// 从sessionStorage删除保存的数据
window.sessionStorage.removeItem('key');

// 从sessionStorage删除所有保存的数据
window.sessionStorage.clear();
```

localStorage使用的例子
```javascript
var storage=window.localStorage;
            var data={
                name:'xiecanyong',
                sex:'man',
                hobby:'program'
            };
            var d=JSON.stringify(data);
            storage.setItem("data",d);
            //将JSON字符串转换成为JSON对象输出
            var json=storage.getItem("data");
            var jsonObj=JSON.parse(json);
            console.log(typeof jsonObj);
```
sessionStorage使用的例子
```javascript
// 获取文本输入框
var field = document.getElementById("field");
 
// 检测是否存在 autosave 键值
// (这个会在页面偶然被刷新的情况下存在)
if (window.sessionStorage.getItem("autosave")) {
  // 恢复文本输入框的内容
  field.value = window.sessionStorage.getItem("autosave");
}
 
// 监听文本输入框的 change 事件
field.addEventListener("change", function() {
  // 保存结果到 sessionStorage 对象中
  window.sessionStorage.setItem("autosave", field.value);
});
```
目前pc浏览器支持状态

|Feature|Chrome|Firefox (Gecko)|Internet Explorer|Opera|Safari (WebKit)|
|:----|:----|:----|:----|:----|:----|
|localStorage|4|3.5|8|10.50|4|
|sessionStorage|5|2|8|10.50|4|
目前手机浏览器支持状况

|Feature|Android|Firefox Mobile (Gecko)|IE Phone|Opera Mobile|Safari Mobile|
|:----|:----|:----|:----|:----|:----|
|Basic support|2.1|?|8|11|iOS 3.2|