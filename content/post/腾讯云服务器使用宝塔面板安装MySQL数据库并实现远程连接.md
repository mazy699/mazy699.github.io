---
title: "腾讯云服务器使用宝塔面板安装MySQL数据库并实现远程连接"
date: 2022-06-11T17:49:23+08:00
lastmod: 2022-06-11T17:49:23+08:00
draft: false
keywords: ["服务器","腾讯云服务器","宝塔面板","MySQL"]
description: "腾讯云服务器使用宝塔面板安装MySQL数据库并实现远程连接"
tags: ["技巧","服务器","MySQL"]
categories: ["经验心得"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
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
1. 软件商店下载mysql
2. 安装完成后在数据库页面修改root密码
3. 命令行连接数据库 `mysql -uroot -p`
4. 输入修改后密码，登录mysql
5. 执行以下命令、
	1. MySQL 5 版本 `GRANT ALL ON *.* TO root@'%' IDENTIFIED BY '替换成你的root密码' WITH GRANT OPTION;`
	2. MySQL 8 版本 `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '替换成你的root密码';
6. 允许远程登录 `update user set host = '%' where user = 'root';` 如果报错没有选择database，就 `use mysql` 之后重新执行命令
7. 最后刷新 `FLUSH PRIVILEGES;`
8. 注意：服务器需要开放端口