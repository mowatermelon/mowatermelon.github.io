---
title: 框架学习之docker基础学习
category: 框架学习
tags:
  - base
  - docker
  - 框架学习
date: 2017-11-07 00:00:00
---

> 第一步  安装docker

```bash
sudo yum -y docker
```

<!--more-->

> 第二步 启动服务

```bash
service docker start
```

> 第三步 拉取镜像，或者直接启动镜像

```bash
docker pull training/webapp  # 载入镜像
docker run -d -p 5000:5000 training/webapp python app.py
#  -d:让容器在后台运行。
# -P:将容器内部使用的网络端口映射到我们使用的主机上。
```

> 第四步 查看当前启动的容器

```bash
docker ps
```

> 第五步 重启当前容器

正在运行的容器，我们可以使用命令来重启

```bash
docker restart
```

> 第六步 停止对应容器服务

```bash
docker stop <dockerName>
# 举个栗子 在上一步中查看的容器名称是melon

docker stop melon
```

> 第七步 移除WEB应用容器

我们可以使用命令来删除不需要的容器

```bash
docker rm <dockerName>
# 举个栗子 在上一步中查看的容器名称是melon

docker rm melon
```

> 过程截图

![image](https://user-images.githubusercontent.com/18508817/37816431-057eb69a-2eae-11e8-91b7-5f34b5ee9c23.png)
