---
title: 框架学习之hexo建blog
category: 框架学习
tags:
  - node
  - github page
  - hexo
  - vscode
  - markdown
  - 框架学习
date: 2017-09-12 14:29:17
---
# 1. 了解hexo

> A fast, simple & powerful blog framework
一个快速，简单和强大的博客框架

放上[官网](https://hexo.io/)

<!--more-->

# 2. 所需要的使用环境

## 2.1. 软件环境

### 2.1.1 markdown编辑器

推荐[vscode](https://code.visualstudio.com/Download)，一个颜值比较赞的编辑器，支持`多种语言`开发环境，主要是对于`markdwon`的插件也多，支持`git`版本管理或者`svn`版本管理，而且软件启动快，也支持多个终端命令行，记得安装相关以下推荐插件。

> Auto-Open Markdown Preview

  你打开一个`markdown`文件，右侧会对当前文件进行预览显示。

> Markdown Preview Github Style

  你打开一个`markdown`文件，预览效果与你在`Github`上的预览效果是一样的，`VSCODE`上默认的预览高亮不会改变背景颜色，只会改变字体颜色，还有和平常使用`atom`预览的效果有很多不同，所以你如果要用`VSCODE`写`markdown`，建议要安装这个。

> markdownlint

  管理现有markdown的格式正确性

> terminal

  支持多中命令的终端命令行

### 2.1.2 node

放上[安装地址](https://nodejs.org/en/)，这个安装过程就可以一路`next`就好，当然你如果有`强迫症`要改变安装路径，记得修改安装地址，但是`一定`要记住`安装路径`，然后将`安装路径`下的`node_global`文件夹，或者`指令安装`的配置到`环境变量`中(`计算机-->右键属性-->高级系统设置-->环境变量`)，对于`node`不一定要下载最新的版本，可以下载的`LTS`稳定版本，截止到`20170918`，`node`官网显示的最稳定的版本是`v6.11.3` 。

举个配置`环境变量`的栗子，我公司电脑系统盘是`D盘`，软件安装在系统盘，这边的默认`全局安装路径`是`D:\Program Files\nodejs\node_global`，但是我家中的电脑，系统盘是`C盘`，软件不是安装在系统盘，所以`全局安装`之后的安装路径是`C:\Users\Administrator\AppData\Roaming\npm`。

```bash
# 在node cmd中进行全局安装，将安装地址更换为国内的淘宝镜像地址
D:\Users\Administrator>npm i cnpm -g --registry=https://registry.npm.taobao.org

# 在vscode终端中输入以下指令，如果能够正常输出版本号，就是安装成功

PS x:\xx\xxxx>node -v
v6.9.4

PS x:\xx\xxxx>npm -v
3.10.10

PS x:\xx\xxxx>cnpm -v
cnpm@5.1.1 (D:\Program Files\nodejs\node_global\node_modules\cnpm\lib\parse_argv.js)
npm@5.4.1 (D:\Program Files\nodejs\node_global\node_modules\cnpm\node_modules\npm\lib\npm.js)
node@6.9.4 (D:\Program Files\nodejs\node.exe)
npminstall@3.1.4 (D:\Program Files\nodejs\node_global\node_modules\cnpm\node_modules\npminstall\lib\index.js)
prefix=D:\Program Files\nodejs\node_global
win32 x64 6.1.7601
registry=http://registry.npm.taobao.org
```

一定要保证`cnpm -v`可以在`vscode`终端中正常执行，要不然后续通过`hexo`指令新建`blog`，会一直显示`hexo`指令未定义的。

### 2.1.3 github

- 注册`github`账号。
- 新建一个`{注册呢称}.github.io`的仓库。

- 进入新建好的仓库`Settings`，找到`GitHub Pages`，设置`Source`下的`page`页所处的`branch`，这个一般就选择`master`，然后选择`Save`。

成功之后该页面会显示

```bash
Your site is published at https://{注册呢称}.github.io/

Your GitHub Pages site is currently being built from the master branch. Learn more.
```

- 页面上可以直接选择`Jekyll theme`，随便选择一个主题，在浏览器中输入`https://{注册呢称}.github.io/`，看是否能够正常预览界面。
- 下载[github](https://desktop.github.com/)客户端，在安装过程中记得不要一路点击`next`，其中有一步是询问`git`指令是全局安装还是仅能在`git shell`或者`git bash`中运行，软件默认是第一个，指令只能在`git shell`或者`git bash`中运行，请选择第二个，`git`指令所有的`命令行工具`都可以运行。`20170913`的最新版`vscode`支持`powershell`，`cmd`和`bash`终端命令行，这个限制可以不用管了。

```bash
# 在vscode终端中验证git指令能不能全局执行
PS x:\xx\xxxx>git --version
git version 2.10.2.windows.1
```

验证`git命令`是否能够全局执行，这个很重要，要不然你在`非git`命令行面板中，是不能执行`hexo`将`blog`推送到远程仓库的。

## 2.2. 相关依赖包

  ```bash
  # 在node cmd中进行全局安装，
  cnpm i hexo-cli -g

  # 在vscode终端中输入以下指令，安装成功的效果
  PS x:\xx\xxxx>hexo -v
  hexo-cli: 1.0.3
  os: Windows_NT 6.1.7601 win32 x64
  http_parser: 2.7.0
  node: 6.9.4
  v8: 5.1.281.89
  uv: 1.9.1
  zlib: 1.2.8
  ares: 1.10.1-DEV
  icu: 57.1
  modules: 48
  openssl: 1.0.2j
  ```

`全局安装`之后，会提示`安装路径`，如果该`路径`你之前已经设置成`环境变量`就不用管，但是如果提示的`安装路径`你没有设置过`环境变量`，你就会发现这个`全局安装`的指令一直跑不了，记得把提示的`安装路径`设置成`环境变量`。

## 2.3. hexo初始化

  在文件本地新建测试项目文件，右键在`vscode`中打开
  ```bash
  # 在vscode终端中输入以下指令，安装成功的效果
  PS x:\xx\xxxx>hexo init #博客初始化
  PS x:\xx\xxxx>npm install #安装相关依赖包

  # 成功之后查看blog文件夹中的内容是否正常生成
  PS x:\xx\xxxx>dir
  Mode                LastWriteTime     Length Name
  ----                -------------     ------ ----
  d----         2017/9/12      9:05            .vscode #vscode自动生成的，可以忽略
  d----         2017/9/12      9:06            node_modules #安装相关环境
  d----         2017/9/12      9:06            scaffolds #转化不同layout的markdown文章的模板
  d----         2017/9/12      9:06            source #markdown文章所在地
  d----         2017/9/12      9:06            themes #主题
  -a---         2017/9/12     14:32        174 db.json #source解析所得到的
  -a---          2017/9/3      1:36        721 package.json #项目所需模块项目的配置信息
  -a---          2017/9/8     16:30       2460 _config.yml #博客的主要配置
  ```

## 2.4. 必须要配置的文件

### 2.4.1. 在根目录`_config.yml`里修改配置

```yml
# Site
title: {{你想要显示在网页title上的名称}}
subtitle: {{你想要显示在网页上的座右铭}}
description: {{你想要显示在网页上的描述}}
author: {{你想要显示在网页的呢称}}
language: chinese
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://{{注册呢称}}.github.io/
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

····

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/{{注册呢称}}/{{注册呢称}}.github.io.git
  branch: master

····
```

### 2.4.2. 主题文件夹中`_config.yml`里添加配置

如果没有更换主题的话，就在默认主题`landscape`中的`_config.yml`里添加配置，如果已经更换主题，请在对应的主题文件夹中的`_config.yml`里添加配置。

```yml
# SubNav
# 如果你想将网站与某个你的个人账户管理显示，正确配置之后，就放开对应的账号前面的  # 号
subnav:
  github: "https://github.com/{{注册呢称}}"
  #weibo: "#"
  #rss: "#"
  zhihu: "https://www.zhihu.com/people/{{注册呢称}}/activities"
  #qq: "#"
  #weixin: "#"
  #jianshu: "#"
  #douban: "#"
  #segmentfault: "#"
  #bilibili: "#"
  #acfun: "#"
  #mail: "mailto:{{你的呢称}}"
  #facebook: "#"
  #google: "#"
  #twitter: "#"
  #linkedin: "#"
```

## 2.5. 预览效果

```bash
  # 现在本地预览效果
  PS x:\xx\xxxx>hexo s --watch
  INFO  Start processing
  INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.

  # 如果本地blog内容已经修改完成，生成本地静态文件，上传到github上去
  PS x:\xx\xxxx>hexo d -g
```

在浏览器中输入`https://github.com/{注册呢称}/{注册呢称}.github.io`，查看文件是否上传成功，如果全部上传成功，这个仓库下的文件内容应该和本地的`public`中的文件一模一样。然后在浏览器中输入`https://{注册呢称}.github.io/`，看是否能够看到`blog`相关内容。

# 3. 可能遇见的问题

## 3.1 git指令无效

  环境变量没有正确配置，请将git路径所在文件夹，配置到环境变量中

## 3.2 hexo指令无效

  环境变量没有正确配置，请将hexo路径所在文件夹，配置到环境变量中

## 3.3 上传到github上之后页面404

  查看上传文件中没有`index.html`，如果没有请检查一下本地根目录的`package.json`文件，看一下安装包是否完整，如果不完整的话，请在vscode中执行`cnpm i --save {{你缺少的依赖包}}`，一定要记得写`--save`，这样依赖包安装才会保存到`package.json`，避免以后重复安装。
  ```json
    "dependencies": {
    "hexo": "^3.2.0",
    "hexo-deployer-git": "^0.3.1",
    "hexo-deployer-openshift": "^0.1.2",
    "hexo-deployer-rsync": "^0.1.3",
    "hexo-generator-archive": "^0.1.4",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-feed": "^1.2.0",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-sitemap": "^1.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.0",
    "hexo-renderer-marked": "^0.3.0",
    "hexo-renderer-stylus": "^0.3.1",
    "hexo-server": "^0.2.2"
  }
  ```

## 3.4 不知道怎么更换主题

  [官方主题shop](https://hexo.io/themes/)，你可以选择你想要的主题，每个主题的`readme.md`中都有相关说明，日常摊手.jpg，我肯定是要拿自己改写的主题做例子，我主题的名称是`melon`，如果大家对这个主题有什么好的建议，可以直接这个仓库下提`issues`进行相关建议。

  > 安装
  ```bash
  # 在vscode终端中输入以下指令，这个是在项目根文件夹下执行这个指令
  PS x:\xx\xxxx>git clone {主题github地址} themes/{你想设置的主题名称}
  #举个栗子
  PS x:\xx\xxxx>git clone https://github.com/mowatermelon/hexo-theme-melon.git themes/melon
  ```

  > 配置

  修改`hexo`根目录下的`_config.yml`
  ```yml
  #主题一定要和上文对应
  theme: {你想设置的主题名称}
  #举个栗子
  theme: melon
  ```
  > 主题更新
  ```bash
  #主题一定要和上文对应
  cd themes/{你想设置的主题名称}
  git pull
  #举个栗子
  cd themes/melon
  git pull
  ```

## 3.5 全局安装了hexo但是命令无效

我最近电脑刚换了系统（2017-11-23），全局安装的`hexo`是比较新的，全局安装完成之后，我在`cmd`中执行`hexo -v`，是正常的，但是在进入`blog`所在文件夹的时候，`hexo s --watch`指令不能正常使用，当时以为我打开文件夹的方式不对，最后测试得出，是一个`hexo`相关环境包`hexo-deployer-heroku`有问题，主要问题是`hexo-deployer-heroku`所依赖包中一个叫`swig`的包已经找不到了，所以这边找`hexo-deployer-heroku`的就找不到，然后导致`hexo`看到自己所依赖的包找不到，特别委屈巴巴，他就不想运行了，把`package.json`中`hexo-deployer-heroku`删掉就好了。

这次错误主要是我使用指令的时候一般只关注`error`，不关注`warning`，其实在将远程仓库`clone`到本地之后，使用`cnpm install`的时候，就看到安装了17个环境包，没有关注下面的`warning`，再次执行`cnpm install`，`warning`不会再次出现，所以在第一次`warning`警告出现的时候，就需要仔细看一下，可能以后就不出现了，那之后就发现不了问题实质了。

# 4. hexo的相关指令和参数

## 4.1 Front-matter

`Front-matter` 是文件最上方以 `---` 分隔的`区域`，用于指定个别文件的变量，举例来说：

```yaml
title: Hello World
date: 2013/7/13 20:46:25
---
```

以下是默认提供的参数，可以将这些参数添加到`scaffolds/**.md`中。

|   预定参数   |   描述   |   默认值
|:---|:---|:---|
|   layout   |   布局   |      |
|   title   |   标题   |      |
|   date   |   建立日期   |   文件建立日期   |
|   updated   |   更新日期   |   文件更新日期   |
|   comments   |   开启文章的评论功能   |   true   |
|   tags   |   标签（不适用于分页）   |      |
|   categories   |   分类（不适用于分页）   |     |
|   permalink   |   覆盖文章网址   |     |

## 4.2 默认指令

```bash
Usage: hexo <command>
```

> Commands:

|   可选参数名   |   官方解释   |   个人解读   |
|:---|:---|:---|
|   hexo clean   |   Remove generated files and cache.   |   清除所有生成的网页文件夹和数据缓存，主要是清除项目中`hexo -g`生成的`public`文件夹中内容，或者通过`hexo s  --watch`生成网站的一些`数据缓存`   |
|   hexo config   |   Get or set configurations.   |   获取当前的hexo所有配置   |
|   hexo deploy   |   Deploy your website.   |   将本地的`blog`推送到对应的`git仓库`，使用缩写`d`也可以执行，一般执行`hexo d -g`   |
|   hexo generate   |   Generate static files.   |   将本地静态`md`文件生成对应的静态`blog`文件，使用缩写`g`也可以执行，本地预览的时候一般执行`hexo g --watch`，也会结合deploy，如`hexo g -d`，一键生成和部署，生成的文件一般在本地项目`public`文件夹中   |
|   hexo help   |   Get help on a command.   |   当对某个指令用法不太清楚的时候，可以用这个指令   |
|   hexo init   |   Create a new Hexo folder.   |   hexo的初始化，自动下载默认的博客主题和相关依赖包   |
|   hexo list `type`   |   List the information of the site   |   列出当前文件夹的文件列表，type的类型可以为 `page`, `post`, `route`, `tag`, `category`，`type`参数为必填参数  |
|   hexo migrate `type` `source`  |   Migrate your site from other system to Hexo.   |   从其他blog系统迁移到hexo blog，目前需要通过指令迁移的支持的`type`参数是`joomla`、`rss`和`wordpress`，详细说明请看`4.3.2`  |
|   hexo new `layout` `title`  |   Create a new post.   |   生成规定`layout`和规定`title`的`md`文件，`layout`可以是`post`, `page`, `draft` or `whatever you want`，`title`是生成的md文件名，内容可以是`whatever you want`，但是请注意使用英文名，也不要出现太多奇怪符号。   |
|   hexo publish `layout` `filename`  |   Moves a draft post from _drafts to _posts folder.   |   将md文件从`draft`中发布成`post`模版格式，在`post`中的md文件在执行`hexo s`时在页面才会被看到，`layout`参数为`选填参数`，默认是`draft`，`filename`参数为必填参数，文件名必须是`source/_drafts`中已经存在的文件名  |
|   hexo render   |   Render files with renderer plugins.   |   强制将文件进行渲染，可参考4.3.1   |
|   hexo server   |   Start the server.   |   启动hexo本地服务，在本地查看网页运行效果，并且实时监听页面变化，可以简写成`hexo s --watch`   |
|   hexo version   |   Display version information.   |   查看本地hexo版本，还可以写成`hexo v`或者`hexo -v`   |

> Global Options:

|   可选参数名   |   官方解释   |   个人解读   |
|:---|:---|:---|
|   --config   |   Specify config file instead of using _config.yml   |   展示`_config.yml`的配置内容   |
|   --cwd   |   Specify the CWD   |   目前不理解   |
|   --debug   |   Display all verbose messages in the terminal   |   会把运行过程中的内容记录到debug.log   |
|   --draft   |   Display draft posts   |   显示文章草稿   |
|   --safe   |   Disable all plugins and scripts   |   禁用所有插件和脚本   |
|   --silent   |   Hide output on console   |   隐藏在控制台输出   |

## 4.3 复杂指令的说明

### 4.3.1 手动渲染文章格式（目前没有发现有什么用）

```bash
  PS x:\xx\xxxx>hexo render <file1> [file2] ...
```

> Description:

Render files with renderer plugins (e.g. Markdown) and save them at the specified path.

> Options:

|   备选参数名   |   官方解释   |   个人解读   |
|:---|:---|:---|
|   --engine   |   Specify render engine   |   自定义渲染引擎   |
|   --output   |   Output destination. Result will be printed in the terminal if the output destination is not set.   |   指令执行时的默认在终端打印的提示文本内容   |
|   --pretty   |   Prettify JSON output   |   将文件中的json进行格式化输出   |

### 4.3.2 如何从其他blog系统进行迁移

> RSS

首先，安装 `hexo-migrator-rss` 插件。

```bash
  PS x:\xx\xxxx>npm install hexo-migrator-rss --save
```

插件安装完成后，执行下列命令，从 `RSS` 迁移所有文章。`source` 可以是`文件路径`或`网址`。

```bash
  PS x:\xx\xxxx>hexo migrate rss <source>
```

> Jekyll

把 `_posts` 文件夹内的所有文件复制到 `source/_posts` 文件夹，并在 `_config.yml` 中修改 `new_post_name` 参数。

```YML
new_post_name: :year-:month-:day-:title.md
```

> Octopress

把 `Octopress`中`source/_posts` 文件夹内的所有文件转移到 `Hexo` 的 `source/_posts` 文件夹，并修改 `_config.yml` 中的 `new_post_name` 参数。

```YML
new_post_name: :year-:month-:day-:title.md
```

> WordPress

首先，安装 `hexo-migrator-wordpress` 插件。

```bash
  PS x:\xx\xxxx>npm install hexo-migrator-wordpress --save
```

在 `WordPress` 仪表盘中导出数据`(“Tools” → “Export” → “WordPress”)`（详情参考WP支持页面）。

插件安装完成后，执行下列命令来迁移所有文章。`source` 可以是 `WordPress` 导出的`文件路径`或`网址`。

```bash
  PS x:\xx\xxxx>hexo migrate wordpress <source>
```

> __注意__

这个插件并不能完美地实现`WordPress->Hexo`的数据转换，尤其是在处理`WordPress`的分类方面`存在问题`（见`Front-matter`中的分类与标签）。因此，建议您在迁移完成后，手工审阅所有生成的`markdown`文件，检查其中是否有`错误`。对于文章数量较大的`WordPress`站点，这项工作可能要花很长的时间。

> Joomla

首先，安装 `hexo-migrator-joomla` 插件。

```bash
  PS x:\xx\xxxx>npm install hexo-migrator-joomla --save
```

使用 `J2XML` 组件导出 `Joomla` 文章。
插件安装完成后，执行下列命令来迁移所有文章。`source` 可以是 `Joomla` 导出的`文件路径`或`网址`。

```bash
  PS x:\xx\xxxx>hexo migrate joomla <source>
```

### 4.3.3 发布文章

```bash
Usage: hexo new [layout] <title>
```

> Description:

Create a new post.

> Arguments:

|   必要参数名   |   官方解释   |   个人解读   |
|:---|:---|:---|
|   layout   |   Post layout. Use post, page, draft or whatever you want.   |   新建的`md`模板类型，非必写，默认是`draft`   |
|   title   |   Post title. Wrap it with quotations to escape.   |   新建的`md`文件名称，必写   |

> Options:

|   必要参数名   |   官方解释   |   个人解读   |
|:---|:---|:---|
|   -p, --path   |   Post path. Customize the path of the post.   |   自定义生成的文章地址   |
|   -r, --replace   |   Replace the current post if existed.   |   对于已经存在的文件进行重写的时候，直接替换，要不然会新建不成功   |
|   -s, --slug   |   Post slug. Customize the URL of the post.   |   文章缩略名，自定义文章显示的url地址中文章名   |