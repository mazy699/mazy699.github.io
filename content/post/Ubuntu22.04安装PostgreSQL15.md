---
title: "Ubuntu22.04安装PostgreSQL15"
date: 2023-07-13T21:18:28+08:00
lastmod: 2023-07-13T21:18:28+08:00
draft: false
keywords: ["Ubuntu","PostgreSQL"]
description: "Ubuntu22.04安装PostgreSQL15"
tags: ["服务器","技巧","PostgreSQL"]
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
#typora-root-url: ..\..\static
---

<!--more-->
### 启用 PostgreSQL 包存储库
```shell
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'  
wget -qO- https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo tee /etc/apt/trusted.gpg.d/pgdg.asc &>/dev/null
```
使用 apt update 命令获取包的最新版本
```shell
sudo apt update
```
### 安装数据库服务端和客户端
使用下面的 apt 命令安装 PostgreSQL 客户端和服务器
```shell
sudo apt install postgresql postgresql-client -y
```
验证 PostgreSQL 服务是否启动并运行
```shell
sudo systemctl status postgresql
```
使用 psql 命令行实用程序检查 PostgreSQL 版本
```shell
psql --version
```
### 更新管理员用户密码
连接到 PostgreSQL 服务器
```shell
sudo -u postgres psql
```
为 postgres 用户设置密码
```postgresql
ALTER USER postgres PASSWORD 'demoPassword';
```
上面的 SQL 查询将用户密码设置为 **`demoPassword`**。
使用 **`q`** 命令终止与服务器的当前会话
我们再次连接数据库服务器
```shell
psql -h localhost -U postgres
```
输入 **`demoPassword`** 字符串作为密码，我们可以成功连接到数据库。
### 配置 PostgreSQL 允许远程连接
默认情况下，PostgreSQL 只接受来自本地主机的连接。我们可以修改配置，允许远程客户机的连接。  
使用编辑器打开 /etc/postgresql/15/main/postgresql.conf 配置文件
```shell
sudo vim /etc/postgresql/15/main/postgresql.conf
```
取消 listen_addresses 开头的行注释，用 * 替换 localhost
```conf
listen_addresses = '*'
```
接下来，编辑 pg hba.conf 文件的 IPv4 本地连接部分，以允许来自所有客户端的 IPv4 连接。
```shell
sudo vim /etc/postgresql/15/main/pg_hba.conf
```
修改IPv4 local connections
```conf
# IPv4 local connections:  
host    all             all             127.0.0.1/32            scram-sha-256  
host    all             all             0.0.0.0/0            scram-sha-256
```
如果开启了防火墙，那么使用下面的命令允许 PostgreSQL 5432 端口
```shell
sudo ufw allow 5432
```
### 验证远程连接
重新启动服务并检查它是否正常运行
```shell
sudo systemctl restart postgresql  
sudo systemctl status postgresql
```