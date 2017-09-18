---
title: 样式表之媒体查询
category: 样式表
tags:
  - 媒体查询
  - 样式表
date: 2017-04-17 00:00:00
---

来至[搬运工](http://www.cnblogs.com/tdalcn/p/3512140.html)

> 媒体查询相关关键词 @media only screen and


  * only(限定某种设备)
  * screen 是媒体类型里的一种
  * and 被称为关键字，其他关键字还包括 not(排除某种设备)
***
<!-- more -->

> 常用类型

|类型	|解释
| :-------- | :-----|   
|all |所有设备
|braille |盲文
|embossed |盲文打印
|handheld |手持设备
|print	|文档打印或打印预览模式
|projection |项目演示，比如幻灯
|screen |彩色电脑屏幕
|speech |演讲
|tty |固定字母间距的网格的媒体，比如电传打字机
|tv |电视

ps:screen一般用的比较多，下面是我自己的尝试，列出常用的设备的尺寸，然后给页面分了几个尺寸的版本。
***

>  常用设备

|设备	|屏幕尺寸
| :-------- | :-----|
|显示器|1280 x 800
|ipad |1024 x 768
|Android |800 x 480
|iPhone |640 x 960

两种方式
```css
  /*
  <link rel="stylesheet" type="text/css" href="styleB.css" media="screen and (min-width: 600px) and (max-width: 800px)">

  意思是当屏幕的宽度大于600小于800时，应用styleB.css
  */

  @media screen and (max-width: 600px) { /*当屏幕尺寸小于600px时，应用下面的CSS样式*/
    .class {
      background: #ccc;
    }
  }
```

***
> 媒体查询相关关键词 device-aspect-ratio

  device-aspect-ratio可以用来适配特定屏幕长宽比的设备，这也是一个很有用的属性，比如，我们的页面想要对长宽比为4:3的普通屏幕定义一种样式，然后对于16:9和16:10的宽屏，定义另一种样式，比如自适应宽度和固定宽度：
```css
@media only screen and (device-aspect-ratio:4/3)
```
-webkit-min-device-pixel-ratio的常见值对比（是设备上物理像素和设备独立像素，设备像素比率）

|设备	   |分辨率	   |设备像素比率
| :--------   | :-----   | :---- |
|Android LDPI	|320×240	|0.75
|Iphone 3 & Android MDPI	|320×480	|1
|Android HDPI	|480×800	|1.5
|Iphone 4	|960×640	|2.0

> -webkit-min-device-pixel-ratio: 1.0

    所有非 Retina 的 Mac
    所有非 Retina 的 iOS 设备
    Acer Iconia A500
    Samsung Galaxy Tab 10.1
    Samsung Galaxy S

其他设备
> -webkit-min-device-pixel-ratio为1.3

    Google Nexus 7

> -webkit-min-device-pixel-ratio为1.5

    Google Nexus S
    Samsung Galaxy S II
    HTC Desire
    HTC Desire HD
    HTC Incredible S
    HTC Velocity
    HTC Sensation

> -webkit-min-device-pixel-ratio为2.0

    iPhone 4
    iPhone 4S
    iPhone 5
    iPad (3rd generation)
    iPad 4
    所有Retina displays 的MAC
    Google Galaxy Nexus
    Google Nexus 4
    Google Nexus 10
    Samsung Galaxy S III
    Samsung Galaxy Note II
    Sony Xperia S
    HTC One X

> -webkit-min-device-pixel-ratio: 3.0

     1.HTC Butterfly
     2.Sony Xperia S
***
> @media only screen and (min-resolution:144dpi)<resolution>（分辨率）


使用于：位图媒体类型,接受`max/min`前缀：
`resolution`媒体特性描述输出设备的分辨率，例如，像素密度。若查询设备的非方形像素，在`min-resolution`查询中指定的值必须与最稀疏尺寸进行比较，在`max-resolution`查询中必须与最密集尺寸进行比较。对于`resolution`（没有`min-`或`max-`前缀）查询从不查询设备的非方形像素。

对于印刷机，相当于分辨率（任意颜色的绘制点的分辨率）。

举例说明：该媒体查询表示样式表适用于分辨率大于每英寸144点的设备：
```css
@media print and (min-resolution: 144dpi) { … }
```
