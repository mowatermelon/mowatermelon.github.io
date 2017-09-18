---
title: 框架学习之angular_app学习
category: 框架学习
tags:
  - angular
  - bower
  - gulp
  - less
  - 框架学习
date: 2017-09-04 00:00:00
---

> 本文档是学习[Angular JS 仿拉勾网 WebApp 开发移动端单页应用](http://coding.imooc.com/lesson/80.html#mid=2256)学习日志

# 1 了解涉及到的技术

## 1.1 angular

诞生于`2009年`，由`Misko Hevery` 等人创建，后为`Google`所收购。是一款优秀的`前端JS框架`，已经被用于`Google`的多款产品当中。`AngularJS`有着诸多特性，最为核心的是：`MVC`、`模块化`、`自动化双向数据绑定`、`语义化标签`、`依赖注入`等等。

<!-- more -->
angular主要使用到的概念，`module` `diretive` `表达式` `service` `injector` `依赖注入` `模型` `filter` `数据绑定` `$scope` `controller` `view`
，对于其中部分进行相关解释。

> module

模块 所有的东西必须先放在模块中  才会正常运行    魔法书

> directive 指令

召唤魔法
定义:通过HTML标签、属性、样式或注释使Angular编译器居来为指定的`DOM`元素绑定特定的行为，甚至是改变DOM元素和它的子元素。

内置指令:`ng-model`,`ng-bind`,`ng-click`,`ng-class`,`ng-if`,`ng-hide`,`ng-repeat`

自定义指令常用属性:
`template`,`templateUrl`,`link`,`restrict`,`scope`,`transclude`

> service 服务

共有的代码逻辑  攻击魔法

> controller 控制器

私有的代码逻辑 辅助魔法

> filter 过滤器

对数据进行过滤

> view 视图

指令是angular的灵魂 核心

angular webapp 结构图

## 1.2 bower

`twitter` 推出的一款包管理工具，基于`The Only Real Dev Language`的`模块化思想`，把功能`分散`到各个模块中，让模块和模块之间存在`联系`，通过 `Bower` 来管理模块间的这种联系。  
`包`是指一系列有意义的资源的集合，在`bower`这里，更多体现在`json`文件，它是这些资源的配置文件，一个完整的包都应该有一个`bower.json`文件。
`管理`包含`获取`，`下载`，`安装`，`更新`，`查找`,`注册`等等一系列对资源的操作。

### 1.2.1 基础功能

    `注册模块`：每个包需要确定一个唯一的 ID 使得搜索和下载的时候能够正确匹配   
    `文件存储`：把文件存储在一个有效的网络地址上,使用的时候可以直接下载到  
    `上传下载`：你可以把你的包注册后上传存储，使用的时候可以使用一条命令直接下载到当前项目  
    `依赖分析`：它帮我们解决了包与包直接的依赖关系，当我们下载一个`包A`的时候,由于它依赖`包B`,所以`bower`会自动帮我们下载好`包B`  

### 1.2.2 `Bower` 与 `npm` 的关系

`npm`是专门管理`node`模块的管理工具，而`bower`是`node`的模块，因为`bower`是依赖`node`，`npm`和`git`。正如前面所言，`npm`是擅长的是`管理node模块`，而`bower`管理的`范围更大`，涉及html,css,js和图片等`媒体资源`。或许，这也是人们喜欢在`服务器端`使用`npm`,而在`客户端`使用`bower`。

### 1.2.3 为什么要使用`Bower`?

- `节省时间`  
    为什么要学习`Bower`的第一个原因，就是它会为你节省寻找客户端的依赖关系的时间。一般安装`jQuery`的时候，都需要去`jQuery`网站`下载包`或`使用CDN版本`。但是有了`Bower`，只需要输入一个命令，`jquery`就会安装在本地计算机上，你 __不需要__ 去记`版本号`之类的东西，你也可以通过`Bower`的`info`命令去查看任意库的信息。  
- `脱机工作`  
    `Bower`会在用户主目录下创建一个`.bower`的文件夹，这个文件夹会下载所有的资源、并安装一个软件包使它们可以离线使用。如果你熟悉`Java`，`Bower`即是一个类似于现在流行的`Maven`构建系统的`.m2`仓库。每次你下载任何资源库都将被安装在两个文件夹中 —— 一个在的应用程序文件夹，另一个在用户主目录下的`.bower`文件夹。因此，下一次你需要这个仓库时，就会用那个用户主目录下`.bower`中的版本。  
- `可以很容易地展现客户端的依赖关系`  
    你可以创建一个名为`json`的文件，在这个文件里你可以指定所有客户端的依赖关系，任何时候你需要弄清楚你正在使用哪些库，你可以参考这个文件。  
- `让升级变得简单`  
    假设某个库的新版本发布了一个重要的安全修补程序，为了安装新版本，你只需要运行一个命令，`bower`会自动更新所有有关新版本的依赖关系。

## 1.3 gulp

`gulp`是前端开发过程中对代码进行构建的工具，是自动化项目的构建利器；不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成；使用她，我们不仅可以很愉快的编写代码，而且大大提高我们的工作效率。

`gulp`是基于`Nodejs`的自动任务运行器， 她能自动化地完成 `javascript`/`coffee`/`sass`/`less`/`html`/`image`/`css` 等文件的的`测试`、`检查`、`合并`、`压缩`、`格式化`、`浏览器自动刷新`、`部署文件生成`，并`监听文件`在改动后重复指定的这些步骤。在实现上，她借鉴了`Unix操作系统`的`管道（pipe）思想`，前一级的`输出`，直接变成后一级的`输入`，使得在操作上非常简单。

`gulp` 和 `grunt` 非常类似，但相比于 `grunt` 的频繁 `IO` 操作，`gulp` 的流操作，能更快地更便捷地完成构建工作。

```javascript
gulp.src() //读取文件和文件夹
gulp.dest() //生成文件和文件夹
gulp.watch() //监控文件和文件夹
gulp.task() //定制任务
gulp.pipe() //用流的方式处理文件
//举个栗子
gulp.task('happyLife',function(){
    gulp.src('happyPepople/life/**/*')
    .pipe(gulp.dest(EVA.devPath))
    .pipe(gulp.dest(EVA.proPath))
    .pipe($.connect.reload());//只要编译命令执行就刷新页面
});
```

## 1.4 less 样式预处理器

`LESS`将`CSS`赋予了动态语言的特性，是`css预编译处理`，如`变量`，`继承`，`运算`，`函数`。`LESS`既可以在`客户端`上运行 (支持`IE 6+`, `Webkit`, `Firefox`)，也可以借助`Node.js`或者`Rhino`在服务端运行。  
本质上，`LESS` 包含一套`自定义`的`语法`及一个`解析器`，用户根据这些语法定义自己的样式规则，这些规则最终会通过`解析器`，`编译生成`对应的 `CSS 文件`。`LESS `并没有`裁剪` CSS `原有的特性`，更不是用来`取代` CSS 的，而是在现有 CSS 语法的基础上，为 CSS 加入`程序式语言`的特性。

### 1.4.1 基础使用案例

```less
    //这里是一些简单的LESS语法
    //@import 'a.less'
    //自动计算依赖文件生成对应的综合的css文件
    @width:400px;
    @height:300px;
    @font_size:12px;
    @bg:#111;

    textarea {
        width:@width;
        height:@height;
        font-size:@font_size;
    }
    .bg{
        .fun(123px);/*调用相关函数*/
        background-color:@bg;
        .select{
            width:@width;
        }
        &:after{
            content:'';
        }
    }
    .fun(@px){
        height:@px;
    }
```

### 1.4.2 生成的css文件形式

```css
    textarea {
        width: 400px;
        height: 300px;
        font-size: 12px;
    }
    .bg {
        height: 123px;
        background-color: #111111;
    }
    .bg .select {
        width: 400px;
    }
    .bg:after {
        content: '';
    }

```

## 1.5 单页应用

`单页应用（SPA）`是指在浏览器中运行的应用，它们在使用期间`不会重新加载`页面。像所有的应用一样，它旨在帮助用户`完成任务`，比如`编写文档`或者`管理Web服务器`。可以认为`单页应用`是一种从`Web服务器`加载的`富客户端`。
说白就是无刷新，整个`webapp`就一个`html`文件，里面的各个功能页面是`javascript`通过`hash`,或者`history api`来进行`路由`，并通过`ajax`拉取`数据`来实现`响应功能`。因为整个`webapp`就一个`html`，所以叫`单页面`。
`单页应用`的页面切换流畅,属于`前后端分离`的典型。

# 2 安装相关环境

先安装好[node](https://nodejs.org/en/)和[git bash](https://git-for-windows.github.io/)两个软件，注意安装`git bash`不要一路点击next，其中有一步是询问`git`指令是全局安装还是仅能在`git shell`或者`git bash`中运行，软件默认是第一个，指令只能在`git shell`或者`git bash`中运行，请选择第二个，`git`指令所有的`命令行工具`都可以运行。当然如果你本地已经安装过`github`客户端，那你就不用安装这个软件，直接通过`git shell`就可以了。
对于`node`不一定要下载最新的版本，可以下载之前的稳定版本，然后通过`node`命令指示符全局安装相关环境。

```bash
# 已经翻墙
npm install -g bower
npm install -g gulp

# 未翻墙
npm install cnpm -g --registry=https://registry.npm.taobao.org
cnpm i -g bower
cnpm i -g gulp
```

将安装指令的文件夹配置到系统环境变量`PATH`中(`计算机-->右键属性-->高级系统设置-->环境变量`)，我公司电脑系统盘是`D盘`，这边的默认全局安装路径是`D:\Program Files\nodejs\node_global`，但是我家中的电脑，系统盘是`C盘`，全局安装之后的安装路径是`C:\Users\Administrator\AppData\Roaming\npm`，每次全局安装之后，会提示安装路径，如果该路径你之前已经设置成环境变量就不用管，但是如果提示的安装路径你没有设置过环境变量，你就会发现这个全局安装的指令一直跑不了，还有就是`bower`指令这个是基于`git`指令的，如果你的`github`在安装的时候没有设置全局安装，还需要手动将`git`指令所在文件夹配置到环境变量中，我就是由于前期安装了`github`客户端，直接用的`git shell`,`git`的声明路径应该是`C:\Users\Administrator\AppData\Local\GitHub\PortableGit_f02737a78695063deace08e96d5042710d3e32db\mingw32\bin`，就是你本地`github`安装路径下的`bin`文件夹，具体地址请根据实际情况配置。

# 3 开始写项目

## 3.1 git初始化

如果上一步没有将`git指令`设置全局可用，那么需要在其他终端进行`git初始化`，如果没有设置的话，将`gitbash`添加到右键功能栏，[相关教程](../software-learning-rightClick-to-add-Gitbash/)
,或者将`git shell`添加到右键功能栏。但是如果已经将`git指令`设置为所有终端都可以用，那就直接在`vscode`终端中输入相关指令，新建项目文件夹，并在项目文件夹中执行`git初始化`。

```bash
git init
```

执行完成之后，空项目文件夹中应该有以下文件夹

```text
- .git
    - hooks
    - info
    - objects
    - refs
```

## 3.2 bower初始化

在项目文件夹中右键选择`open with code`，在`vscode`中打开当前项目文件,如果没有下载的可以点击链接进行下载[Download scode](https://code.visualstudio.com/Download)，
请注意一定要先`git`初始化，再`bower`初始化，要不然会报错，说当前文件夹找不到`git`相关文件，在终端中输入`bower`初始化指令。

```bash
bower init
? name angular_app # 项目名称
? description this is a test angular webapp # 项目描述
? main file # 项目主目录
? keywords angular gulp less bower # 项目关键词
? authors mowatermelon # 作者名称
? license MIT # 项目版权
? homepage # 项目主页
? set currently installed components as dependencies? Yes # 现在是否已经按照一些组件，请根据实际情况输入 yes or no
? add commonly ignored files to ignore list? Yes# 是否忽略一些默认需要忽略检测的文件 yes or no
? would you like to mark this package as private which prevents it from being ac
? would you like to mark this package as private which prevents it from being ac
cidentally published to the registry? Yes# 是否把这个包标记为私有，防止它成为ac  yes or no

{
  name: 'angular_app',
  authors: [
    'mowatermelon'
  ],
  description: 'this is a test angular webapp',
  main: '',
  keywords: [
    'angular',
    'gulp',
    'less',
    'bower'
  ],
  license: 'MIT',
  homepage: '',
  private: true,
  ignore: [
    '**/.*',
    'node_modules',
    'bower_components',
    'test',
    'tests'
  ]
}

? Looks good? Yes//相关文件夹是否正确生成
```

> bowerrc处理

重新配置`bower`包安装路径，__非必要步骤__，`bower`下载的包默认的安装路径是`bower_components`，如果你看到默认文件夹名字特别不爽，是换一个文件夹放安装包，注意新建`.bowerrc文件`有一定窍门。

```bash
//新建`.bowerrc`路径配置文件，这个必须通过指令新建，`window`默认文件必须有文件名
PS X:\XX\demo>null>.bowerrc
//命令执行之后会新建文件，但是会报错，这个报错可以忽略。
//该命令只能在系统或者`node`的命令管理器中执行，请注意这个语句在`vscode`终端中是不能执行的

```

> 在`.bowerrc`文件中配置以下`json`，设置默认`bower`的包下载文件夹名称

```json
{
    "directory": "lib"
}
```

## 3.3 bower 安装运行相关包

### 3.3.1 举个安装的完整栗子

```bash
  bower install --save angular
  # 默认安装不是不会更新到包管理中的，需要添加--save 才会自动保存到bower管理中。
  # 针对移动端不存在兼容性，如果是pc项目，需要考虑ie兼容，需要安装低版本
  # bower install --save angular#1.2
  bower not-cached    https://github.com/angular/bower-angular.git#*
  bower resolve       https://github.com/angular/bower-angular.git#*
  bower download      https://github.com/angular/bower-angular/archive/v1.6.6.tar.
gz
  bower extract       angular#* archive.tar.gz
  bower resolved      https://github.com/angular/bower-angular.git#1.6.6
  bower install       angular#1.6.6

angular#1.6.6 bower_components\angular
# 添加到配置文件
```

### 3.3.2 安装依赖包

然后在vscode终端中开始安装其他包

```bash
  bower install --save requirejs
  bower install --save ui-router#0.4.2
# 如果你想按照课程学下去，
# 请注意一定要安装这个指定ng路由版本(ui-router)，
# 或者你可以去研究一下最新版怎么玩，你就不用管版本了
# 这边不指定版本，直接安装最新版本的话，
# 反正我这边是在安装最新的是`1.0.6`，
# 安装下来之后，完全找不到`angular-ui-router.js`这个文件，
# 然后我安装网上的安装
# "angular-ui-router": "0.2.8-bowratic-tedium"，
# 结果控制台一直报各种"transition"的错，
# 程序都还没有做什么，就这么多错，真的气到原地爆炸.gif
  bower install --save mdui # 这个样式库不一定要安装，只是个人喜好
```

### 3.3.3 卸载依赖包

如果发现包安装错误或者安装多余可以进行包的卸载

```bash
  bower uninstall --save requirejs #卸载相关包并且修改bower.json，推荐这种卸载
  bower uninstall requirejs #仅卸载相关包不会修改bower.json
```

### 3.3.3 复制配置好的`bower.json`

或者你想偷懒不想通过指令去安装，可以直接把我这边配置好的`bower.json`的`dependencies`内容直接拿过去用，然后直接执行`bower install`就好，其中`mdui`这个是我个人喜欢的一个样式框架，非必须安装。

```json
  "dependencies": {
    "angular": "^1.5.5",
    "angular-resource": "^1.5.6",
    "angular-ui-router": "^0.4.2",
    "mdui": "^0.3.0"
  }
```

## 3.4 npm安装服务环境相关包

```bash
  npm  install --save-dev gulp gulp-clean gulp-concat gulp-connect gulp-cssmin gulp-imagemin gulp-less gulp-load-plugins gulp-uglify open
 # 每个模块之间通过空格隔开，可以进行批量安装
```

> 相关说明

| 依赖包名 | 功能 |
|:-------|:-------|
|  gulp  |  必要的运行包，毕竟还要靠gulp干大事  |
|  gulp-load-plugins  |  协助gulp找到其他gulp子包一起玩的类似脚手架之类的感觉  |
|  gulp-clean  |  在gulp-load-plugins的召唤下，可以清理相关文件夹  |
|  gulp-concat  |  在gulp-load-plugins的召唤下，可以整合文件夹下的所有js文件合并成一个文件  |
|  gulp-connect  |  在gulp-load-plugins的召唤下，可以重新刷新当前页面保证在编辑器中做修改，浏览器自动刷新展示  |
|  gulp-cssmin  |  在gulp-load-plugins的召唤下，可以压缩生成的css文件，在生产环境下的css文件需要进行压缩  |
|  gulp-imagemin  |  在gulp-load-plugins的召唤下，可以压缩生成的image文件，在生产环境下的image文件需要进行压缩  |
|  gulp-less  |  在gulp-load-plugins的召唤下，可以编译less文件生成正常的css文件  |
|  gulp-uglify  |  在gulp-load-plugins的召唤下，可以压缩生成的js文件，在生产环境下的js文件需要进行压缩  |
|  open  |  可以打开配置好的对应端口网页|

> 配置好的`package.json`

最后放上安装好的配置，可以直接把我这边配置好的`package.json`的`devDependencies`内容直接拿过去用，然后直接执行`npm install`就好，或者你使用的是淘宝镜像，执行`cnpm install`就好。

```json
  "devDependencies": {
    "gulp": "^3.9.1",
    "gulp-load-plugins": "^1.5.0",
    "gulp-clean": "^0.3.2",
    "gulp-concat": "^2.6.1",
    "gulp-connect": "^5.0.0",
    "gulp-cssmin": "^0.2.0",
    "gulp-imagemin": "^3.3.0",
    "gulp-less": "^3.3.2",
    "gulp-uglify": "^3.0.0",
    "open": "0.0.5"
  }
```

## 3.5 编写相关gulp命令

在当前项目的根目录下新建一个`gulpfile.js`，请注意文件名一定要正确，并编写相关`gulp`指令

```javascript
    var gulp =require('gulp');//调用总指令
    var $ = require('gulp-load-plugins')();
    //请注意一定要写后面这个空括号对，代表直接调用这个函数
    var open =  require('open');

    var app ={
        srcPath:'src/',//默认需要做处理的原始文件夹路径
        devPath:'build/',//开发环境文件夹名字
        proPath:'dist/'//生产环境文件夹名字
    }
    /*
    gulp.task(taskName,callback);
    */
    gulp.task('lib',function(){
        gulp.src('lib/**/*.min.js')
        /*
        获取bower安装包路径二级目录下所有已经压缩过的js，
        色
        请注意如果你之前没有使用bowerrc文件修改，
        这里的lib文件名应该是默认的bower_components，
        vendor是供应商的意思，这个名字不是固定的，可换。
        */
        .pipe(gulp.dest(app.devPath+'vendor'))//复制文件到开发环境
        .pipe(gulp.dest(app.proPath+'vendor'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('html',function(){
        gulp.src(app.srcPath+'**/*.html')//获取src文件夹下所有的html文件
        .pipe(gulp.dest(app.devPath))//复制文件到开发环境
        .pipe(gulp.dest(app.proPath))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('json',function(){
        gulp.src(app.srcPath+'data/**/*.json')//
        /*
        因为不连接数据库，需要做数据mock，获取moock文件夹下所有的json文件，
        如果直接连接数据库的话，就不用写 这个任务
        */
        .pipe(gulp.dest(app.devPath+'data'))//复制文件到开发环境
        .pipe(gulp.dest(app.proPath+'data'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });
    /*MDUI大法好  以md开头的任务都是我为MDUI大法写的，如果你不用这个样式库可以直接忽略*/
    gulp.task('mdcss',function(){
        gulp.src('lib/mdui/src/mdui.less')//这个lib文件夹注意对应你本地的bower安装包路径
        .pipe($.less())//编译less成对应的css文件
        .pipe(gulp.dest(app.devPath+'css'))//复制文件到开发环境
        .pipe($.cssmin())//生产环境的样式文件需要压缩生成的
        .pipe(gulp.dest(app.proPath+'css'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('mdfont',function(){
        gulp.src('lib/mdui/dist/fonts/**/*')//这个lib文件夹注意对应你本地的bower安装包路径
        .pipe(gulp.dest(app.devPath+'fonts'))//复制文件到开发环境
        .pipe(gulp.dest(app.proPath+'fonts'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('mdicon',function(){
        gulp.src('lib/mdui/dist/icons/**/*')
        /*
        这个lib文件夹注意对应你本地的bower安装包路径,
        注意这个还有一个坑，就是mdui下的字体图标路径相对不是fonts下，
        原本的相对路径是../icons/material-icons/
        如果你想和我一样偷懒，把所有字体文件放到fonts下，
        需要修改lib/mdui/src/icon/less/material-icons.less文件，
        将字体文件路径都修改为 ../fonts/material-icons/，
        */
        .pipe(gulp.dest(app.devPath+'fonts'))//复制文件到开发环境
        .pipe(gulp.dest(app.proPath+'fonts'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });
    /*MDUI大法相关任务完结*/
    gulp.task('less',function(){
        gulp.src(app.srcPath+'style/index.less')//复制在src下我们自己定义样式的总less文件，注意在该文件中，导入其他自定义样式less文件
        .pipe($.less())//编译less成对应的css文件
        .pipe(gulp.dest(app.devPath+'css'))//复制文件到开发环境
        .pipe($.cssmin())//生产环境的样式文件需要压缩生成的
        .pipe(gulp.dest(app.proPath+'css'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('js',function(){
        gulp.src(app.srcPath+'script/**/*.js')//复制在src下我们自己写的所有js文件，注意指明文件格式
        .pipe($.concat('index.js'))//把所有的js文件都整合成一个index.js文件
        .pipe(gulp.dest(app.devPath+'js'))//复制文件到开发环境
        .pipe($.uglify())//生产环境的js文件需要压缩生成的
        .pipe(gulp.dest(app.proPath+'js'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('image',function(){
        gulp.src(app.srcPath+'image/**/*')//复制在src下所有图片文件
        .pipe(gulp.dest(app.devPath+'image'))//复制文件到开发环境
        .pipe($.imagemin())//生产环境的图片文件需要压缩生成的
        .pipe(gulp.dest(app.proPath+'image'))//复制文件到生产环境
        .pipe($.connect.reload());//只要编译命令执行就刷新页面
    });

    gulp.task('build',['image','js','mdcss','mdfont','mdicon','less','lib','html','json']);

    gulp.task('serve',['build'],function(){
        $.connect.server({
            root:[app.devPath],//默认的环境是开发环境，可以成修改成生产环境 app.proPath
            livereload:true,//是否实时监听，这个需要结合谷歌插件
            port:1234//端口号，只要配置未被占用的端口号就行
        });
        open('http://localhost:1234');//自动打开绑定的端口界面

        gulp.watch(app.srcPath+'script/**/*.js',['js']);//监听自定义的js改动情况
        gulp.watch(app.srcPath+'lib/**/*.js',['lib']);//监听加载其他插件的js改动情况
        gulp.watch(app.srcPath+'**/*.html',['html']);//监听自定义的html改动情况
        gulp.watch(app.srcPath+'data/**/*.json',['json']);//监听mook数据的改动情况
        gulp.watch(app.srcPath+'lib/mdui/src/mdui.less',['mdcss']);//监听MDUI的样式文件的改动情况
        gulp.watch(app.srcPath+'lib/mdui/dist/fonts/**/*',['mdfont']);//监听MDUI的主要字体文件的改动情况
        gulp.watch(app.srcPath+'lib/mdui/dist/icons/**/*',['mdicon']);//监听MDUI的图标字体文件的改动情况
        gulp.watch(app.srcPath+'style/index.less',['less']);//监听自定义的样式文件改动情况
        gulp.watch(app.srcPath+'image/**/*',['image']);//监听图片文件改动情况
    });

    gulp.task('default',['serve']);//gulp默认执行的命令会执行的任务，即直接输入gulp就会执行的任务

    gulp.task('clean',function(){
        gulp.src([app.devPath,app.proPath])
        /*
        当你觉得生产和开发环境中的文件中生成的错误文件比较多，
        可以直接清理相关文件夹 可以执行该任务
        */
        .pipe($.clean());
    });
```

编写完成之后可以直接执行`gulp`命令就可以直接在生产和开发环境中生成对应文件，并且`自动`打开对应网页界面，当然，也可以单独执行一下执行，都是可以单独运行。

```bash
    gulp
    gulp lib
    gulp html
    gulp json
    gulp mdcss
    gulp mdfont
    gulp mdicon
    gulp less
    gulp image
    gulp clean
```

## 3.6 开始写界面

### 3.6.1 hello World

在`src`文件夹下新建`index.html`,当然也可以是其他名字，但是一般默认的就主页面名字就写`index`,添加相应的样式文件和js文件，写一个`hello World`，通过`gulp`指令，页面就自动打开在眼前，如果页面顺利打开，并且控制台没有任何报错，对应文件下所有文件都是正确生成，那么就继续往下走，如果控制台有报错，请往前看，是否有没有注意的细节。

> src/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>angular-webapp</title>
    <link rel="stylesheet" href="css/mdui.css"><!--导入mdui样式文件-->
</head>
<body ng-app="myApp"><!--告诉angular这个范围的内容，都可以用ng指令，你注意ng-scope-->
  <div class="mdui-container">
    <div class="mdui-typo-display-4-opacity">hello World</div>
  </div>
</body>
<script src="vendor/angular/angular.min.js"></script><!--导入angular JS文件-->
<script src="js/index.js"></script><!--一定要记得调用，要不然angular会召唤不成功-->
</html>
```

> src/script/app.js

```javascript
  "use strict";//使用严格模式
  //angular接收的第一个参数需要和index.html中的ng-app声明的值要一致。
  var app = angular.module('myApp',[]);
```

### 3.6.2 测试相关功能

- 保证控制台没有任何报错
- 在编辑器中修改`src`下的网页或者其他文件内容，浏览器中的内容是否正常刷新
- 测试`gulp`相关指令是否都可以正常执行
- 保证生产环境和开发环境中的相关js、css和html等都是正常生成，并且生产环境中的文件进行了相应压缩
- 测试`angular`是否被正常召唤，一般召唤成功的话，在页面所有标签下都会新增`ng-scope`样式

### 3.6.3 了解路由注意事项

```javascript
'/home':只匹配'/home'

'/mood/:id'、'/mood/{id}':匹配'/mood/1234'，或者'/mood/'

'/setting?before&after'：非rest传参
```

### 3.6.4 开始写使用路由的demo

- `src/index.html`网页加入`angular-ui-router.min.js`文件，这个具体路径看实际开发环境文件夹中的Index页和这js文件的相对路径。
- `src/index.html`网页加入`index.css`文件，加入自定义的样式文件
- 编写测试的路由页面，我这边是写了四个路由页面
- `src/script/app.js`，中引用`ui.router`，告诉`angular`，可以使用第三方的路由啦。
- `src/script/config/router.js`，中编写实际路由相关内容。

### 3.6.4 路由测试成功，放上所有文件

> src/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>angular-webapp</title>
    <link rel="stylesheet" href="css/mdui.css"><!--导入mdui样式文件-->
    <link rel="stylesheet" href="css/index.css"><!--导入自定义样式文件-->
</head>
<body ng-app="myApp"><!--告诉angular这个范围的内容，都可以用ng指令，你注意ng-scope-->
    <div class="mdui-bottom-nav mdui-bottom-nav-text-auto mdui-bottom-nav-scroll-hide mdui-color-blue">
        <!--ui-sref-active设置路由激活样式，这个结合实际使用的框架设置对应的样式名，这边我用的是mdui中面板激活的样式名。
				ui-sref设置路由地址，路由地址必须要已经配置好的的，ng-animate设置路由视图展示动画效果"-->
        <a href="javascript:void(0);" ui-sref-active="mdui-bottom-nav-active" class="mdui-ripple mdui-ripple-white" ui-sref="home">
            <i class="mdui-icon material-icons">home</i>
            <label>主页</label>
        </a>

        <a href="javascript:void(0);" class="mdui-ripple mdui-ripple-white" ui-sref="pic">
            <i class="mdui-icon material-icons">picture_in_picture</i>
            <label>美图</label>
        </a>
        <a href="javascript:void(0);" class="mdui-ripple mdui-ripple-white" ui-sref="mood">
            <i class="mdui-icon material-icons">mood</i>
            <label>心情</label>
        </a>

        <a href="javascript:void(0);" class="mdui-ripple mdui-ripple-white" ui-sref="setting">
            <i class="mdui-icon material-icons">settings</i>
            <label>设置</label>
        </a>
    </div>
   <ui-view  class="mdui-container" ng-animate="slide"></ui-view>
</body>
<script src="vendor/angular/angular.min.js"></script><!--导入angular JS文件-->
<script src="vendor/angular-ui-router/release/angular-ui-router.min.js"></script><!--导入angular-ui-router.min.js文件-->
<script src="vendor/mdui/dist/js/mdui.min.js"></script><!--导入mdui.min.js文件-->
<script src="js/index.js"></script>
</html>
<!--因为是做测试，所以，这边四个路由页面，都是在src/view文件夹下直接新建网页文件，随便在body中写内容，就不放上来了-->
```

> src/script/app.js

```javascript
"use strict";
  //angular接收的第一个参数需要和index.html中的ng-app声明的值要一致。
  var app = angular.module('myApp',['ui.router']);//可以导入多个三方插件，注意对应插件的名字
```

> src/script/config/router.js

```javascript
    //请注意app这个变量是app.js中定义的变量名，请注意这两个变量名的一致
    //'$stateProvider','$urlRouterProvider'是为了更好的语义化，所以写的全名，只要注意和后面回调函数的参数名要一致
    app.config(['$stateProvider','$urlRouterProvider',function($stateProvider,$urlRouterProvider){
        $stateProvider.state('home',{
            url: '/home',//子路由的虚拟路径名，这个要和路径title要一致即传入state函数的第一个参数名
            templateUrl: 'view/home.html',//子路由的页面地址
            controller: 'homeCtrl'//子路由的controller名，注意和下面controller中要一致
        }).state('mood',{
            url: '/mood',//子路由的虚拟路径名，这个要和路径title要一致即传入state函数的第一个参数名
            templateUrl: 'view/mood.html',//子路由的页面地址
            controller: 'moodCtrl'//子路由的controller名，注意和下面controller中要一致
        }).state('pic',{
            url: '/pic',//子路由的虚拟路径名，这个要和路径title要一致即传入state函数的第一个参数名
            templateUrl: 'view/pic.html',//子路由的页面地址
            controller: 'picCtrl'//子路由的controller名，注意和下面controller中要一致
        }).state('setting',{
            url: '/setting',//子路由的虚拟路径名，这个要和路径title要一致即传入state函数的第一个参数名
            templateUrl: 'view/setting.html',//子路由的页面地址
            controller: 'settingCtrl'//子路由的controller名，注意和下面controller中要一致
        });
        $urlRouterProvider.otherwise('home');//设置默认的路由页面
    }]);

    app.controller('homeCtrl', function ($scope, $state) {
        $scope.changeState = function () {
            $state.go('/home');//点击该路由，激活的页面地址，请注意和上文中controller对应的url要一致
        };
    });
    app.controller('moodCtrl', function ($scope, $state) {
        $scope.changeState = function () {
            $state.go('/mood');//点击该路由，激活的页面地址，请注意和上文中controller对应的url要一致
        };
    });
    app.controller('picCtrl', function ($scope, $state) {
        $scope.changeState = function () {
            $state.go('/pic');//点击该路由，激活的页面地址，请注意和上文中controller对应的url要一致
        };
    });
    app.controller('settingCtrl', function ($scope, $state) {
        $scope.changeState = function () {
            $state.go('/setting');//点击该路由，激活的页面地址，请注意和上文中controller对应的url要一致、
        };
    });
```

## 3.7 后续添加

# 4 参考网站

- [node官网](https://nodejs.org/en/)
- [angular2官网](https://angularjs.org/)
- [angular4官网](https://angular.io/)
- [angular中文社区](http://www.angularjs.cn/)
- [Bower官网](https://bower.io/)
- [使用Bower进行前端依赖管理](http://www.cnblogs.com/nickai/p/5864898.html)
- [gulp官网](http://www.gulpjs.com.cn/docs/getting-started/)
- [gulp详细入门教程](http://www.cnblogs.com/horanly/p/6596415.html)
- [less官网](http://lesscss.org/)
- [less中文官网](http://lesscss.cn/)
- [LESS CSS 框架简介](https://www.ibm.com/developerworks/cn/web/1207_zhaoch_lesscss/)
- [LESS CSS 框架简介](https://www.ibm.com/developerworks/cn/web/1207_zhaoch_lesscss/)
- [LESS在线编辑器](http://tool.oschina.net/less)