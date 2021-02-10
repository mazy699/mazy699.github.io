---
title: "使用Hugo+Github Page搭建个人博客"
date: 2021-02-10T23:17:19+08:00
lastmod: 2021-02-10T23:17:19+08:00
draft: true
keywords: ["Hugo","Github Page","博客"]
description: "使用Hugo+Github Page搭建个人博客"
tags: ["Hugo","Github"]
categories: ["经验心得"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: true
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
---

> 记录一下在使用Hugo+Github Page搭建个人博客的过程，以及碰到的问题和解决方法。

<!--more-->

git 添加主题子模块，例如使用主题hugo-theme-even时

```
git submodule add https://github.com/olOwOlo/hugo-theme-even.git themes/even
```

