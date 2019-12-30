title: 路由与交换课程（思科的CCIE）——6（VLAN技术）
tags: []
categories:
  - 计算机网络
date: 2019-04-17 12:50:00
author:
---




Virtual Lan 虚拟局域网

如果一个交换机，遇到一个广播包比如ARP包，那么它会向所有网络发，所以需要隔离，划分Vlan

+ 有了Vlan可以隔离广播域（一个Vlan一个广播域）
+ 安全管理
+ 易于管理

Vlan的分类：
+ 数据Vlan
+ 语音Vlan
+ 管理Vlan
+ 自然Vlan
+ 私有Vlan

Vlan的范围<0~4094>：

![upload successful](/images/pasted-152.png)
默认情况下，所有默认接口放在Vlan1，Vlan1为管理Vlan
