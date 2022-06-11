---
title: "SSH远程登录报错"
date: 2022-06-11T17:49:10+08:00
lastmod: 2022-06-11T17:49:10+08:00
draft: false
keywords: ["ssh"]
description: "SSH远程登录出现 WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! 解决办法"
tags: ["技巧","ssh"]
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
# SSH远程登录出现 WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! 解决办法
## 腾讯云重新安装系统后SSH登录报错
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202206071601650.png)
- 远程主机标识已更改

## 解决方法
- 删除报错信息中提到的 ~/.ssh/know_hosts 文件中对应ip地址的公钥信息
- 注意：服务器需要开放ssh端口