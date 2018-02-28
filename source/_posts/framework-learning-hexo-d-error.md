---
title: 框架学习之hexo_deploy失败 
category: 框架学习
tags:
  - node
  - hexo
  - vscode
  - hexo d
  - 框架学习
date: 2017-11-04 14:29:17
---

> 最近公司网络比较艰苦，那天写了一个文章，执行hexo g -d，正常生成了public文件，但是一直发布不成功，记录一下我解决的过程

<!--more-->

# 1. 问题产生操作步骤

- 文章写完

- 执行`hexo s --watch`

- 预览页面效果，修改部分细节

- 执行`hexo g -d`

- 出现错误提示，提示

```bash
delete mode 100644 placeholder
warning: LF will be replaced by CRLF in js/script.js.
The file will have its original line endings in your working directory.
bash: /xxx/xxx: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': Invalid argument
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/do                                                        cs/troubleshooting.html
Error: bash: /xxx/xxx: No such device or address
error: failed to execute prompt script (exit code 1)
fatal: could not read Username for 'https://github.com': Invalid argument
```

# 2. 尝试解决过程

## 2.1 尝试一

- 执行`hexo g`,`public`文件夹生成成功

- 执行`hexo d`，控制台出现错误提示和上文一样

- 卒

## 2.2 尝试二

- 修改项目根文件夹下的`_config.yml`文件，修改请求地址属性名，将`repository`修改为`repo`。

> 修改前

```yml

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/{{注册呢称}}/{{注册呢称}}.github.io.git
  branch: master

```

> 修改后

```yml

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/{{注册呢称}}/{{注册呢称}}.github.io.git
  branch: master

```

- 执行`hexo g -d`，控制台出现错误提示和上文一样

- 卒

## 2.3 尝试三

- 修改项目根文件夹下的`_config.yml`文件，请求仓库链接方式，将原有的`http`请求链接修改为`SSH`请求模式。

> 修改前

```yml

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/{{注册呢称}}/{{注册呢称}}.github.io.git
  branch: master

```

> 修改后

```yml

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: git@github.com:{{注册呢称}}/{{注册呢称}}.github.io.git
  branch: master

```

- 执行`hexo g -d`，出现错误提示。

```bash
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

FATA Something's wrong.Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html

Error: Warning; Permanently added the RSA host key for IP address'52.74.223.119' to the list of known hosts.

Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

  at ChildProcess.<anonymous> (x:\xx\xxxx\{{注册呢称}}.github.io\node_modules\hexo-util\lib\spawn.js:37:17)
  at emitTwo (events.js:126:13)
  st ChildProcess.emit (events.js:214:7)
  at ChildProcess.cp.emit (x:\xx\xxxx\{{注册呢称}}.github.io\node_modules\cross-spawn\1ib\enoent.js:40:29)
  at maybeclose (internal/child_process.js :925 :16)
  at Process.ChildProcess._handle.onexit (internal/child_process.js:209:5)
```

- 卒

## 2.4 尝试四

- 保存上文修改修改项目根文件夹下的`_config.yml`文件中`Deployment`请求为`SSH`请求模式

- 重新生成`SSH`

- 在控制台执行`ssh-keygen-t rsa -C {你的邮箱地址}`

- 会出现三次询问过程，一般就直接默认了

- 生成成功

```bash
$ ssh-keygen-t rsa -C XXXX@XXXX.com

Generating public/private rsa key pair
Enter file in which to save the key (/C/Users/Administrator/.ssh/id_rsa) :
created directory'/C/Users/Administrator/ ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /C/Users/Administrator/.ssh/id_rsa.
Your public key has
been saved in /C/Users/Administrator/ssh/id_rsa.pub.
The key fingerprint is:
SHA256:NF10yf+QE7HGu6S+j2Vz9PpN8dJ+uS/FVJ5qo XXXX@XXXX.com

The key's randomart image is:
+-----[RSA 2048]----+
|             .o... |
|          .  +o... |
|         o .  .o++ |
|        . .   .o.. |
|         s    .oBo |
|             o+o+* |
|            ..o@+* |
|            .oBoB= |
|             EBO+. |
+-----[SHA25 6]-----+
```

- 访问上文的公钥地址`c/Users/Administrator/.ssh/id_rsa`

- 复制`id_rsa.pub`文件中内容。

- 访问`https://github.com/settings/keys`，选择`New SSH Key`按钮

- 在`SSH keys / Add new`中，主要需要填写两个内容，一个是将要新建的`SSH`的`title`，相当于这个`SSH`的`alias`，用于区分不同`SSH`；一个是需要填写的`SSH Key`内容。

- `SSH Key`输入框中会有默认提示，`Begins with 'ssh-rsa', 'ssh-dss', 'ssh-ed25519', 'ecdsa-sha2-nistp256', 'ecdsa-sha2-nistp384', or 'ecdsa-sha2-nistp521'`，即这个`SSH Key`必须要以`ssh-rsa`, `ssh-dss`, `ssh-ed25519`, `ecdsa-sha2-nistp256`, `ecdsa-sha2-nistp384`, 或者 `ecdsa-sha2-nistp521`。

- 将从`id_rsa.pub`文件中复制的内容，粘贴到`SSH Key`输入框。

- 选择`Add SSH key`按钮

- `github`新建`SSH key`完成

- 在本地编辑器中添加全局用户设置

```bash
$ git config --global user.name {你的全局呢称}
$ git config --global user.email {你的全局邮箱地址}

# 举个栗子

$ git config --global user.name "mowatermelon"
$ git config --global user.email "neefoxmo@gmail.com"

```

- 在本地编辑器控制台中进行验证`SSH`是否添加成功

```bash
$ ssh -T git@github.com
Hi xxxx! You've successfully authenticated, but GitHub does not provide shell access.

# xxxx应该与你在上一步设置的`user.name`一致
```

- 在`blog`所在项目根文件夹，执行`hexo g -d`，执行一切顺利。

```bash
INFO Deploy done:git
```

# 3 总结

- 感觉在远程仓库这块，网络是个很大因素，决定你是否能够成功访问，和成功发布。
- 之前用http请求没感觉，现在网络不太好，就很明显了。
- http记得是基于TCP面向连接的，要求服务器可以保持持续连接状态
- 面向连接的请求，保证了数据的安全性，但是对于网络条件要求更高
- 但是这边SSH链接请求，似乎对网络条件要求低一些。
