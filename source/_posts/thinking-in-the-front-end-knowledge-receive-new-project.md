---
title: 前端思考之接手新项目
category: 前端思考
tags:
  - 接手新项目
  - 前端思考
date: 2017-10-28 00:00:00
---

> 最近接手了一个比较老的项目，整理一下我接手之后操作流程

<!-- more -->

# 1 阅读项目代码

## 1.1 配置代码

### 1.1.1 参数配置代码

  `<serverInfor></serverInfor>`,`<map></map>`

### 1.1.1 组件配置代码

  `<formInfo></formInfo>`,`<business></business>`

### 1.1.1 路由配置代码

  `<widgetcontainer></widgetcontainer>`

## 1.2 使用到的前端库

### 1.2.1 样式库

  `esri.dijit`,`esri.symbol`,`ligerUI`

### 1.2.2 控制库

  `dojo`,`esri.map`,`esri.geometry`

# 2 分析新增功能需求

- 2.1 添加对应功能按钮到主页面

- 2.2 绑定功能对应的面板功能

- 2.3 面板能够选择本地文件夹

- 2.4 上传文件到后台

- 2.5 后台分析文件内容

- 2.6 后台返回对应规范的结果集

- 2.7 前台获取到数据

- 2.8 对于获取到的数据信息进行分析

- 2.9 获取需要的参数

- 2.10 通过获取的参数，调用相关方法进行页面展示

# 3 确认技术实现逻辑

## 3.1

在`<widgetcontainer>`中添加一个新的`widget`，并寻找合适的功能按钮图片。

## 3.2

在`项目/javascript/Widget`文件路径中，参考其他组件js模版，新建`OverlayfileMsg.js`。

## 3.3

在页面拼接Template中添加`input[type=file]`的组件，并添加相关样式，优化显示效果。为了更好的提示效果，绑定一个`span`标签实时进行显示上传文件路径。

## 3.4

先将上传文件的类型进行判断，是否为空和或者用户选择的上传类型是否匹配。

## 3.5

将通过判断的数据，读取相关配置，通过`dojo.io.iframe.send()`方法传到对应的`c#`后台，后台通过`HttpFileCollection files = context.Request.Files;HttpPostedFile fileObj = files[i];`进行获取，先判断文件上传格式是否正确，如果都正确，则进行文件保存到服务器指定路径处理，并返回处理结果。

## 3.6

> 后台返回对应规范的结果集

- 文件上传失败！（初始值）
- 请选择文件。
- 目录名不正确。
- 上传文件大小超过限制。
- 上传文件扩展名是不允许的扩展名。
- 上传成功

## 3.7

> 前台获取到数据，获取后台实际返回值，判断后台处理状态，根据不同状态做对应处理。

### 3.7.1 上传成功

获取需要的参数，调用相关方法进行页面展示

### 3.7.2 上传失败

对于请求后台失败的情况下进行直接弹窗报错

# 4 开始写代码

  通过对应代码编辑器，编写代码，如果遇见错误，通过相关[开源社区](https://github.com/)，搜索相关案例，了解[dojo实现机制](http://dojotoolkit.org/reference-guide/1.9/)，了解[esri实现机制](https://developers.arcgis.com/javascript/3/jsapi/)。

## 4.1

```xml
<widget label ="叠加"  visible="true" index="8"   config="Widget.OverlayfileMsg" icon="images/img/sharp.png"/>
```

## 4.2

```javascript
  dojo.declare("Widget.OverlayfileMsg", null, {
      title: "叠加外部数据",
      divID: "LoadDiv",
      btnLoad: "btnLoadFileByName",
      formFile:"fileForm",
      ConfigTool: null,
      map: null,
      opened: false,
      graphicLayer: null,
      floatPanel: null,
      floatPanelHeight: 128,
      floatPanelWith: 288,
      qryTemplate: "",
      adjust: 12,
      highlightSymbol: null,
      EmptyGraphicLayer: null, //空白图层
      handleMapOnClickHandle: null,
      constructor: function (param) {
      },
      CreateQryTemplate: function () {
      },
      startup: function () {
      },
      adjustFloatPanelTitle: function (adjust) {
      },
      setSubmit:function(fileType){
      },
      initalPanel: function () {
      },
      show: function () {
      },
      hide: function () {
      },
      clear: function () {
      }
  });
```

## 4.3

```html
  <a class="l-button" id="addfile"  style="position: relative;display:inline-block;margin:0 auto;line-height: 24px;text-align: center;"><span>选择文件</span><input type="file" name="fileUp" id ="btnLoadFile" style="position: absolute;right: 0;top: 0;opacity: 0;width: 100%;cursor: pointer;text-indent: -2em;"/></a>
```

```javascript
  /*------------------------------OverlayfileMsg.js*/

  dojo.connect(dojo.byId(this.btnFileLoad), "onchange", this, "changeFile");
  changeFile:function(){
      // debugger;
      var fileObj = dojo.byId(this.btnFileLoad);
      var nameObj = dojo.byId(this.spanFileLoad);
      if(fileObj.value.length>0){
          nameObj.innerHTML=fileObj.files[0].name;
      }else{
          nameObj.innerHTML="未选择任何文件";
      }
  },
```

## 4.4

```javascript
  var _this = this;
  var arrRadioItem = dojo.query("input[type='radio']");
  dojo.forEach(arrRadioItem, function (item) {
      dojo.connect(item, "onclick", item, _this.checkRadio);
  });
  checkRadio: function (obj) {
      //保证单选按钮的唯一性
      dojo.query(".radio" + obj.srcElement.name).parent().siblings().children().attr("checked", false);
  },
  checkFileType: function () {
      if (this.map && this.opened) {
          var fileType = "";
          var TempText = "";
          var dataHTML = this.dataTemplate();
          var fileTypeL = dataHTML.length;
          if (fileTypeL == 0) {
              fileType = "SHARP";
          } else if (fileTypeL == 1) {
              fileType = dataHTML[0].ID;
          } else if (fileTypeL > 1) {
              fileType = dojo.query("input[type='radio']::checked").attr("value");
          }
          if (fileType.length > 0) {
              fileType = fileType.toString();
              var filePath ="";
              var fileObj = dojo.byId(this.btnFileLoad);
              var fileLength =fileObj.files.length;
              if(fileType!="SHARP"){
                  filePath = fileObj.files[0].name;
              }else{
                  filePath = dojo.byId(this.spanFileLoad).innerHTML;
              }
              // debugger;

              filePath = filePath.toString();
              filePath = filePath.toLowerCase();
              if (fileLength > 0) {
                  // debugger;
                  this.addFile(fileType, filePath,fileLength);
              } else {
                  TempText = "必须要选择一个文件";
              }
          } else {
              TempText = "必须要选择一个文件类型";
          }

          if(TempText.length>0){
              showMessage(TempText);
          }
      }
  },
  checkUnique:function(filePath){
      var isRight =false;
      //给数组去重
      Array.prototype.unique = function () {
          this.sort(); //先排序
          var res = [this[0]];
          for (var i = 1; i < this.length; i++) {
              if (this[i] !== res[res.length - 1]) {
                  res.push(this[i]);
              }
          }
          return res;
      }

      var patt=/\.+[\w]{3}/g
      var ml = filePath.replace(patt,'');
      ml = ml.split("，").unique();
      if(ml.length==1){
          isRight =true;
      }
      // console.log("checkUnique");
      // console.log(isRight);
      return isRight;
  },
  checkContainer:function(filePath){
      var isRight =true;
      var checkType = ["dbf", "shp", "shx"];
      var patt=/[\w]+\./g;
      var ml = filePath.replace(patt,'');
      ml = ml.toLowerCase().split("，");
      var rightArray = [];
      for(var i = 0 ; i <ml.length ; i++){
        var pattern = RegExp(ml[i]);
        if(pattern.test(checkType)&& ml[i]!==undefined&&!pattern.test(rightArray)){
          rightArray.push(ml[i]);
        }
      }
      if(rightArray.length!=checkType.length){
          isRight = false;
      }
      // console.log("checkContainer");
      // console.log(isRight);
      return isRight;
  },
  addFile: function (fileType, filePath,fileLength) {
      //var filePath = dojo.byId(this.btnFileLoad).attr("value");
      var isRight = false;
      var TempText = "";
      // debugger;
      switch (fileType) {
          case "SHARP":
              // debugger;
              var TempTxt = "请上传同一个Sharp文件，并且至少要选择后缀名为.shp、.dbf和.shx这三种格式，请重新选择！";
              if(fileLength<3){
                  TempText = TempTxt;
              }else if(fileLength>=3){
                  if(this.checkUnique(filePath)){
                      if (!this.checkContainer(filePath)) {
                          TempText = TempTxt;
                      }
                  }else{
                      TempText = TempTxt;
                  }
              } //判断Shape文件
              break;
          case "CAD":
              if (filePath.indexOf(".dwg") == -1||fileLength!=1) {
                  TempText = "请只上传一个文件，并且上传文件类型属于CAD文件！请重新选择";
              }//判断CAD文件
              break;
          case "TXT":
              if (filePath.indexOf(".txt") == -1||fileLength!=1) {
                  TempText = "请只上传一个文件，并且上传文件类型属于TXT文件！请重新选择";
              }//判断TXT文件
              break;
          default:
              if (filePath.indexOf(".txt") == -1) {
                  TempText = "请只上传一个文件，并且上传文件类型属于TXT文件！请重新选择";
              }//判断TXT文件
              break;
      }
      if(TempText.length==0){
          this.setSubmit(fileType);
      }else{
          showMessage(TempText);
      }
  }
```

## 4.5

```javascript
  /*------------------------------layoutOther.js*/

  //分析文件路径
  getFXWJLJQueryMethod: function () {
      var result = null;
      var arrServer = this.getFileQueryServerInfo();
      var strMethodID = "分析文件路径";
      result = this.getMethod(arrServer, strMethodID);
      return result;
  },
  //获取文件分析服务信息
  getFileQueryServerInfo: function () {
  }

  /*------------------------------OverlayfileMsg.js*/
  setSubmit:function(fileType){
      var method = this.ConfigTool.getFXWJLJQueryMethod();
      if (method) {
          var uploadUrl = method.url;
          var uploadMethod = method.name;
          var _this =this;
          try {
              dojo.io.iframe.send({
                  form:_this.formFile, //某个form元素包含本地文件路径
                  method: "GET",
                  handleAs: "html", //服务器将返回html页面
                  url: uploadUrl,
                  content:{
                      dir:fileType,
                      method:uploadMethod,
                      global:_this
                  },
                  load: this.onSubmitted, //提交成功
                  error: this.onSubmitError //提交失败
              });
          }
          catch (e) {
              showMessage("查找文件实际路径出错，错误原因是" + e.message);
          }

      }else{
          showMessage("读取配置失败，请检查配置");
      }
  },
  onSubmitted:function(response, ioArgs){
      var res = response.childNodes[0].innerText;
      // debugger;
      var _this =this;
      if(!!res){
          res = JSON.parse(res);
          if(res.success!="false"){
              var fileType = _this.content.dir;
              _this.content.global.readFile(res.msg);
          }else{
              showMessage(res.msg);
          }
      }
  },
  onSubmitError:function(response, ioArgs){
      // debugger;
      showMessage(response);
  }

```

## 4.6

```c#
  private void showSuc(HttpContext context, string message)
  {
      string res = "{\"success\":\"true\",\"msg\":" + message + "}";
      context.Response.AddHeader("Content-Type", "text/html; charset=UTF-8");
      context.Response.Write(res);
      context.Response.End();
  }

  private void showError(HttpContext context, string message)
  {
      string res = "{\"success\":\"false\",\"msg\":\"" + message + "\"}";
      context.Response.AddHeader("Content-Type", "text/html; charset=UTF-8");
      context.Response.Write(res);
      context.Response.End();
  }
```

## 4.7

### 4.7.1 上传成功

```javascript
  onSubmitted:function(response, ioArgs){
      var res = response.childNodes[0].innerText;
      // debugger;
      var _this =this;
      if(!!res){
          res = JSON.parse(res);
          if(res.success!="false"){
              var fileType = _this.content.dir;
              _this.content.global.readFile(res.msg);
          }else{
              showMessage(res.msg);
          }
      }
  },
  initArcJson:function(data){
    var starttime =new Date();
    var getAttr = data;
    getAttr.spatialReference= this.map.spatialReference;
    var demo ={
        "geometry": {},
        "attributes": {
            "generated": Number(starttime),
            "title": "西瓜信息技术股份有限公司",
            "status": 200
        }
    };
    demo.geometry = getAttr;
    return demo;
  },
  readFile: function (data) {
    // debugger;
    // var starttime =new Date();
    // console.log("starttime"+starttime);
    // console.log(data);
    this.EmptyGraphicLayer.clear();
    for(var i=0;i<data.length;i++){
        // debugger;
        var tempType = data[i].type;
        var tempData = this.initArcJson(data[i]);
        switch (tempType)
        {
            case "point":
                this.loadPoint(tempData);      //加载point信息
                break;
            case "line":
                this.loadLine(tempData);      //加载line信息
                break;
            case "polygon":
                this.loadPolyon(tempData);    //加载polygon信息
                break;
            default:
                this.loadPoint(tempData);    //加载point信息
                break;
        }

    }
    // console.log("this.EmptyGraphicLayer"+this.EmptyGraphicLayer);
    // console.log("took", new Date - starttime, "milliseconds");
  },
  loadPoint: function (data) {
    try {
        // debugger;
        if(!!data){
            var markerSymbol = new esri.symbol.SimpleMarkerSymbol();
            markerSymbol.setColor(new esri.Color([192, 64, 223,0.5]));
            var labelPoint = data.geometry.points;
            var labelSr =data.geometry.spatialReference;
            var labelAttr =data.attributes;
            // debugger;
            for(var item in labelPoint){
                    var point = new esri.geometry.Point([Number(labelPoint[item][0]), Number(labelPoint[item][1])], labelSr);
                    var wmpoint = esri.geometry.webMercatorUtils.geographicToWebMercator(point);
                    var textSymbol = new esri.symbols.TextSymbol("item: " + item );

                    if (!this.EmptyGraphicLayer){
                            this.EmptyGraphicLayer = getEmptyGraphicLayer();
                    }
                    var grPp = new esri.Graphic(point, markerSymbol);
                    var grPt = new esri.Graphic(point, textSymbol);

                    if (grPp) {
                            grPp.visible = true;
                            grPp.attributes = labelAttr;
                            grPt.visible = true;
                            grPt.attributes = labelAttr;
                            this.EmptyGraphicLayer.add(grPp);
                            // this.EmptyGraphicLayer.add(grPt);
                            this.EmptyGraphicLayer.visible = true;
                    }
                    if(item==labelPoint.length-1){
                        // debugger;
                        this.map.centerAndZoom(point,18);
                    }
            }

        }else{
            showMessage("数据为空");
        }
    }
    catch (e) {
            showMessage("加载点信息错误，错误原因是" + e.message);
    }
  },
  loadLine: function (data) {
    try {
        var LineSymbol = new esri.symbols.CartographicLineSymbol();
        LineSymbol.setWidth(5);
        var labelAttr =data.attributes;
        if(!!data){
            data.visible = true;
            var t_graphic =new esri.Graphic(data);
            t_graphic.symbol=LineSymbol;
            t_graphic.attributes = labelAttr;
            if (!this.EmptyGraphicLayer){
                this.EmptyGraphicLayer = getEmptyGraphicLayer();
            }
            this.EmptyGraphicLayer.add(t_graphic);
            var centerPoint =t_graphic.geometry.getExtent().getCenter();
            console.log(centerPoint);
            this.map.centerAndZoom(centerPoint,18);
            this.EmptyGraphicLayer.visible = true;
            this.EmptyGraphicLayer.opacity=0.75;
        }else{
            showMessage("数据为空");
        }
    }
    catch (e) {
            showMessage("加载线信息错误，错误原因是" + e.message);
    }
  },
  loadPolyon: function (data) {
    try {
        var labelAttr =data.attributes;
        var fillSymbol = new esri.symbol.SimpleFillSymbol(esri.symbol.SimpleFillSymbol.STYLE_NULL,new esri.symbol.SimpleLineSymbol("solid", new esri.Color([82, 158, 229, 0.7]), 5),null);
        if (!!data) {
            data.visible = true;
            var t_graphic =new esri.Graphic(data);
            t_graphic.symbol=fillSymbol;
            t_graphic.attributes = labelAttr;
            if (!this.EmptyGraphicLayer){
                this.EmptyGraphicLayer = getEmptyGraphicLayer();
            }
            this.EmptyGraphicLayer.add(t_graphic);
            var centerPoint =t_graphic.geometry.getExtent().getCenter();
            // debugger;
            this.map.centerAndZoom(centerPoint,18);
            // var markerSymbol = new esri.symbol.SimpleMarkerSymbol();
            // var textSymbol = new esri.symbols.TextSymbol("中心点");
            // var grPt = new esri.Graphic(centerPoint, textSymbol);
            // var grPm = new esri.Graphic(centerPoint, markerSymbol);

            // this.EmptyGraphicLayer.add(grPt);
            // this.EmptyGraphicLayer.add(grPm);
            this.EmptyGraphicLayer.visible = true;
            this.EmptyGraphicLayer.opacity=0.75;
        }else{
            showMessage("数据为空");
        }
    }
    catch (e) {
            showMessage("加载面信息错误，错误原因是" + e.message);
    }
  }
```

### 4.7.2 上传失败

```javascript
  //提示错误原因
  onSubmitError:function(response, ioArgs){
    // debugger;
    showMessage(response);
  }
```

# 5 测试代码运行效果

  在本地部署项目，利用后台断点和前台debugger进行相关排错。

# 6 保证代码持续运行

- 上传文件格式错误，进行合理报错
- 上传文件过多，进行合理报错
- 上传文件中包含正确的文件，但是也包含不正确的文件，进行合理报错
- 解析图形文件是否正确绘制在页面，进行合理报错
- 三种类型文件上传解析是否都正确，进行合理报错
- 后续需要处理大文件上传的文件，前后台是否存在异步，进行合理报错
- 后续补充
