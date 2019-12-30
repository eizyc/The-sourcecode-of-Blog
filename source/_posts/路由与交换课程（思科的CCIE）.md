title: 路由与交换课程（思科的CCIE）——1(硬件架构和指令)
tags:
  - 思科
categories:
  - 计算机网络
  - ''
date: 2019-03-17 09:26:00
author:
---
1(硬件架构和指令)

#### 设备硬件架构
- 1.路由器(三层)硬件架构
    - 1.1运算系统
        - 1.1.1 引擎 \(supervisor\),CPU
    - 1.2存储系统
        - 1.2.1 FALSH\(硬盘\) 
        - 1.2.2 RAM\(内存)
        - 1.2.3 ROM\(只读存储器==CMOS/BIOS\)
        - 1.2.4 NVRAM\(非易失性存储器\)
    - 1.3 电源系统
    - 1.4 外围系统
        1. 插槽
        2. 接口
        
        <!--more-->
- 2.FLASH
    - 2.1功能：放置操作系统镜像 \(互联网操作系统(Internetwork Operating System,简称IOS\)
    - 2.2注意：不需要安装，即丢即用

- 3.ROM \(只读存储器\)
    - 3.1功能：用于系统故障恢复及高级操作
    - 3.2组成：
       - 3.2.1POST程序 \(Power\-on self Test 加电自检，检查硬件\)
       - 3.2.2BootStrap程序 \(启动引导程序，就像Linux里的Grub引导程序，把操作系统搬到内存里\)
       - 3.2.3ROMMON程序\(ROM Monitor 类似WinPE，通过另一个系统对原来的系统操作。它可以用来破解路由器密码，系统升级恢复\)
       - 3.2.4MiniIOS镜像\(小型操作系统，当FLASH里的坏了后，加载这里的操作系统。现在很多都放在FLASH里了，不放在ROM里了\)
    
- 4.NVRAM\(非遗失性存储器\)
    - 4.1功能：用于保存配置及配置寄存器，实现了一个硬件上的安全隔离
 
- 5.路由器的启动流程

```flow
st=>start: 开机
e=>end: 正常运行
op1=>operation: 加电自检(POST)
保证硬件正常
op2=>operation: 加载并引导执行引导程序
Bootstrap
op3=>operation: 寻找IOS映像文件
FALSH
op4=>operation: 加载IOS映像文件
到内存
op5=>operation: 寻找配置文件
NVRAM
op6=>operation: 加载配置文件
到内存

st->op1->op2
op2->op3
op3->op4
op4->op5
op5->op6
op6->e
```

![upload successful](/images/pasted-18.png)
- 6.交换机（二层）硬件架构
    - 6.1与路由器的区别1：没有NVRAM,把配置文件放在FLASH中,所以在FLASH中除了操作系统还有配置文件
    - 6.2与路由器的区别2：RoMMon程序变成Switch模式，功能类似
    - 6.3与路由器的区别3：所以启动流程中，去NVRAM找配置文件，其他一样
---

#### IOS基础操作
1. IOS概述
Internetwork operation system
网际操作系统
2. 操作模式

```flow
op1=>operation: 用户模式>
普通用户0-1
op2=>operation: 特权模式#
管理员2-14
op3=>operation: 全局模式（config）
超级管理员15


op1->op2
op2->op3

```
3. 等级切换（返回上一级都是exit,end直接到特权）
   - 用户模式
   - 特权模式（enable命令/en）
     - 功能：查看更多系统信息 
        + show  flash 读flash
        + show  run 读内存
        + show start 读NVRAM
        + show diag 查看硬件板卡信息
        + clock set 
        + show 可以换成dir，类似与linux
        + show ip interface brief 查看三层简要信息 
        + show ip interface f0/0 查看三层信息
        + show interface f0/0 查看接口二层详细信息
        + show cdp neighbors 查看思科设备的邻居信息 ,cisco discover potocal
        + show arp 查看ip到mac的映射（主机上的操作是arp-a）
        + ctrl+shift+6终止
        
     - 实现系统的备份,升级等操作
     - 实现远程登录
     - 实现连通性测试
   - 全局模式(congfigure terminal/conf t)     
        + hostname xxx命名
        + no ip domain lookup不要域名解析
        + line console 0 (网络设备一般有一个console口，对它进行配置，line表示登录连线，telnet就是line vty 0)
        + exec-timeout 1 1（一分钟一秒如果没有动，就退出特权模式。若是 0 0就是不退出）
        + no exec(千万不要输，意思是不给界面)
        + logging synchronous（输出同步）
        + interface f0/0（进接口）
        + no shutdown（打开接口）
        + ip add 10.1.1.1 255.255.255.0
        + description xxx（描述接口）
---
#### IOS进阶操作

  - 管理方式
     + outbound带外管理（console）
     + inbound带内管理（Telnet,SSH,HTTP）这些都是VTY
     + 为何是带内带外，指的是这个line和用户的http是不是一起的
  - 密码
     + 用户密码
        - 全局模式下
        - line console 0
        - 或者line vty 0 4
        - password xxx
        - login（这个一定要）
        - 第二种：username xx password xxx
        - line console 0或者vty
        - login local（调用本地数据库）
     + 特权密码
       - 全局模式下
       - enable password xxx
       - 把password换成secret就可以加密，在show run里就不会明文显示
       - service password encryption开启全局密码加密
     + 特权级别设置
       - line con 0
       - priviledge level 0-15
       - 或者特定用户特定级别
       - username xx priviledge 15 secret xxx
       - 后面和上面的一样
     
 - 配置管理
    + 保存配置
       - copy run start
    + 删除配置
       - 删除RAM 命令前加no 
       - 删除NVRAM write erase
       - reload 重启设备
    + 备份配置