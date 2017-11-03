---
layout: blog
istop: true
lasted: true
code: true
title: "ubuntu/deepin 安装jekyll环境"
background-image: "../img/2017-11-03/0.jpg"
date: 2017-11-03 19:33:00
category: Ruby
tags: 
- Ruby
- 安装软件
- jekyll
- jekyll环境
---

# 在Ubuntu/deepin上安装Ruby

## 安装 Rudy

输入以下命令：

> sudo apt-get install Ruby-full 

这里选择安装 Ruby-feed 是因为在Ubuntu的包里Ruby被分成了许多小包，我们要安装 Ruby-feed 才能安装所有的包。  

安装Ruby之后，我们可以使用：

> ruby -v

和

> gem -v  

来检查是否正确安装，当出现了版本号时，说明安装正确

## 安装 jekyll

在安装好了 RUby 之后，我们使用它自带的包管理器gem 来安装 jekyll

> gem install jekyll  

如果出现没有权限的情况，则使用管理员权限，即：

> sudo gem install jekyll

## 使用 jekyll 生成第一个博客

使用以下命令：

> jekyll new myblog 

这条命令会新建一个名字为 myblog 的文件夹，这个文件就是存放博客源文件的目录。

如果出现：
![img](/img/2017-11-03/bundler.png)

则说明缺少bundler这个包，使用以下命令安装：

> gem install bundler  

同样的，如果提示没有权限，则使用 sudo 执行

## 运行博客项目

使用 cd 命令进入到博客目录中去，比如我前面新建的博客项目是 myblog ：

> cd myblog  

使用以下命令运行项目：  

> jekyll serve  

如果出现：

![img](/img/2017-11-03/minima.png)  
和
![img](/img/2017-11-03/jekyll-feed.png)

都是缺少相应的包的原因，分别 使用以下命令安装：

> gem install minima  
和  
> gem install jekyll-feed

同样，提示权限不够的话，使用sudo权限执行。