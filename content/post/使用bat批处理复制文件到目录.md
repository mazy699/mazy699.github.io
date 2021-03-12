---
title: "使用bat批处理复制文件到目录"
date: 2021-03-11T23:09:08+08:00
lastmod: 2021-03-11T23:09:08+08:00
draft: false
keywords: ["bat批处理","技巧"]
description: "使用bat批处理读取txt文件中的文件名list，并将文件复制到指定目录下。"
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

使用bat批处理读取txt文件中的文件名list，并将文件复制到指定目录下。

<!--more-->

## 需求

想要从有多个深层目录下的众多文件中挑选出部分文件，并且保留目录结构，一个一个去找比较麻烦，就写了这个批处理。

## 示例

例子中的注释已经比较详细了，直接看就能明白，使用时注意修改 **txt文件名** 和 **目录路径**。

`test.bat`

```batch
::声明更改代码页为UTF-8
chcp 65001
@echo off
echo ------------------开始---------------------
:: for循环逐行读取test.txt
for /f   %%i in (test.txt)  do (
::设置本地为延迟扩展。其实也就是：延迟变量，
::开始与终止批处理文件中环境改动的本地化操作。
::在执行 Setlocal 之后所做的环境改动只限于批处理文件。
::要还原原先的设置，必须执行 Endlocal。
SetLocal EnableDelayedExpansion
::打印读取到的值到控制台
echo %%i
::设置变量str，并设置为%%i的值
set str=%%i
::替换str中的from为to
Set str=!Str:from=to!
::将替换后的值写到1.txt
echo !str!>>1.txt
::复制%%i 到 str，取消提示“是文件名还是目录名”，默认选择复制文件f，文件夹d，
echo f | xcopy %%i !str! /Y >>log.log
EndLocal
)
echo ------------------结束---------------------
::删除文件
del 1.txt
echo. & pause

```

`test.txt`

```
C:\test\from\1\1.txt
C:\test\from\1\11\11.txt
C:\test\from\1\11\111\111.txt
C:\test\from\2\2.txt
C:\test\from\2\22\22.txt
C:\test\from\2\22\222\222.txt
C:\test\from\3\3.txt
C:\test\from\3\33\33.txt
C:\test\from\3\33\333\333.txt
```

![Image1](/image/使用bat批处理复制文件到目录/Image1.png)

![Image2](/image/使用bat批处理复制文件到目录/Image2.png)