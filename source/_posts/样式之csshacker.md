---
title: 样式之csshacker
category: 样式表
tags:
  - csshacker
  - 样式表
date: 2017-04-21 00:00:00
---


- 1 按钮和input在谷歌中会有一个默认蓝色边框，由于我用的是bootstrap，所以我这边直接就btn的总样式改了，还有加了input的选中样式修改。
```css
input,.btn{
  outline:0 none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline:0 none;
}
input:hover,
input:focus,
input:active{
  outline:0 none;
}
```
<!-- more -->
- 2 自动填充的文本框默认有个黄色背景
由于chrome浏览器默认的给自动填充的文本框添加了背景样式属性
```css

/*谷歌默认样式*/
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
    background-color: rgb(250, 255, 189);
    background-image: none;
    color: rgb(0, 0, 0);
}
/*修改版本一 没有用*/
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
    background-color: transparent !important;
    background-image: none;
    color: var(--c);//用了一个css变量
}
/*最终建议修改样式*/
input:-webkit-autofill {
  -webkit-box-shadow: 0 0 0px 1000px white inset;
}
```
- 3 让文本自动换行
> 做网页的时候，我们很经常碰到文本的显示，通常来说，文本太长就会很难看，可以用CSS控制文本自动换行。

方法一：你定死盒子的宽度，即给盒子一个宽度值（是数值，不是百分比）  

方法二：强制不换行
```css
div{
    white-space：normal;
    //默认不换行;
    white-space:nowrap; 
    //nowrap强制在同一行内显示所有文本，
    //直到文本结束或者遭遇 <br/> 对象
}
```
方法三：自动换行
```css
div{ 
    word-wrap: break-word;
    //normal 亚洲语言和非亚洲语言的文本规则，
    //允许在字内换行
    word-break: normal;
 }
```

方法四：强制英文单词断行
```css
div{
    word-break:break-all;
    //word-break可以设置强行换行;
}
```
方法五 另外，只要在CSS中定义了如下句子，可保网页不会再被撑开了，以表格为例。
```css
table{
    table-layout: fixed;
}
td{
    word-break: break-all; 
    word-wrap:break-word;
}
```
方法六 既防止表格/层撑破又防止单词断裂，以表格为例。
```css
table { 
    table-layout: fixed;
    word-wrap:break-word;
}
div { 
    word-wrap:break-word;
}
```