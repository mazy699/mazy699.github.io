---
title: "使用Hugo+Github Pages搭建个人博客"
date: 2021-02-10T23:17:19+08:00
lastmod: 2022-05-12T19:31:49+08:00
draft: false
keywords: ["Hugo","Github","博客"]
description: "使用Hugo+Github Pages搭建个人博客"
tags: ["Hugo","Github","博客"]
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

记录一下在使用Hugo+Github Pages搭建个人博客的过程，以及碰到的问题和解决方法。

<!--more-->

开始准备用Hexo搭建的，但是部署的时候push不到Github，就换Hugo了。

## 准备工作

### 安装Golang

从[Golang官方](https://golang.org/)下载对应系统的版本，安装时默认选择就可以。打开命令行，输入**go version**验证是否安装成功。

### 安装Hugo

到[Hugo releases](https://github.com/gohugoio/hugo/releases)下载对应系统的版本，下载下来是一个安装包，解压后放到一个目录（C盘D盘都可以），将其中的Hugo.exe添加到环境变量path（更加详细参照[Hugo安装](https://www.gohugo.org/doc/overview/installing/)）。打开命令行，输入**hugo version**验证是否安装成功。

### 安装Git

参照[官方安装文档](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)，安装完关联Github还需要设定config，ssh免密码之类的，这部分网上教程比较多，自己搜索一下。

### 注册Github Pages

参照[使用 GitHub Pages](https://docs.github.com/cn/github/working-with-github-pages)，官方的文档有中文（网页右上角有切换语言选项），也介绍的比较详细。

## Hugo使用 

### 创建站点

准备工作完成后，就可以创建博客站点了。选择一个目录，打开命令行切换到选择的目录，执行下面的命令

```shell
$hugo new site Blog
```

新创建的站点的目录结构如下

```
├─archetypes
├─content
├─data
├─layouts
├─resources
├─static
└─themes
```

+ 根目录下 `config.toml` 是博客站点的配置文件
+ `archetypes` 目录下 default.md 是在创建新文章的默认模板
+ `content` 目录存放的是博客的 markdown 源文件
+ `static` 目录可以存放博客中用到的图片
+ `themes` 目录下存放主题

### 创建文章

```shell
$hugo new post/my-first-post.md
```

这条命令会在 `content/post` 下生成新文章 my-first-post.md，随便修改 my-first-post.md 文件。

### 运行Hugo

在站点目录（Blog/）下通过命令行执行下面命令，就可以启动本地服务查看自己的博客。

hugo server 的参数：-D 就可以显示设置 draft 草稿状态的文章

```shell
$hugo server -D
Start building sites …

                   | ZH-CN
-------------------+--------
  Pages            |    23
  Paginator pages  |     0
  Non-page files   |     0
  Static files     |    39
  Processed images |     0
  Aliases          |     7
  Sitemaps         |     1
  Cleaned          |     0

Built in 46 ms
...
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

命令执行出现上面的结果时，就可以通过 http://localhost:1313/ 在浏览器预览自己的博客

### 主题

[hugo themes](https://themes.gohugo.io/) 挑选喜欢的主题，以 [even](https://github.com/olOwOlo/hugo-theme-even) 主题为例，在`themes`目录下通过 `git clone` 下载主题到本地。

```shell
$ git clone https://github.com/olOwOlo/hugo-theme-even themes/even
```

主题使用说明 [wiki](https://github.com/ahonn/hexo-theme-even/wiki)，参照此说明配置完成后，再次预览就可看到主题已经应用成功。

使用过程碰到的问题可以在主题下的 [issues](https://github.com/olOwOlo/hugo-theme-even/issues) 查找是否有相似的问题，大部分问题可能已经closed。

## 部署到GitHub

以上的配置完成后，我们的博客只能通过本地服务查看和管理，当换一台电脑时还需要复制一份，这样并不方便管理。

可以通过部署到GitHub上进行管理，这样可以在网上查看，而且不会丢失文件。

前提：既然要部署到GitHub，那么就需要有一个GitHub账号，并且创建`GitHub Pages`。创建过程参考官方文档[创建 GitHub Pages 站点](https://docs.github.com/cn/github/working-with-github-pages/creating-a-github-pages-site)

命令行执行，执行前将文章的草稿状态从true改为false `draft: false`

```shell
$hugo
Start building sites …

                   | ZH-CN
-------------------+--------
  Pages            |    16
  Paginator pages  |     0
  Non-page files   |     0
  Static files     |    39
  Processed images |     0
  Aliases          |     4
  Sitemaps         |     1
  Cleaned          |     0

Total in 474 ms
```

站点根目录下生成`public`目录，将此目录下文件推送到GitHub Pages仓库的`master`分支。

此外还需要将站点根目录下文件推送到GitHub Pages仓库的`hugo`分支，当然也可以新建仓库存放。

根目录下`themes` 可以通过添加子模块与站点总仓库（hugo分支）关联，例如使用主题hugo-theme-even时

```shell
$git submodule add https://github.com/olOwOlo/hugo-theme-even.git themes/even
```

`public`推送成功后，可以在个人的GitHub Pages页面查看到自己博客，[我的博客](https://mazy699.github.io/)

## 后续

### 图片问题

+ 改为[使用Github+PicGo搭建图床](https://mazy699.github.io/post/%E4%BD%BF%E7%94%A8github+picgo%E6%90%AD%E5%BB%BA%E5%9B%BE%E5%BA%8A/)

~~本地使用**Typora**给博客插入图片时，会有一个路径问题，图片放在 根目录下`static/image`目录下，如果在md文件引用是使用相对路径`../../static/image/github.jpg` ，写博客时可以看到图片，部署之后看不到图片。~~

~~解决方法：**Typora** 设置图片根目录为`..\..\static`，引用时`image/github.jpg`这样就可以编辑时看到图片，部署后也正常显示图片。~~

---
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202205121800203.png)

---

### Git工具

通过 **GIt** 推送博客时，命令行使用不习惯的话，可以使用 [fork](https://git-fork.com/)，很方便好用。

## 参考

1. [Hugo 快速开始指引](https://www.gohugo.org/doc/overview/quickstart/)
2. [Hugo 命令](https://www.gohugo.org/doc/commands/)
3. [Github Docs](https://docs.github.com/cn)

