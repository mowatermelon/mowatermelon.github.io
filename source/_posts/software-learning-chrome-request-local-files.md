---
title: 软件折腾之chrome请求本地文件
category: 软件折腾
tags:
  - chrome
  - 软件折腾
date: 2017-04-16 00:00:00
---

> 今天在做一个demo测试的时候发现谷歌中有如下报错

```javascript
XMLHttpRequest cannot load 
file:///D:/XXX?%20&T=0.2576446940590924.
 Cross origin requests are only supported for protocol schemes: `http`, `data`,` chrome`, `chrome-extension`, `https`.
```

<!-- more -->

报错的意思应该就是`chrome`下，跨域请求只能通过通过这些协议标准实现：`http`、`data`、`https`、`chrom-extension`、`chrom-extension-resource`。

# 1 什么叫跨域(WHAT)？

 字面理解，跨是跨越，域是别的服务器，跨域就是到别的服务器上取东西。  
 只要协议、域名、或端口有任何一个不同，就会被当做是不同的域。

# 2 为何会跨域(WHY)？

  `chrome`在读取本地相对路径脚本时，禁止向第三方请求数据。  
 只要是通过file://方式访问，或者直接拖进浏览器访问，都叫本地运行  
 什么叫`第三方`？那就是不管本地文件、还是服务器url文件都不行。  

# 3 怎么解决(HOW)？

查资料，发现有一种解决方法，不用启动服务器模式，直接更改`chrome`的设置就行。   
> 放上默认的参数 参考官网<https://code.google.com/archive/p/xiaody/wikis/ChromiumCommandLineSwitches.wiki>  

| 序号 | 参数 | 说明 |
|:-------|:-------|:-------| 
| 1 | --allow-outdated-plugins | 不停用过期的插件。|
| 2 | --allow-running-insecure-content | 默认情况下，https 页面不允许从 http 链接引用 javascript/css/plug-ins。添加这一参数会放行这些内容。| 
| 3 | --allow-scripting-gallery | 允许拓展脚本在官方应用中心生效。默认情况下，出于安全因素考虑这些脚本都会被阻止。|
| 4 | --disable-accelerated-2d-canvas | 停用 GPU 加速二维画布。| 
| 5 | --disable-accelerated-video | 停用 GPU 加速视频。|
| 6 | --disable-dart | 停用 Dart。|
| 7 | --disable-desktop-notifications | 禁用桌面通知，在 Windows 中桌面通知默认是启用的。| 
| 8 | --disable-extensions | 禁用拓展。 |
| 9 | --disable-file-system | 停用 FileSystem API。（注意一些拓展如 Adblock Plus for Google Chrome™ 依赖此 API 运行）|
| 10 | --disable-java | 停用 Java。| 
| 11 | --disable-local-storage | 禁用 LocalStorage。 | 
| 12 | --disable-preconnect | 停用 TCP/IP 预连接。| 
| 13 | --disable-remote-fonts | 关闭远程字体支持。SVG 中字体不受此参数影响。| 
| 14 | --disable-speech-input | 停用语音输入。|
| 15 | --disable-sync | 停用同步功能。| 
| 16 | --disable-ssl3 | 停用 SSL v3。| 
| 17 | --disable-web-security | 不强制遵守同源策略，供网站开发人员测试站点使用。| 
| 18 | --disk-cache-dir | 将缓存设置在给定的路径。| 
| 19 | --disk-cache-size | 设置缓存大小上限，以字节为单位。| 
| 20 | --dns-prefetch-disable | 停用DNS预读。| 
| 21 | --enable-print-preview | 启用打印预览。| 
| 22 | --extensions-update-frequency | 设定拓展自动更新频率，以秒为单位。 | 
| 23 | --incognito | 让浏览器直接以隐身模式启动。|
| 24 | --keep-alive-for-test | 最后一个标签关闭后仍保持浏览器进程。（某种意义上可以提高热启动速度，不过你最好得有充足的内存）| 
| 25 | --kiosk | 启用kiosk模式。（一种类似于全屏的浏览模式）| 
| 26 | --lang | 使用指定的语言。| 
| 27 | --no-displaying-insecure-content | 默认情况下，https 页面允许从 http 链接引用图片/字体/框架。添加这一参数会阻止这些内容。| 
| 28 | --no-first-run | 跳过 Chromium 首次运行检查。|
| 29 | --no-referrers | 不发送 Http-Referer 头。| 
| 30 | --no-sandbox | 彻底停用沙箱。|
| 31 | --no-startup-window | 启动时不建立窗口。|
| 32 | --proxy-pac-url | 使用给定 URL 的 pac 代理脚本。（也可以使用本地文件，如 --proxy-pac-url="file:\\c:\proxy.pac"）| 
| 33 | --proxy-server | 使用给定的代理服务器，这个参数只对 http 和 https 有效。（例如 --proxy-server=127.0.0.1:8087 ）|
| 34 | --show-component-extension-options | 让自带的拓展组件显示在 chrome://settings/extensions 里。（目前有一个 "Bookmark Manager 0.1"）| 
| 35 | --single-process | 以单进程模式运行 Chromium。（启动时浏览器会给出不安全警告）| 
| 36 | --skip-gpu-data-loading | 跳过启动时的 GPU 信息收集、黑名单读取与黑名单自动更新，这样一来，所有的 GPU 功能都可供使用，并且 about:gpu 页面会显示空白。此参数仅供测试使用。|
|37 |--start-maximized | 启动时最大化。| 
| 38 | --touch-optimized-ui | 使用对触屏更友好的用户界面。（目前来看似乎只是把一些字体放大了）| 
| 39 | --user-agent | 使用给定的 User-Agent 字符串。|
| 40 | --user-data-dir | 浏览器存储用户配置文件的目录。|
| 41 | --allow-file-access-from-files | 允许本地`Ajax`请求，也叫`file`协议下的`Ajax`请求 |
| 42 | --enable-file-cookies | 允许本地的`cookies` |


在`chrome`属性设置中，添加启动参数：   
~~--args --disable-web-security  --user-data-dir~~  
`--allow-file-access-from-files`  

> window

设置方法：`chrome`快捷方式–右键`属性`–`快捷方式`–`目标`
```bash
"D:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --allow-file-access-from-files
```

> mac

```bash
//chrome 浏览器
open -a "Google Chrome" 
//safari 浏览器 
open -a '/Applications/Safari.app' --allow-file-access-from-files
```

> linux

```bash
chromium-browser --allow-file-access-from-files  
```