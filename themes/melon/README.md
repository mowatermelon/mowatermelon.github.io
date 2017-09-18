# hexo-theme-melon

# 1 前言

这个是基于hexo-theme-yilia主题之外进行了一定订制，修改了主题的默认的tag、高亮和title等的一些样式，并且集成了gitment评论插件，可以去[我的博客](https://mowatermelon.github.io/)查看实际效果

>  Yilia 是为 hexo 2.4+制作的主题。 崇尚简约优雅，以及极致的性能。  可以去[原作者的博客](http://litten.me/) 查看效果。

# 2 开发者

如果想要做其他订制修改，请参考原作者的[修改说明](https://github.com/litten/hexo-theme-yilia/wiki/Yilia源码目录结构及构建须知)。

# 3 使用

> 安装
```bash
$ git clone https://github.com/mowatermelon/hexo-theme-melon.git themes/melon
```

> 配置

修改hexo根目录下的 _config.yml ： theme: melon

> 更新
```bash
cd themes/melon
git pull
```

# 4 完整配置说明

```bash
# Header

menu:
  主页: /
  #menu1: /categories/menu1/
  #js学习: /categories/js学习/
  #软件折腾: /categories/软件折腾/
  #样式学习: /categories/样式表/
  #近期文字: /archives/2017/05

# SubNav
# 如果你想将网站与某个你的个人账户管理显示，正确配置之后，就放开对应的账号前面的  # 号
subnav:
  github: "https://github.com/mowatermelon"
  #weibo: "#"
  #rss: "#"
  zhihu: "https://www.zhihu.com/people/wu-mo-61-63/activities"
  #qq: "#"
  #weixin: "#"
  #jianshu: "#"
  #douban: "#"
  #segmentfault: "#"
  #bilibili: "#"
  #acfun: "#"
  #mail: "mailto:neefoxmo@gmail.com"
  #facebook: "#"
  #google: "#"
  #twitter: "#"
  #linkedin: "#"

rss: /atom.xml

# 是否需要修改 root 路径
# 如果您的网站存放在子目录中，例如 http://yoursite.com/blog，
# 请将您的 url 设为 http://yoursite.com/blog 并把 root 设为 /blog/。
root:

# Content

# 文章太长，截断按钮文字
excerpt_link: 'read more'
# 文章卡片右下角常驻链接，不需要请设置为false，如果已经设置了文章截断，不需要设置这个打开这个参数
show_all_link: false
# 数学公式
mathjax: false
# 是否在新窗口打开链接
open_in_new: false

# 打赏
# 打赏type设定：0-关闭打赏； 1-文章对应的md文件里有reward:true属性，才有打赏； 2-所有文章均有打赏
reward_type: 0
# 打赏wording
reward_wording: 'watermelon lalala~~~'
# 支付宝二维码图片地址，跟你设置头像的方式一样。比如：/assets/img/alipay.jpg
alipay:
# 微信二维码图片地址
weixin:

# 目录
# 目录设定：0-不显示目录； 1-文章对应的md文件里有toc:true属性，才有目录； 2-所有文章均显示目录
toc: 1
# 根据自己的习惯来设置，如果你的目录标题习惯有标号，置为true即可隐藏hexo重复的序号；否则置为false
toc_hide_index: true
# 目录为空时的提示
toc_empty_wording: '目录君被吃掉了，好可怜555555'

# 是否有快速回到顶部的按钮
top: true

# Miscellaneous
# baidu_analytics 统计用户id  可以到 https://tongji.baidu.com/web/register    进行申请，一般是十六位的数字字母结合一个字符串
#                 然后就可以在 https://tongji.baidu.com/web/welcome/login  登陆后看到网站的流量详情了
# google_analytics 你的跟踪ID  请到 https://analytics.google.com/analytics/web/?authuser=0#provision/CreateAccount/ 页面申请，一般是通过中横线分为三段一个字符串，除了第一段是字母，后面两段都是纯数字
#                 然后就可以在 https://analytics.google.com/analytics/web/  登陆后看到网站的流量详情了，这个需要谷歌账号翻墙来着才能看
# 默认集成的谷歌分析
baidu_analytics: ''
google_analytics: ''
favicon: /favicon.png

# 你的头像url，
# 可以是你github的图像地址，如果不知道可以去https://api.github.com/users/{your-github-name}查看相关信息
# 也可以是相对主页面的img图片地址
avatar:

# 是否开启分享
share_jia: false

# 评论：1、Gitment ，2、畅言；3、Disqus ； 不需要使用某项，直接设置值为false，或注释掉
# 多说和网易云跟帖已经关了，畅言注册需要网站备案，Disqus被墙了，而且样式感觉一般
# 我主要这边默认已经将gitment的样式集成到项目中了，如果想要修改就在当前根目录执行 npm install，安装相关包之后，
# 在修改了source-src/css/comment.scss之后，执行npm run dist，就可以重新编译一遍了

# 1 Gitment
# 插件作者官方说明: https://imsun.net/posts/gitment-introduction/
# 也直接去可以去https://github.com/settings/applications/new  申请你自己的相关id和Secret信息
# 设置enable为true之后，需要先登录账号，对gitment评论框进行初始化，才可以用，本地是不能测试评论功能的
#  enable: false
#  githubID: #{your-github-name}
#  repo: #{your-github-name}.github.io
#  ClientID: #{your-ClientID}
#  ClientSecret: #{your-ClientSecret}
gitment:
  enable: false
  githubID:
  repo:
  ClientID:
  ClientSecret:

# 2、畅言
changyan_appid: false
changyan_conf: false

# 3、Disqus 在hexo根目录的config里也有disqus_shortname字段，优先使用yilia的
disqus: false


# 样式定制 - 一般不需要修改，除非有很强的定制欲望…
style:
  # 头像上面的背景颜色
  header: '##00bcd4'
  # 右滑板块背景
  slider: 'linear-gradient(200deg,#a0cfe4,#e8c37e)'

# slider的设置
slider:
  # 是否默认展开tags板块
  showTags: false

# 显示在主页右侧栏的智能菜单
# 如不需要，将该对应项置为false，这个一般推荐配置
# 比如
# smart_menu:
#  innerArchive: '所有文章'
#  friends: '文字分类'
#  aboutme: '关于我'
smart_menu:
  innerArchive: false
  friends: false
  aboutme: false

friends:

  friends_url_01: #/categories/friends_url_01/
  friends_url_02: #/tags/friends_url_02/

# aboutme 页面对应的文本内容
aboutme: welcome to my home

```


# 5 如果想要加入第三方的js
现将三方的js放到`source-src/js/`文件夹中，然后修改`source-src/script.ejs`，举个栗子，你想加入的地方的`js`名字叫`demo`。

```java
    <% if (asset.indexOf('slider') >= 0) { %>
      <% var slider = asset %>
      <% } %>
      <% if (asset.indexOf('gitment') >= 0) { %>
      <% var gitment = asset %>
      <% } %>
      <% if (asset.indexOf('gitment') >= 0) { %>
      <% var gitment = asset %>
      <% } %>
      //添加其他三方js
      <% if (asset.indexOf('demo') >= 0) { %>
      <% var demo = asset %>
      <% } %>
      
    <% } %>
    loadScript("<%= left %>config.root<%= right %><%= right2 %><%= slider %>")
    loadScript("<%= left %>config.root<%= right %><%= right2 %><%= demo %>")
```

# 6 欢迎前来进行交流沟通
