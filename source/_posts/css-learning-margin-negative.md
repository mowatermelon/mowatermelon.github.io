---
title: 样式之使用margin负值
category: 样式表
tags:
  - margin_negative
  - 样式表
date: 2017-10-17 00:00:00
---

之前想的是如果要在一个盒子上加一个小的`文字标签`，首先会考虑到`absolute`，结果我今天做`position`整理的时候看了一下张鑫旭关于使用`margin负值`做`文字标签`，才发现用`margin`写，代码会很简洁。

<!-- more -->

但是前提是知道父盒子的宽度和高度，如果不知道宽度，而且父盒子不是内联元素，使用absolute很可能满天飞；如果是使用margin的解决办法的话不知道图片大小那真的就是一脸懵，一点一点的左移上移，感觉效率也没那么高。

还有可以结合overflow和margin负值来做图片轮播图，就不过多举例了。

[更多测试案例](https://mowatermelon.github.io/demoArray/basecss/marginHack.html)

> 先放上html结构

```html
<div class="demo-absolute">
  <dt class="p-img">
      <a href="javascript:void(0)">
        <img src="https://static.bootcss.com/www/assets/img/jqueryapi.png?1510078115427"/>
      </a>
      <div class="b-price">￥999.00</div>
  </dt>
</div>
<div class="demo-margin">
  <dt class="p-img">
    <a href="javascript:void(0)">
      <img src="https://static.bootcss.com/www/assets/img/jqueryapi.png?1510078115427"/>>
    </a>
    <div class="price-box"><span class="b-price">￥999.00</span></div>
  </dt>
</div>

```

>然后放上两种样式解决思路

```css
/*先放上主要共有样式*/
a img {
    border: 0 none;
    vertical-align: middle;
}
dt {
    height: 130px;
}
.p-img {
    margin: 5px 0;
}
.b-price{
  background: none repeat scroll 0 0 #4ad5ff;
  color: #fff;
  font-family: arial;
  font-weight: bold;
  line-height: 1.5;
  padding: 2px 5px;
}
/*absolute 解决方案*/
.demo-absolute dt {
  position: relative;
  width: 300px;
}
.demo-absolute  .b-price {
  position: absolute;
  top: 5px;
  left: 20px;
}

/*margin 解决方案*/
.demo-margin .t-r .price-box{
  margin: -145px 0 0 221px;
}
```