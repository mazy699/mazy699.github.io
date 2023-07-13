---
title: "Ubuntu虚拟机固定ip"
date: 2023-07-13T21:17:54+08:00
lastmod: 2023-07-13T21:17:54+08:00
draft: false
keywords: ["Ubuntu","虚拟机"]
description: "Ubuntu虚拟机固定ip"
tags: ["服务器","技巧"]
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
### 做好备份
- 首先做好对于原有网络配置yaml文件的备份
```bash
sudo cp 01-network-manager-all.yaml 01-network-manager-all.yaml.bak
```

### 查看网络接口
```bash
ifconfig
```
![](https://cdn.jsdelivr.net/gh/mazy699/PicGo@main/img/202307132056784.png)
### 修改配置文件
**00-installer-config.yaml**
```yaml
network:  
  renderer: NetworkManager  
  ethernets:  
    ens33:  
      addresses:  
        - 192.168.31.128/24  
      routes:  
        - to: default  
          via: 192.168.31.1  
      nameservers:  
        addresses:  
          - 8.8.8.8  
          - 114.114.114.114  
  version: 2
```
- 在上面的文件中，我们使用了以下内容：
    - ens33：接口名称
    - addresses：用来设置静态IP
    - nameservers：用来设置 DNS server
    - routes： 用来设置网关
    - 这里的ens33 就是我们上边看到的接口
    - 这里的192.168.31.128就是我们想要固定到的静态ip，/24表示的则是子网掩码的前缀长度（/24 对应了255.255.255.0）
    - 这里的routes则是路由器的ip地址，可以将其中的192.168.31.1替换为你的路由器ip
    - 这里的nameservers是域名解析服务器，除了路由器以外还添加了114.114.114.114 备用
    - 这里的renderer指的则是我们选用的网络控制方式，Netplan同时支持networkd和NetworkManager这两种方式作为后台。区别在于networkd是Systemd的一部分，换句话说，是systemd当中的systemd-networkd在管理网络连接。另一方面，NetworkManager则是Gnome的一部分，你可以让Netplan使用NetworkManager作为后台，这对于桌面用户很有用。至此，我们的配置已经修改完毕了，接下来我们应用修改。
- 要使上述更改生效
```bash
sudo netplan apply
```
