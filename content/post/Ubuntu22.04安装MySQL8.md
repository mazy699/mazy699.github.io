---
title: "Ubuntu22.04安装MySQL8"
date: 2023-07-13T21:18:14+08:00
lastmod: 2023-07-13T21:18:14+08:00
draft: false
keywords: ["Ubuntu","MySQL"]
description: "Ubuntu22.04安装MySQL8"
tags: ["服务器","技巧","MySQL"]
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
### 第一部分：安装mysql
##### 使用apt安装
```shell
sudo apt update  
sudo apt install -y mysql-server
```
安装完成之后自动结束，不需要输入密码。
##### 更新用户密码
这里默认安装的是mysql8.0版本，因为i没有输入密码；所以无法使用mysql -u root -p进入mysql，需要执行这个命令（一定要加sudo），免密码进入mysql
```shell
sudo mysql -uroot
```
然后使用sql更新用户密码：
```mysql
use mysql  
alter user 'root'@'localhost' identified with mysql_native_password by 'your_new _password';
```
然后就可以使用密码登陆mysql 的root账户了
```shell
mysql -uroot -p
```
### 第二部分：授权远程使用
##### 更新root账号地址
因为之前修改root账号的密码时，地址为localhost，所以这里不能直接授权其他主机访问，需要先把root账号的host修改为可以访问所有主机，再去授权。
```mysql
update user set host='%' where user='root';  
flush privileges;  
grant all on *.* to 'root'@'%';  
flush privileges;
```
记得修改完root账号的host以后要刷新权限，不然无法授权，授权之后也要刷新权限。
##### 修改mysql.conf
```shell
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
并将bind-address参数的值更改为服务器的IP地址或0.0.0.0
```cnf
bind-address = 0.0.0.0
```
##### 重启mysql
```shell
systemctl restart mysql
```
##### 开放防火墙端口
```shell
sudo ufw allow 3306  
sudo ufw reload
```