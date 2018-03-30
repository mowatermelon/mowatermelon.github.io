---
title: 框架学习之Arcgis for js 4.6本地部署
category: 框架学习
tags:
  - webgis
  - Arcgis for js 4.6
  - local-build
  - 框架学习
date: 2017-11-06 00:00:00
---
# 1 部署包下载

- [下载对应版本](https://developers.arcgis.com/downloads/apis-and-sdks?product=javascript)

<!--more-->

# 2 部署包举例

> 下载之后的目录效果，以4.6举例

![image](https://user-images.githubusercontent.com/18508817/38014622-ef5da80c-329b-11e8-8fea-fb0248c274cb.png)
![image](https://user-images.githubusercontent.com/18508817/38014649-fd5678b2-329b-11e8-879b-d53b3c67bb16.png)

# 3 安放部署包到项目中

> 将文件放到项目路径下面去，记住这个路径`/static/plugins/arcgis46`，我是把文件放在相对项目根文件夹的这个路径中

![image](https://user-images.githubusercontent.com/18508817/38014700-258ab4c4-329c-11e8-91f7-1bfe0688e257.png)

# 4 根据安放路径修改源码

## 4.1 修改init.js

修改上图中的init.js，将该文件中的`baseUrl:"https://[HOSTNAME_AND_PATH_TO_JSAPI]dojo`，修改为`baseUrl: (location.protocol === 'file:' ? 'http:' : location.protocol) + '//' + (function () { var result = ""; result = window.location.href.substr(window.location.href.indexOf("//") + 2); result = result.substr(0, result.lastIndexOf("/")); return result; })() + "/static/plugins/arcgis46/dojo"`

即指向从项目根文件夹开始写实际的`dojo.js`所在路径，如果后期部署包，路径进行了修改，主要是对`"/static/plugins/arcgis46/dojo"`进行修改。

## 4.2 修改dojo.js

同时修改`/static/plugins/arcgis46/dojo/dojo.js`，将该文件中的`baseUrl:"https://[HOSTNAME_AND_PATH_TO_JSAPI]dojo`，修改为`baseUrl: (location.protocol === 'file:' ? 'http:' : location.protocol) + '//' + (function () { var result = ""; result = window.location.href.substr(window.location.href.indexOf("//") + 2); result = result.substr(0, result.lastIndexOf("/")); return result; })() + "/static/plugins/arcgis46/dojo"`

即指向从项目根文件夹开始写实际的`dojo.js`所在路径，如果后期部署包，路径进行了修改，主要是对`"/static/plugins/arcgis46/dojo"`进行修改。

# 5 测试引入情况

## 5.1 安装esri依赖

```bash
cnpm i esri-loader --s
cnpm i dojo-loader --s
```

## 5.2 新建MapView组件

> 请注意

- 配置`esriLoader`的引入路径是`../../static/plugins/arcgis46/init.js`，即项目中实际的`init.js`的路径。
- 注意引入`esri`基础所需样式文件，`@import './../../static/plugins/arcgis46/esri/css/main.css'`。
- `view对象`实例化对应的标签一定要写一个固定的高度，要不然页面上不会显示。
- 请注意实例化`view`的过程中，通过`esriLoader`引入的依赖文件，一定要注意顺序，应该是`"esri/map", "esri/views/MapView","dojo/domReady!"`，顺序有问题，页面会报错，说`MapView`不是一个`constructor`。
- 注意通过`esriLoader.isLoaded()`来监听esriLoader是否已经初始化过了
- 注意通过`map.initialized`来判断`map`对象是否已经初始化完成。
- 对于`_this.view.hitTest(e)`来解析当前鼠标行为，在`3.X`版本之中，监听到鼠标的`evt`对象之后，就可以直接通过`evt.MapObject`来获取当前鼠标的经纬度，但是在`4.X`版本之中，是需要先将鼠标的`evt`对象进行解析之后，才能获取相关的地理信息数据。

> 组件源码

```html
<template>
  <div class="map_box">
    <div id="viewDiv" class="map_div" @mousemove="showCoordinates($event)" ></div>
    <p class="text-right map-info" :class="{'hide': isHide}">当前坐标：x:{{evt.x}},y:{{evt.y}}</p>
  </div>
</template>
<script>
  import esriLoader from 'esri-loader'

  export default {
    name: 'MapView',
    data () {
      return {
        map: {'loaded': ''},
        isHide: true,
        evt:{x:'',y:''},
        camera:{},
        view:{}
      }
    },
    watch: {
      'map.loaded': function () {
        if (this.map.initialized == true) {
          this.isHide = false;
        }
      }

    },
    mounted: function () {
      // 监听esriLoader是否存在，创建map
      if (!esriLoader.isLoaded()) {
        // no, lazy load it the ArcGIS API before using its classes
        esriLoader.bootstrap((err) => {
          if (err) {
            console.error(err);
          } else {
            // once it's loaded, create the map
            this.createMap();
          }
        }, {
          // use a specific version instead of latest 4.x
          url: '../../static/plugins/arcgis46/init.js'
        });
      } else {
        // ArcGIS API is already loaded, just create the map
        this.createMap();
      }

    },
    methods: {
      // 创建地图
      createMap: function () {
        let _this =this;

        esriLoader.dojoRequire(["esri/map", "esri/views/MapView","dojo/domReady!"], (Map,MapView) => {
          _this.map = new Map({
            basemap: "osm",
            ground: "world-elevation"// Use the world elevation service
          });
          _this.view = new MapView({
            container: "viewDiv",     // Reference to the scene div created in step 5
            map: _this.map,                 // Reference to the map object created before the scene
            scale: 50,          // Sets the initial scale to 1:50,000,000
            center: [114.40845006666666,30.456864444444443]  // Sets the center point of view with lon/lat
          });
        });
      },
      // 缩放到中心图层
      centerZoom: function () {
        this.map.centerAndZoom([114.40845006666666,30.456864444444443], 16);
      },
      // 显示当前坐标
      showCoordinates: function(e) {
        let _this = this;
        _this.view.hitTest(e)
          .then(function(res){
            let point = res.screenPoint;
            if(!_this.isHide){
                _this.evt.x = point.x;
                _this.evt.y = point.y;
            }
        });
      }

    }

  }
</script>
<style lang="scss" scoped>
@import './../../static/plugins/arcgis46/esri/css/main.css';
.map_box .map_div {
  width:100%;
  height: calc(100vh*0.8);
  cursor: pointer;
}
</style>
```