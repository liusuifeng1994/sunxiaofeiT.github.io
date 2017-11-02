---
layout: blog
istop: true
front: true
title: "Git 如何同时向两个仓库push代码"
background-image: "../img/2017-11-02.jpg"
date: 2017-11-02 10:30:00
category: Git
tags:
- Git
- Git命令
- 总结
---

# 同一个项目同时向两个仓库push代码

## 查看当前远端仓库

> git remote -v

可以看到当前的远程仓库，正常情况下有两个，一个是 `fetch`，一个是`push`

## 添加一个远端仓库

这里以 Github 和 Coding.net 为例

> git remote add both git@github.com:username/project.git

终端中是没有任何提示的，但是远端仓库是已经建立好的。

将username替换成自己的账号名字，project改为自己的项目名称

## 为新建的远端仓库添加两个要push的地址

> git remote set-url --add --push git@github.com:username/project/git  
> git remote set-url --add --push git@git.coding.net:username/project.git

注意，这样添加的ssh方式，需要提前配置好 SSH 公钥

## 推送到两个仓库

使用一下命令就可以同时推送到两个仓库了：

> git push both

## 删除新建的库

我们可以使用下列命令来删除新建的库：

> git remote remove remoteName

将remoteName 改为要删除的库名

可以使用：

> git remote -v

来查看当前目录下的所有库名。