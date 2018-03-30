---
title: .NET学习之C#实现调用Java类中方法
category: NET
tags:
  - .NET
  - java
  - jar
  - IKVM
date: 2017-11-09 00:00:00
---

> 基本思路

用`C#`实现调用`Java`编写的类中的方法；重点是将`Java`编写的程序打包成`Jar`，然后使用开源工具`IKVM`将其转化成`DLL`控件，在`.NET`环境下调用。

<!--more-->

分为以下步骤：

- 下载`JDK6`（注:`JDK7`下可能不支持，建议使用`JDK6`和`Eclipse`），进行安装，然后配置环境变量Path，将JDK安装的路径(例如：`D:\Program Files\Java\jdk1.6.0_10\bin`)添加到`Path`变量后面。

   用`cmd`打开`DOS`框，输入`javac`就可以查看是否配置成功，配置成功会有较详细的信息展示。

- 到`IKVM`官方网站下载IKVM需要的组件 `http://www.ikvm.net/`,或者`https://sourceforge.net/projects/ikvm/files/ikvm/0.42.0.3`

    `ikvm-0.42.0.3.zip`，`ikvmbin-0.42.0.3.zip`，`openjdk6-b16-stripped.zip`分别下载三个压缩文件，然后将`ikvm-0.42.0.3.zip`进行解压，将其解压的文件的路径添加到用户和系统环境变量`Path`后面，类似于配置JDK时的做法。

![image](https://user-images.githubusercontent.com/18508817/37642373-d85c24fc-2c57-11e8-8e3d-ac6327f46af4.png)

- 将转化的JAR包通过IKVM工具转化为`DLL`控件。举例jar文件名是`com.Hello.jar`，你想转化之后的文件名是`Hello.dll`

```cmd
ikvmc -out:Hello.dll com.Hello.jar
```

- 新建`C#`项目，将`ikvm-0.42.0.3.zip`解压出来的文件路径的`bin`目录下找到以下3个DLL控件`IKVM.OpenJDK.Core.dll` ，`IKVM.Runtime.dll` ，`IKVM.Runtime.JNI.dll` 将它们添加引用添加到`C#`项目中。然后添加自己生成的`Hello.dll`控件。