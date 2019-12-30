title: 用到的系统指令
tags: []
categories: []
date: 2019-07-16 08:46:00
author:
---
#### 用到的系统指令
1. linux
  +  [** scp ** ](#1)
  +  [** firewall-cmd --state** ](#2)
2. windows


<span id="1"> </span>
+ ** scp **  
使用于：在hadoop本地向服务器传安装包时  
格式 ： scp hadoop-2.6.0-cdh5.15.1.tar.gz hadoop@192.168.199.233：~/software/  
Linux scp命令用于Linux之间复制文件和目录。
scp是 secure copy的缩写, scp是linux系统下基于ssh登陆进行安全的远程文件拷贝命令。

<span id="2"> </span>
+ ** firewall-cmd --state **  
使用于：hadoop检查防火墙状态时,停止服务是systemctl stop firewalld.service
CentOS 7中查看防火墙状态，[相关firewall-cmd指令](https://www.jianshu.com/p/411274f96492)