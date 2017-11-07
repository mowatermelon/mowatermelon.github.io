---
title: js学习之prompt学习
category: js学习
tags:
  - prompt
  - localStorage
  - js学习
date: 2017-04-25 00:00:00
---

参考网站[developer.mozilla](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/JavaScript_basics)

# 1 定义

用于显示可提示用户进行输入的对话框，会弹出一个对话框， 有一点像 `alert()` 只不过 `prompt()` 需要用户输入数据,，而且在用户点击 `OK` 后将数据存储在变量里。

# 2 语法

```javascript
prompt(text,defaultText)
```

|参数|描述|
|:---|:---|
text| 可选。要在对话框中显示的纯文本（而不是 HTML 格式的文本）。
defaultText|可选。默认的输入文本。

> 说明

如果用户单击提示框的`取消按钮`，则返回 `null`。如果用户单击`确认按钮`，则返回输入字段当前显示的文本。
在用户点击`确定按钮`或`取消按钮`把对话框关闭之前，它将阻止用户对浏览器的`所有输入`。在调用 `prompt()` 时，将`暂停`对 JavaScript 代码的执行，在用户作出响应之前，`不会`执行下一条语句。

# 3 完整案例

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,Chrome=1" />
  <meta name="viewport" content="width=device-width,initial-scale=1, minimum-scale=1.0, maximum-scale=1, user-scalable=no" />
  <meta http-equiv="Pragma" content="no-cache"/>
  <meta http-equiv="Cache-Control" content="no-cache"/>
  <meta http-equiv="Expires" content="0"/>
  <meta name="author" content="WU EVA" />
  <title>prompt_demo</title>
  <style>
  button, html input[type="button"], input[type="reset"], input[type="submit"] {
      cursor: pointer;
      -webkit-appearance: button;
  }
  .btn-info {
      color: #ffffff;
      background-color: #5bc0de;
      border-color: #46b8da;
  }
  .btn {
      display: inline-block;
      padding: 6px 12px;
      margin-bottom: 0;
      font-weight: normal;
      line-height: 1.428571429;
      text-align: center;
      white-space: nowrap;
      outline: 0 none;
      vertical-align: middle;
      cursor: pointer;
      border: 1px solid transparent;
      border-radius: 4px;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      -o-user-select: none;
      user-select: none;
  }
  pre {
      display: block;
      padding: 9.5px;
      margin: 0 0 10px;
      font-size: 13px;
      line-height: 1.428571429;
      color: #333333;
      word-break: break-all;
      word-wrap: break-word;
      background-color: #f5f5f5;
      border: 1px solid #cccccc;
      border-radius: 4px;
  }
  code, pre {
      font-family: Monaco, Menlo, Consolas, "Courier New", monospace;
  }
  pre {
      white-space: pre-wrap;
  }
  code, kbd, pre, samp {
      font-family: monospace, serif;
      font-size: 1em;
  }
  h1, .h1 {
      font-size: 36px;
  }
  h1, h2, h3 {
      margin-top: 20px;
      margin-bottom: 10px;
  }
  h1, h2, h3, h4, h5, h6, .h1, .h2, .h3, .h4, .h5, .h6 {
      font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
      font-weight: 500;
      line-height: 1.5;
  }
  h1 {
      margin: 0.67em 0;
      font-size: 2em;
  }
  *, *:before, *:after {
      -webkit-box-sizing: border-box;
      -moz-box-sizing: border-box;
      box-sizing: border-box;
  }
  </style>
</head>
<body>
  <div class="container">
    <h1>study prompt()<br/></h1>
    <input type="button" class="btn btn-info" value="Display a prompt box" />
    <br/>
    <br/>
    <pre>
    window.onload =function(){
      var show_btn = document.querySelector('input');
      var show_sel =document.querySelector('h1');
      show_btn.onclick =function(){
        //召唤promt大法
        show_prompt(show_sel);
      }
    }

    //弹出promt提示框，并作转化处理
    function show_prompt(selText){
      var myName = prompt('Please enter your name.','watermelon');
      if (myName!=null && myName!=""){
        localStorage.setItem('name', myName);
        selText.innerHTML += ' hello , <span class="text-info">' + myName+'</span>';
      }
    }
    </pre>
  </div>
</body>
<script type="text/javascript">
    window.onload =function(){
      var show_btn = document.querySelector('input');
      var show_sel =document.querySelector('h1');
      checkName(show_sel);
      show_btn.onclick =function(){
        show_prompt(show_sel);
      }
    }

    //弹出promt提示框，并作转化处理
    function show_prompt(selText){
      var myName = prompt('Please enter your name.','watermelon');
      if (myName!=null && myName!=""){
        localStorage.setItem('name', myName);
        selText.innerHTML += 'hello, <span class="text-info">' + myName+'</span>';
        selText.innerHTML += '<br/>'
      }
    }

    //检查当前的localstroge 的用户姓名
    function checkName(selText){
      var usrName = localStorage.getItem('name');
      if (usrName!=null && usrName!=""){
        selText.innerHTML += 'hello, <span class="text-info">' + usrName+'</span>';
        selText.innerHTML += '<br/>'
      }
    }

  </script>
</html>

```