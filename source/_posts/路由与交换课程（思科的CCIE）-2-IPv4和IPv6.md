title: 路由与交换课程（思科的CCIE）——2(IPv4和IPv6)
tags:
  - 思科
categories:
  - 计算机网络
author: cyz
date: 2019-03-21 23:13:00
---
#### IP地址

 + 1.概述
   + IANA：The Internet Assigned Numbers Authority，互联网数字分配机构)
   + ISP:Internet Service Provider
 + 2.格式
   + 由32个bit位组成（43亿，但实际上并没有用到43亿，D和E类没有在用）
   + 网络号+主机号=IP
   + 基于技术分类
   <!--more-->
        + A： ![upload successful](/images/pasted-19.png)
但是并不是0.0.0.0~127.255.255.255，因为127被用作本地环回,0    也有其他作用，在下面会讲。所以是1~126.x.x.x
     
     + B:![upload successful](/images/pasted-20.png)
10000000.x.x.x~10111111.x.x.x
所以是128~191.x.x.x
    
    + C:同理110打头    
![upload successful](/images/pasted-22.png)
11000000.x.x.x~11011111.x.x.x
所以是192~223.x.x.x   

    + D:同理1110打头
11100000.x.x.x~11101111.x.x.x
所以是224~239.x.x.x  

    + E:同理11110打头
11110000.x.x.x~11110111.x.x.x    
  所以是240~x.x.x.x 
  
    + 注意：ABC类是商用，D作组播，E作科研
    
   + 基于应用分类
     + 私有地址(由RFC1918文档规定了三个段)
       1. 10.x.x.x
       2. 172.16.x.x~172.31.x.x
       3. 192.168.x.x
     + 公有地址
        除了私有，特殊，D，E类地址以外i基本都是公有
     + 特殊IP地址
       1. 本地环回地址,用于本地测试，方便实验
         127.x.x.x 一般会认为是127.0.0.1 实际127打头就可以
       2. 广播地址
         + 本地广播 255.255.255.255 本网段的广播
         + 定向广播 任意网段的广播 ping跨网段的广播
         + 注意不一定是255才是广播，比如1.2.3.127/25