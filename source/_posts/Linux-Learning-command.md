---
title: Linux学习之基础指令学习
category: Linux
tags:
  - Linux
  - command
date: 2017-10-13 00:00:00
---
> 我之前都没有怎么使用过linux系统，最近刚刚装了deepin，感觉对着终端，无从下手，所以查了相关指令，进行学习。

# 1 deepin简介

`Deepin` 原名`Linux Deepin`，在2014年4月改名`Deepin`。`Deepin`团队基于`Qt/C++`（用于前端）和`Go`（用于后端）开发了的全新深度桌面环境（`DDE`），以及`音乐播放器`，`视频播放器`，`软件中心`等一系列特色软件。

<!--more-->

`Deepin`是由武汉深之度科技有限公司开发的`Linux发行版`。`Deepin` 是一个基于 `Linux` 的操作系统，专注于使用者对`日常办公`、`学习`、`生活`和`娱乐`的操作体验的极致，适合`笔记本`、`桌面计算机`和`一体机`。它包含了所有你需要的应用程序，`网页浏览器`、`幻灯片演示`、`文档编辑`、`电子表格`、`娱乐`、`声音`和`图片处理软件`，`即时通讯软件`等等。

`Deepin` 的历史可以追溯到 `2004年`，其前身 `Hiweed Linux` 是`中国第一个`基于 Debian的`本地化衍生版`，并提供轻量级的`可用LiveCD`，旨在创造一个全新的简单、易用、美观的 `Linux 操作系统`。

`Deepin`拥有自主设计的特色软件：`深度软件中心`、`深度截图`、`深度音乐播放器`和`深度影音`，全部使用自主的`DeepinUI`，其中有`深度桌面环境`，`DeepinTalk（深谈）`等。

`Deepin`是中国`最活跃`的 `Linux 发行版`，`Deepin` 为所有人提供`稳定`、`高效`的`操作系统`，强调`安全`、`易用`、`美观`。其口号为“免除新手痛苦，节约老手时间”。在社区的参与下，“让 Linux 更易用”也不断变成可以触摸的现实。

# 2 常用指令

| 指令名称  | 指令含义 |
|:----------|:----------|
| ls　　     |    显示文件或目录
|  ls    -l   |         列出文件详细信息l(list)
|   ls   -a    |       列出当前目录下所有文件及目录，包括隐藏的a(all)
| mkdir      |    创建目录
|   mkdir   -p    |        创建目录，若无父目录，则创建p(parent)
| cd         |       切换目录
| man command |  查看某个指令的帮助文档
| touch      |     创建空文件
| echo       |      创建带有内容的文件。
| cat        |      查看文件内容
| cp         |        拷贝
| mv         |       移动或重命
| rm         |       删除文件
|  rm     -r     |        递归删除，可删除子目录及文件
|  rm     -f    |        强制删除
| find        |       在文件系统中搜索某文件
| wc           |      统计文本中行数、字数、字符数
| grep        |      在文本文件中查找某个字符串
| rmdir       |     删除空目录
| tree       |       树形结构显示目录，需要安装tree包
| pwd         |      显示当前目录
| ln         |          创建链接文件
| more、less |  分页显示文本文件内容
| head、tail  |   显示文件头、尾内容
| ctrl+alt+F1 |  命令行全屏模式s

# 3 系统管理命令

| 指令名称  | 指令含义 |
|:----------|:----------|
| stat         |      显示指定文件的详细信息，比ls更详细
| who          |      显示在线登陆用户
| whoami       |    显示当前操作用户
| hostname     |  显示主机名
| uname         |   显示系统信息
| top          |       动态显示当前耗费资源最多进程信息
| ps           |        显示瞬间进程状态 ps -aux
| du           |        查看目录大小 du -h /home带有单位显示目录信息
| df           |       查看磁盘大小 df -h 带有单位显示磁盘信息
| ifconfig      |     查看网络情况
| ping         |        测试网络连通
| netstat       |    显示网络状态信息
| man           |      命令不会用了，找男人  如：man ls
| clear          |     清屏
| alias          |      对命令重命名 如：alias showmeit="ps -aux" ，另外解除使用unaliax showmeit
| kill            |      杀死进程，可以先用ps 或 top命令查看进程的id，然后再用kill命令杀死进程。

# 4 打包压缩相关命令

| 指令名称  | 指令含义 |
|:----------|:----------|
| gzip&bzip2&tar:    |    打包压缩
|      -c          |       归档文件
|      -x         |        压缩文件
|      -z         |        gzip压缩文件
|      -j         |        bzip2压缩文件
|      -v           |      显示压缩或解压缩过程 v(view)
|      -f          |       使用档名

举个栗子

```bash
tar -cvf /home/abc.tar /home/abc              #只打包，不压缩

tar -zcvf /home/abc.tar.gz /home/abc        #打包，并用gzip压缩

tar -jcvf /home/abc.tar.bz2 /home/abc      #打包，并用bzip2压缩
```

当然，如果想解压缩，就直接替换上面的命令  `tar -cvf  / tar -zcvf  / tar -jcvf` 中的`c` 换成`x` 就可以了。

# 5 关机/重启机器

| 指令名称  | 指令含义 |
|:----------|:----------|
| shutdown -r    |        关机重启
| shutdown -h    |         关机不重启
|  shutdown now  |      立刻关机
| halt           |       关机
| reboot        |     重启

# 6 Linux管道

将一个命令的标准输出作为另一个命令的标准输入。也就是把几个命令组合起来使用，后一个命令除以前一个命令的结果。

```bash
#在home目录下所有文件中查找，包括close的文件，并分页输出。
grep -r "close" /home/* | more
```

# 7 Linux软件包管理

## 7.1 dpkg

Debian Package管理工具，软件包名以`.deb`后缀。这种方法适合系统不能联网的情况下。

比如安装`tree`命令的安装包，先将`tree.deb`传到`Linux`系统中。再使用如下命令安装。

```bash
sudo dpkg -i tree_1.5.3-1_i386.deb        # 安装软件
sudo dpkg -r tree                       #卸载软件
```

注：将`tree.deb`传到`Linux`系统中，有多种方式。`VMwareTool`使用挂载方式；或者使用`winSCP`工具等；

## 7.2 APT

Advanced Packaging Tool高级软件工具，这种方法适合系统能够连接互联网的情况。

依然以`tree`为例

```bash
sudo apt-get install tree                         #安装tree
sudo apt-get remove tree                       #卸载tree
sudo apt-get update                                 #更新软件
sudo apt-get upgrade
```

# 8 vim使用

vim三种模式：`命令模式`、`插入模式`、`编辑模式`。使用`ESC`或`i`来切换模式。

命令模式下：

| 字符内容  | 字符含义 |
|:----------|:----------|
|:q      |          退出
|:q!      |            强制退出
|:wq       |          保存并退出
|:set number   |  显示行号
|:set nonumber   |  隐藏行号
|/apache         |      在文档中查找apache 按n跳到下一个，shift+n上一个
|yyp            |          复制光标所在行，并粘贴
|h    |     左移一个字符←
|j    |     下一行↓
|k    |     上一行↑
|l    |     右移一个字符→

# 8 用户及用户组管理

| 账号地址  | 地址含义 |
|:----------|:----------|
| /etc/passwd  |  存储用户账号
| /etc/group    |    存储组账号
| /etc/shadow   |   存储用户账号的密码
| /etc/gshadow   |  存储用户组账号的密码
| useradd 用户名  |  添加用户
| userdel 用户名  |  删除用户
| adduser 用户名  |  未知
| groupadd 组名  |  添加用户组
| groupdel 组名  |  删除用户组
| passwd root     |    给root设置密码
| su root  |  进入管理员帐号，这个时候会提示需要输入密码
| su - root   |  以管理员身份做些事情
| /etc/profile   |   系统环境变量
| bash_profile   |  用户环境变量
| .bashrc      |     用户环境变量
| su user        |     切换用户，加载配置文件.bashrc
| su - user     |    切换用户，加载配置文件/etc/profile ，加载bash_profile

更改文件的用户及用户组

```bash
sudo chown [-R] owner[:group] {File|Directory}
```

例如：还以`jdk-7u21-linux-i586.tar.gz`为例。属于`用户hadoop`，`组hadoop`

要想切换此文件所属的用户及组，可以使用命令。

```bash
sudo chown root:root jdk-7u21-linux-i586.tar.gz
```

# 9 文件权限管理

> 三种基本权限

| 字符内容  | 字符含义 |
|:----------|:----------|
| R           | 读        |  数值表示为4|
| W          | 写         | 数值表示为2|
| X           | 可执行  | 数值表示为1|

如图所示，`jdk-7u21-linux-i586.tar.gz`文件的权限为`-rw-rw-r--`

`-rw-rw-r--`一共十个字符，分成四段。

- 第一个字符“-”表示普通文件；这个位置还可能会出现“l”链接；“d”表示目录

- 第二三四个字符“rw-”表示当前所属用户的权限。   所以用数值表示为4+2=6

- 第五六七个字符“rw-”表示当前所属组的权限。      所以用数值表示为4+2=6

- 第八九十个字符“r--”表示其他用户权限。              所以用数值表示为2

所以操作此文件的权限用数值表示为`662`

> 更改权限

```bash
sudo chmod [u所属用户  g所属组  o其他用户  a所有用户]  [+增加权限  -减少权限]  [r  w  x]   目录名
```

例如：有一个文件`filename`，权限为`-rw-r----x` ,将权限值改为`-rwxrw-r-x`，用数值表示为`765`

```bash
sudo chmod u+x g+w o+r  filename

# 上面的例子可以用数值表示

sudo chmod 765 filename
```