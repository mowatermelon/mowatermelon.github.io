---
title: 框架学习之docker拉取centos镜像
category: 框架学习
tags:
  - centos
  - docker
  - 框架学习
date: 2017-11-08 00:00:00
---
# 1 安装与配置 Docker

## 1.1 安装 Docker

> Docker 软件包已经包括在默认的 CentOS-Extras 软件源里。因此想要安装 docker，只需要运行下面的 yum 命令：

```bash
yum install docker-io -y
```

<!--more-->

> 直接yum安装，安装成功后查看版本

```bash
docker -v
```

> 启动docker

```bash
service docker start
```

> 设置开机启动

```bash
chkconfig docker on
```

---

## 1.2 配置 Docker

> 更换腾讯云镜像源

```bash
echo "OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'" >> /etc/sysconfig/docker
```

> 镜像源挂载

```bash
systemctl daemon-reload
```

> 重启docker镜像

```bash
service docker restart
```

---

# 2 Docker 的简单操作

## 2.1 下载镜像

> 运行容器

这时我们可以在刚才下载的 CentOS 镜像生成的容器内操作了。
生成一个 centos 镜像为模板的容器并使用 bash shell

```bash
docker run -it centos /bin/bash
```

> 这个时候可以看到命令行的前端已经变成了 [root@(一串 hash Id)] 的形式, 这说明我们已经成功进入了 CentOS 容器。

在容器内执行任意命令, 不会影响到宿主机, 如下

```bash
mkdir -p /data/simple_docker
```

> 可以看到 /data 目录下已经创建成功了 simple_docker 文件夹

```bash
ls /data
```

> 退出容器

```bash
exit
```

> 查看宿主机的 /data 目录, 并没有 simple_docker 文件夹, 说明容器内的操作不会影响到宿主机

```bash
ls /data
```

## 2.2 保存容器

> 查看所有的容器信息， 能获取容器的id

```bash
docker ps -a
```

> 请自行将 -m 后面的信息改成自己的容器的信息，保存镜像：

```bash
docker commit -m="备注" 你的CONTAINER_ID 你的IMAGE
```
