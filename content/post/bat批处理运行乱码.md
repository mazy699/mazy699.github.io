---
title: "bat批处理运行乱码"
date: 2021-03-12T20:46:50+08:00
lastmod: 2021-03-12T20:46:50+08:00
draft: false
keywords: ["bat批处理","技巧"]
description: "bat批处理运行时乱码的解决方法"
tags: ["bat批处理","技巧"]
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

bat批处理运行时乱码的解决方法

<!--more-->

## 问题现象

bat文件中包含中文，保存的编码格式UTF-8，此时运行该bat文件会出现乱码

```batch
@echo off
echo ------------------开始---------------------
for /f   %%i in (test.txt)  do (
SetLocal EnableDelayedExpansion
echo %%i
set str=%%i
Set str=!Str:Helloo=hello!
　　echo !str!>>1.txt
　　EndLocal
)
echo ------------------结束---------------------
echo. & pause
```

![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121801443.png)

## 解决方法

1. 改变编码格式为ANSI
2. 在原先 bat 脚本文件中声明更改代码页 `chcp 65001`

```batch
chcp 65001
@echo off
echo ------------------开始---------------------
for /f   %%i in (test.txt)  do (
SetLocal EnableDelayedExpansion
echo %%i
set str=%%i
Set str=!Str:Helloo=hello!
　　echo !str!>>1.txt
　　EndLocal
)
echo ------------------结束---------------------
echo. & pause
```

![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121802355.png)

## 拓展

| 代码页 | 映射的字符集 |
| ------ | ------------ |
| 936    | GB2312       |
| 20127  | US-ASCII     |
| 65001  | UTF-8        |

