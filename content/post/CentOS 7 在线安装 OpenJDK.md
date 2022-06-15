---
title: "CentOS 7 在线安装 OpenJDK"
date: 2022-06-15T22:59:37+08:00
lastmod: 2022-06-15T22:59:37+08:00
draft: false
keywords: ["CentOS","OpenJDK"]
description: "CentOS 7 在线安装 OpenJDK"
tags: ["技巧","服务器"]
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
# yum 安装
```zsh
yum search java|grep openjdk     # 查找安装包
```
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202206152224562.png)

- 执行命令后，会有各种版本，选择想要安装的版本执行安装命令，例如安装 openjdk 11
```zsh
yum install java-11-openjdk
```
- 安装过程会有询问是否下载，输入 y 回车，之后等待安装完成即可。

# 查找 Java 的安装路径
```zsh
# 依此执行以下命令
which java
ls -lr /usr/bin/java
ls -lr /etc/alternatives/java
```
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202206152237274.png)

# 配置环境变量
```zsh
# 编辑 /etc/profile，
vi /etc/profile
```

- 将下面内容加在配置文件最后，注意 JAVA_HOME 修改为上面查到的 Java 安装路径。
```
# Java Environment
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.15.0.9-2.el7_9.x86_64/bin/java
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/jre/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$PATH
```

```zsh
# 使环境变量生效
source /etc/profile

# 确认 java 安装是否成功
java -version
```
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202206152248571.png)