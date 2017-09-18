---
title: 软件折腾之为右键添加Gitbash
category: 软件折腾
tags:
  - gitbash
  - GitHub
  - cmd
  - 软件折腾
date: 2017-09-04 00:00:00
---

> 之前主要使用GitHub客户端，这边项目中需要用到gitbash才发现这个软件不能直接在右键显示，搜索相关博客都是只有文字没有图片，避免以后还要用，写篇日志整理一下

# 1 了解注册表知识

注册表（`Registry`，繁体中文版`Windows`操作系统称之为登录档）是`Microsoft Windows`中的一个重要的数据库，用于存储系统和应用程序的`设置信息`。早在`Windows 3.0`推出`OLE`技术的时候，注册表就已经出现。随后推出的`Windows NT`是第一个从系统级别广泛使用注册表的操作系统。但是，从`Microsoft Windows 95`操作系统开始，注册表才真正成为Windows用户经常接触的内容，并在其后的操作系统中继续沿用至今。

<!-- more -->

# 2 实际操作

## 2.1 打开注册表

![利用cmd打开注册表](../../../../img/利用cmd打开注册表.png)
使用`win+r`快捷键，输入指令`regedit`，打开运行器

## 2.2 选择对应注册表

![打开注册表](../../../../img/打开注册表shell.png)
选择`HKEY_CLASSES_ROOT\Directory\Background`，在下面新建项`Git`，当然这个名字你可以随便起，但是为了语义化，建议取与`Git`有关的名字

## 2.3 在Git项下配置相关参数

![在Git项下配置相关参数](../../../../img/在Git项下配置相关参数.png)
首先配置`Git`项的默认参数，数据值是显示在右键选项上的`text`内容，为了语义化更清楚，我这边直接配置的`git bash here`。
其次配置数据值是显示在右键选项上的`icon`内容,这里需要配置本机`GitBash icon`的地址，我本机的地址是`D:\Program Files\Git\mingw64\share\git\git-for-windows.ico`。

## 2.4 配置Git项下command项

![配置Git项下command项](../../../../img/配置Git项下command项.png)
在`Git`项下新建`command`，配置`command`默认参数,这里也是配置本机`GitBash`的安装地址，我本机的安装地址是`D:\Program Files\Git\git-bash.exe`。

# 3 测试是否安装成功

![GitBash显示在右键功能栏](../../../../img/GitBash显示在右键功能栏.png)