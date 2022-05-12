---
title: "使用Github+PicGo搭建图床"
date: 2022-05-12T19:17:53+08:00
lastmod: 2022-05-12T19:17:53+08:00
draft: false
keywords: ["Github","图床","PicGo"]
description: ""
tags: ["Github","图床","PicGo"]
categories: ["经验心得"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""
typora-root-url: ..\..\static
---

<!--more-->
# Github创建配置
## 创建新仓库
+ 需要创建`public`的仓库
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121826040.png)
## 仓库创建完成后，配置 token 
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121829720.png)
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121832319.png)
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121837523.png)
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121841059.png)
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121844983.png)
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121846101.png)
# PicGo下载配置
## 下载
在[PicGo](https://github.com/Molunerfinn/PicGo/releases)选择对应自己系统的版本下载安装，最好选择最新的正式版。
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121852697.png)
## 配置
+ 安装完成后，打开PicGo进行配置
	+ 仓库名：user/仓库名，例如：zhangsan/PicGoImage
	+ 分支：main
	+ token：Github配置的token
	+ 存储路径：自定义
	+ 自定义域名：使用[jsdelivr](https://www.jsdelivr.com/?docs=gh)进行cdn加速后的域名，https://cdn.jsdelivr.net/gh/user/仓库名@分支，例如https://cdn.jsdelivr.net/gh/zhangsan/PicGoImage@main
+ ![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121912175.png)

