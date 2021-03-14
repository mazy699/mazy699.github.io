---
title: "同时使用Github和Gitee搭建个人博客"
date: 2021-03-14T16:21:57+08:00
lastmod: 2021-03-14T16:21:57+08:00
draft: false
keywords: ["Hugo","Github","Gitee","博客"]
description: "同时使用Github和Gitee搭建个人博客"
tags: ["Hugo","Github","Gitee","博客"]
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

## 原因

最近因为 Github 偶尔抽风打不开，就想着把博客备份到 Gitee，研究了一下，发现有个功能可以同步 Github，这样的话同时维护两个也没有更麻烦。

## 同步操作

1. 复制 Github Pages 已经搭建完成的博客的仓库地址，[博客搭建看这里](https://mazy699.github.io/post/%E4%BD%BF%E7%94%A8hugo+github-page%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)

![Image1](/image/同时使用Github和Gitee搭建个人博客/Image1.png)

2. 注册 Gitee 账号，新建一个仓库，点击最下方的**导入已有仓库**，并将 Github 仓库链接粘贴，创建仓库。

![Image2](/image/同时使用Github和Gitee搭建个人博客/Image2.png)

3. 导入完成后，在仓库界面选择 `服务--->Gitee Pages`

![Image3](/image/同时使用Github和Gitee搭建个人博客/Image3.png)

4. 选择**启动**，可以勾选上强制使用HTTPS，部署成功后会显示 Gitee Pages 网址。

![Image4](/image/同时使用Github和Gitee搭建个人博客/Image4.png)

![Image5](/image/同时使用Github和Gitee搭建个人博客/Image5.png)

5. 打开网址后可能会发现显示不正常，如下图，原因是因为现在路径不对，解决方法就是在管理界面修改仓库路径为用户名，保存之后在 Gitee Pages 更新部署。

![Image6](/image/同时使用Github和Gitee搭建个人博客/Image6.png)

![Image7](/image/同时使用Github和Gitee搭建个人博客/Image7.png)

6. 到这已经完成了 Github--->Gitee 的导入，之后新添加的博客通过同步按钮就可以很方便同步到 Gitee 了。

![Image8](/image/同时使用Github和Gitee搭建个人博客/Image8.png)