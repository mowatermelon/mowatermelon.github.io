---
title: 样式表小白之路
category: 样式表
tags:
  - 小白之路
  - 样式表
date: 2017-04-18 00:00:00
---

> 做了一个图片居中的效果，学习到媒体查询的使用方法

<!-- more -->

```css
@charset "UTF-8";
body{
  height: 100%;
}
.box{
  height: 500px;
  background-repeat: no-repeat;
  background-image: url("03.jpg");
  background-position: center center;
  background-size: 100% 100%;
  text-align: center;
}
@media (min-width: 992px) {

  .col-md-8{
    margin: 0 300px;
  }
}
@media screen  (min-width: 992px)  and  (min-width:768px)  {

  .col-md-8{
    margin: 0 300px;
  }
}
```