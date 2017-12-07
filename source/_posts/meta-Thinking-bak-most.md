---
title: 西瓜有话说之meta学习整理常用篇
category: js_meta
tags:
- bak
- watermelon
- js_meta
date: 2017-10-25 00:00:00
---
# 1 概述

`meta`标签提供关于`HTML`文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他`web`服务。 —— W3School

<!-- more -->

## 1.1 必要属性

|属性|值|描述|
|-:-|-:-|-:-|
|content|some text|定义与http-equiv或name属性相关的元信息|

## 1.2 可选属性

|属性|值|描述|
|-:-|-:-|-:-|
|http-equiv|content-type / expire / refresh / set-cookie|把content属性关联到HTTP头部。|
|name|author / description / keywords / generator / revised / others|把 content 属性关联到一个名称。|
|content|some text|定义用于翻译 content 属性值的格式。|

# 2 详细解释

## 2.1 页面编码

一般`html`源代码和`css`文件编码要统一，如果不统一会导致`CSS hack`，页面乱码网页页面排版乱等兼容问题。这个元数据是必须要被声明的。

国内常用的流行的有`utf-8`、`gb2312`这两种。一般这两种类型就能满足国内网页编码需求。当然程序和数据库中也会用到这两种编码类型来处理网页和存储数据类型。

```html
<!-- html4中声明编码格式 -->
<meta http-equiv="Content-Type" content="text/html; charset=gb2312">
<meta http-equiv="Content-Language" Content="zh-CN">

<!-- html5中声明编码格式 -->
<meta charset='utf-8' />
```

## 2.2 浏览器默认渲染版本

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 关于X-UA-Compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->
<meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 使用IE7 -->
<meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->
```

## 2.3 viewport

能优化移动浏览器的显示，如果不是`响应式网站`，不要使用`initial-scale`或者禁用缩放。
大部分`4.7-5寸`设备的`viewport`宽设为`360px`；`5.5寸`设备设为`400px`；`iphone6`设为`375px`；`ipone6 plus`设为`414px`。

```html

<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
<!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边 -->
```

|属性|值|
|-:-|-:-|
|width|宽度（数值 / device-width），范围从200 到10,000，默认为980 像素|
|height|高度（数值 / device-height），范围从223 到10,000|
|initial-scale|初始的缩放比例，范围从>0 到10|
|minimum-scale|允许用户缩放到的最小比例|
|maximum-scale|允许用户缩放到的最大比例|
|user-scalable|用户是否可以手动缩 (no,yes)|
|minimal-ui|可以在页面加载时最小化上下状态栏。（已弃用）|

注意，很多人使用`initial-scale=1`到非响应式网站上，这会让网站以`100%`宽度渲染，用户需要手动移动页面或者缩放。如果将`initial-scale=1`和`user-scalable=no`或`maximum-scale=1`一起设置，则用户将不能放大/缩小网页来看到全部的内容。

## 2.4 页面作者

每个网页都应有一个不超过 150 个字符且能准确反映描述页面作者标签。

```html
<meta name="author" content="author name" />
<!-- 举个栗子 -->
<meta name="author" content="WU EVA">
```

## 2.5 页面关键词

每个网页应具有描述该网页内容的一组唯一的关键字。

使用人们可能会搜索，并准确描述网页上所提供信息的描述性和代表性关键字及短语。

标记内容太短，则搜索引擎可能不会认为这些内容相关，但是另外标记不应超过 874 个字符。

```html
<meta name="keywords" content="your tags" />
<!-- 举个栗子 -->
<meta name="keywords" content="WATERMELON,HOME,WELCOME" />
```

## 2.6 页面描述

每个网页都应有一个不超过 150 个字符且能准确反映网页内容的描述标签。

```html
<meta name="description" content="150 words" />
<!-- 举个栗子 -->
<meta name="description" content="THERE ARE WATERMELON HOME,WELCOME!" />
```

## 2.7 页面创建时间

指的是文件的创建时间，简单说就是指这个页面写第一行代码的时间。

```html
<meta name="build" content="2017-12-07" />
<!-- 举个栗子 -->
<meta name="build" content="2017-12-07" />
```

## 2.8 页面版权

`copyright`用于定义网页版权，`copyright`出现在`name`属性中，使用`content`属性提供网页的版权

```html
<meta name="copyright" content="your copyright">
<!-- 举个栗子 -->
<meta name="copyright" content="本页版权归watermelon所有。All Rights Reserved">
```

## 2.9 页面生成工具

指的是文件是用什么来生成的，简单说就是页面编辑器是什么。

```html
<meta name="generator" content="your editor">
<!-- 举个栗子 -->
<meta name="generator" content="VSCODE">
```

## 2.10 网络应用名称

定义正运行在该网页上的网络应用名称

```html
<meta name="application-name" content="your application name">
<!-- 举个栗子 -->
<meta name="application-name" content="WATERMELON-APP">
```

## 2.11 页面创建者

以自由格式定义文档创建者的名字。请注意，它可以是该机构的名称。如果不止一个，应该使用几个`<meta>`元素;

```html
<meta name="creator" content="your company">
<!-- 举个栗子 -->
<meta name="creator" content="WATERMELON COMPANY">
```

## 2.12 页面发布者

发布者，以自由格式定义文档的发布者的名称。请注意，它可以是该机构的名称;

```html
<meta name="publisher" content="your company">
<!-- 举个栗子 -->
<meta name="publisher" content="WATERMELON COMPANY">
```

## 2.13 搜索引擎索引方式

`robotterms`是一组使用逗号(,)分割的值，通常有如下几种取值：`none`，`noindex`，`nofollow`，`all`，`index`和`follow`。确保正确使用`nofollow`和`noindex`属性值。

```html
    <meta name="robots" content="index,follow" />
    <meta name="google" content="index,follow" /><!-- 谷歌机器人，这是机器人的代名词，谷歌的索引爬虫; -->
    <meta name="googlebot" content="index,follow" /><!-- 谷歌机器人，这是机器人的代名词，谷歌的索引爬虫; -->
    <meta name="verify" content="index,follow" />
    <meta name="slurp" content="index,follow" /><!-- 跟踪搜索引擎抓取工具Slurp -->
```

|Value|Description|Used by|
|:--|:--|:--|
|all|文件将被检索，且页面上的链接可以被查询|All|
|index|文件将被检索|All|
|noindex|文件将不被检索|All|
|follow|页面上的链接可以被查询|All|
|nofollow|页面上的链接不可以被查询|All|
|noodp|防止使用“Open Directory Project”说明,如果有的话，作为搜索引擎结果页面中的描述|Google, Yahoo, Bing|
|noarchive|防止搜索引擎缓存页面的内容|Google, Yahoo|
|nosnippet|防止在搜索引擎结果页面中显示页面的任何描述|Google|
|noimageindex|防止此页面显示为索引图像的引用页面|Google|
|noydir|防止此页面显示为索引图像的引用页面|Yahoo|
|nocache|防止搜索引擎缓存页面的内容|Bing|

## 2.14 页面重定向和刷新

`content`内的数字代表时间（秒），既多少时间后刷新。如果加`url`,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。

```html
<meta http-equiv="refresh" content="0;url=" />
<!-- 举个栗子 -->
<meta http-equiv="refresh" content="3;url=https://mowatermelon.github.io/">
```

## 2.15 预定义的样式表

`content` 属性的值必须匹配同一文档中的一个 `link` 元素上的 `title` 属性的值，或者必须匹配`同一文档`中的一个 `style` 元素上的 `title` 属性的值。

```html
<meta http-equiv="default-style" content="the document's preferred stylesheet">
<!-- 举个栗子 -->
<meta http-equiv="default-style" content="theme-color-blue">
```

## 2.16 禁用缓存

禁止浏览器从本地计算机的缓存中访问页面内容：这样设定，访问者将无法脱机浏览。

```html
<meta http-equiv="Pragma" content="no-cache">
```

## 2.17 转码申明

用百度打开网页可能会对其进行转码（比如贴广告），避免转码可添加如下meta

```html
<meta http-equiv="Cache-Control" content="no-siteapp" />
```

## 2.18 WebApp全屏模式

伪装app，离线应用。

```html
<meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->
```

## 2.19 隐藏状态栏/设置状态栏颜色

只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent 。

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```

## 2.20 添加到主屏后的标题

```html
<meta name="apple-mobile-web-app-title" content="title">
```

## 2.21 忽略数字自动识别为电话号码

```html
<meta content="telephone=no" name="format-detection" />
```

## 2.22 忽略识别邮箱

```html
<meta content="email=no" name="format-detection" />
```

## 2.23 添加智能 App 广告条 Smart App Banner

告诉浏览器这个网站对应的app，并在页面上显示下载banner。

```html
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
```

## 2.24 屏幕控制相关

```html
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
```

## 2.25 浏览器内核控制

国内浏览器很多都是双内核（`webkit`和`Trident`），`webkit`内核高速浏览，`IE内核`兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器选择何种内核渲染

```html
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```

国内双核浏览器默认内核模式如下：

- 搜狗高速浏览器、QQ浏览器：IE内核（兼容模式）

- 360极速浏览器、遨游浏览器：Webkit内核（极速模式）

## 2.26 Windows 8

```html
<meta name="msapplication-TileColor" content="#000"/> <!-- Windows 8 磁贴颜色 -->
<meta name="msapplication-TileImage" content="icon.png"/> <!-- Windows 8 磁贴图标 -->
```

## 2.27 站点适配

主要用于PC-手机页的对应关系。

```html

<meta name="mobile-agent"content="format=[wml|xhtml|html5]; url=url">
<!--
[wml|xhtml|html5]根据手机页的协议语言，选择其中一种；
url="url" 后者代表当前PC页所对应的手机页URL，两者必须是一一对应关系。
-->
```

## 2.28 revisit-after (重访)

通知搜索引擎多少天访问一次

```html
<meta name="revisit-after" CONTENT="7 days" >
```

## 2.29 Window-target (显示窗口的设定)

`已经废弃`，说明：强制页面在当前窗口以独立页面显示。

```html

<meta http-equiv="Widow-target" Content="_top"/>

```

注意：这个属性是用来防止别人在框架里调用你的页面。Content选项：`_blank`、`_top`、`_self`、`_parent`。

## 2.30 Pics-label (网页RSAC等级评定)

`已经废弃`，说明：在IE的Internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级别就是通过该参数来设置的。

```html

<meta http-equiv="Pics-label" Contect= "(PICS－1.1'http://www.rsac.org/ratingsv01.html' I gen comment 'RSACi North America Sever' by 'inet@microsoft.com' for 'http://www.microsoft.com' on '1997.06.30T14:21－0500' r(n0 s0 v0 l0))">

```

注意：不要将级别设置的太高。RSAC的评估系统提供了一种用来评价Web站点内容的标准。用户可以设置Microsoft Internet Explorer（IE3.0以上）来排除包含有色情和暴力内容的站点。上面这个例子中的`HTML`取自`Microsoft`的主页。代码中的（n 0 s 0 v 0 l 0）表示该站点不包含不健康内容。级别的评定是由RSAC，即美国娱乐委员会的评级机构评定的，如果你想进一步了解RSAC评估系统的等级内容，或者你需要评价自己的网站，可以访问RSAC的站点：`http://www.rsac.org/`。

## 2.31 Page-Enter、Page-Exit (进入与退出)

`已经废弃`，说明：这个是页面被载入和调出时的一些特效。

```html

<meta http-equiv="Page-Enter" Content="blendTrans(Duration=0.5)"/>
<meta http-equiv="Page-Exit" Content="blendTrans(Duration=0.5)"/>
<!-- 注意：blendTrans是动态滤镜的一种，产生渐隐效果。另一种动态滤镜RevealTrans也可以用于页面进入与退出效果:  -->
<meta http-equiv="Page-Enter" Content="revealTrans(duration=x, transition=y)"/>
<meta http-equiv="Page-Exit" Content="revealTrans(duration=x, transition=y)"/>

```

Duration 表示滤镜特效的持续时间(单位：秒)，Transition表示使用哪种特效，取值为0-23。

|Transition|滤镜类型|
|:---|:---|
|0|矩形缩小|
|1|矩形扩大|
|2|圆形缩小|
|3|圆形扩大|
|4|下到上刷新|
|5|上到下刷新|
|6|左到右刷新|
|7|右到左刷新|
|8|竖百叶窗|
|9|横百叶窗|
|10|错位横百叶窗|
|11|错位竖百叶窗|
|12|点扩散|
|13|左右到中间刷新|
|14|中间到左右刷新|
|15|中间到上下|
|16|上下到中间|
|17 右下到左上|
|18|右上到左下|
|19|左上到右下|
|20|左下到右上|
|21|横条|
|22|竖条|
|23|以上22种随机选择一种|

## 2.32 MSThemeCompatible (XP主题)

`已经废弃`，说明：是否在IE中关闭 xp 的主题

```html
<meta http-equiv="MSThemeCompatible" Content="Yes">
```

注意：关闭 xp 的蓝色立体按钮系统显示样式，从而和win2k 很象。

## 2.33 IE6 (页面生成器)

`已经废弃`，说明：页面生成器generator，是ie6

```html
<meta http-equiv="IE6" Content="Generator">
```

注意：用什么东西做的，类似商品出厂厂商。

## 2.34 Content-Script-Type (脚本相关)

`已经废弃`，说明：这是近来W3C的规范，指明页面中脚本的类型。

```html
<meta http-equiv="Content-Script-Type" Content="text/javascript">
```

# 3 常用备份

```html
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,Chrome=1" />
    <meta name="viewport" content="width=device-width,initial-scale=1, minimum-scale=1.0, maximum-scale=1, user-scalable=no" />
    <meta http-equiv="Pragma" content="no-cache"/>
    <meta http-equiv="Cache-Control" content="no-cache"/>
    <meta http-equiv="Expires" content="0"/>
    <meta name="author" content="WU EVA" />
    <meta name="keywords" content="WATERMELON,HOME,WELCOME" />
    <meta name="description" content="THERE ARE WATERMELON HOME,WELCOME!" />
    <meta name="build" content="2017-12-07" />
    <meta name="copyright" content="本页版权归watermelon所有。All Rights Reserved">
    <meta name="generator" content="VSCODE" />
    <meta name="robots" content="all" />
    <meta name="googlebot" content="all" />
```