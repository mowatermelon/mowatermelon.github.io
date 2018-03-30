---
title: 框架学习之node版本升级重装cnpm
category: 框架学习
tags:
  - cnpm
  - node
  - 框架学习
date: 2017-11-11 00:00:00
---

> 今天看了一下，node现在最新稳定版本是8.10.0，最新版本是9.9.0，我本地还是8.9.3，感觉版本有点老，想着本地反正也是用的nvm可以随意升级，就`nvm install v8.10.0`，然后`nvm use v8.10.0`,执行完成之后，我发现我之前装的`cnpm`和`vue`不管用了。

<!--more-->

# 升级之后的版本效果图

![image](https://user-images.githubusercontent.com/18508817/38133667-b4f24834-33ff-11e8-810d-a5b40f831c8b.png)

---

# 安装cnpm出错

我就重新全局安装`cnpm`指令，但是这边一直报错

```bash
D:\Users\Administrator>npm install -g cnpm --registry=https://registry.npm.taoba
o.org
npm ERR! Unexpected end of JSON input while parsing near '...p-equal":"~1.0.1","
ma'

npm ERR! A complete log of this run can be found in:
npm ERR!     D:\Users\Administrator\AppData\Roaming\npm-cache\_logs\2018-03-26T0
6_04_13_634Z-debug.log
```

我以为我镜像指向的路径有问题，重新试了好几遍，结果发现就是不行

> 在网上搜到可以通过强制清理npm cache 来解决，主要是因为之前本地安装cnpm，所以需要清理一下缓存

```bash
npm cache clean --force
```

然后我执行安装操作，安装成功了，不知道对后续有没有其他影响

> 过程截图

![image](https://user-images.githubusercontent.com/18508817/37889629-f207083e-30ff-11e8-88ed-0f1ffcbcb318.png)
