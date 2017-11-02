---
title: js学习之jquery.iviewer图片插件学习
category: js学习
tags:
  - jquery
  - iviewer
  - js学习
date: 2017-10-11 00:00:00
---

> 今天同事找我说，他今天使用jquery.iviewer图片切换出了点问题，我过去看了半天，因为之前没有用过，实在越看越糊涂，很怂的回来，想下了源码看一下，在gayhub中找了半天，有好几个比较相近的，最终确定了<https://github.com/vmeln/iviewer-fix.git>，下载了之后，文件夹中没有专门的使用案例，也没说方法怎么用，我看了半天源码，才知道初始化之后想要调用对象方法怎么玩。

  <!-- more -->

# 第一步

```javascript
//声明一个全局变量接管这个方法
var viewer = $(selector).iviewer({src: "XXX.jpg"});
```

# 第二步

```javascript
//对全局变量进行操作,第一个参数是方法名，从第二个参数开始，就是接收传入方法的参数值
viewer.iviewer("functionName","param01","param02",...................,"paramN");

//举个栗子
//iviewer源码中 有个方法是 zoom_by(delta, zoom_center)，
 viewer.iviewer("zoom_by", -0.98, origin);//后面两个就是传入方法的参数
```

# 完整代码

放上完整代码，这个是做图片切换的例子，比较常用的一个方法

```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <style>
        #container {
            position: absolute;
            top: 200px;
            left: 100px;
            border: 1px solid;
            width: 600px;
            height: 500px;
        }
    </style>
</head>
<body>
    <div id="container"></div>
    <button id="cli">切换</button>
</body>
<script src="jquery.js"></script>
<script src="jquery-ui.js"></script>
<script src="jquery.iviewer.js"></script>
<script>
    $(function () {

    var viewer = $('#container').iviewer({
        src: "http://wallpapers.wallhaven.cc/wallpapers/full/wallhaven-51908.jpg",
        update_on_resize: false,
        onMouseMove: function (ev, coords) { }
    });
    $("#cli").click(function(){
        viewer.iviewer("loadImage", "http://img3.imgtn.bdimg.com/it/u=3504081194,1127587637&fm=27&gp=0.jpg");
    });
})
</script>
</html>
```

# 总结

最开始我以为在初始化之后，我这边就可以直接`viewer.loadImage(url)`，就可以调用了结果这边一直说对象没有这个方法，然后我就以为`viewer.iviewer({loadImage(url)})`这样调用，结果还是不行，只有认真去看源码，以及下载的案例中怎么用的，才发现是`viewer.iviewer(‘loadImage','url')`这样调用的，我去给同事说了之后，同事还说了一句我好厉害，日常羞愧，感觉做东西真的不能想当然，还有，这个要认真看源码，日常捂脸.jpg。
