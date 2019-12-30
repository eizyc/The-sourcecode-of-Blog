title: v2ray的客户端在ubuntu下的配置过程
tags: []
categories:
  - 计算机网络
  - 后端
date: 2019-04-09 14:26:00
author:
---
首先如何搭建服务端的v2ray就不说了，这里说几个要点：
1. 注意时间服务端的时间和客户端的时间不能超过两分钟，如果死都连不上，注意看下时间
2. 使用xshell连接，别用什么putty巨卡
3. 代理模式中的PAC指的是，如果不需要翻墙的请求，它就不会代理，也就是不翻墙咯
4. 去github上搜脚本在服务端安装就好，大把多

<!--more-->

接着是客户端的安装

1.下载v2ray,其实服务端和客户端的v2ray是一样的。= =，选择合适自己的版本就好，之后解压
[v2ray下载](https://github.com/v2ray/v2ray-core/releases/)

2.安装

我们需要一个配置文件，这个文件可以自己部署好了之后，使用脚本导出，也可以在Windows 上用软件导出，更可以自己写，对照[官方文档](https://www.v2ray.com/)

配置文件config.json移到刚刚下好的文件夹中，把里面的vpoint_vmess_freedom.json删除了，这是默认的配置文件.
然后我们在文件夹中打开终端执行sudo ./v2ray


![upload successful](/images/pasted-144.png)

成功

3. 代理设置
最好使用Chrome和Firefox浏览器，因为我们需要下载插件 SwitchyOmege，Chrome上叫做 Proxy SwichyOmega，应用商店下载就行

打开拓展

新建情景模式

![upload successful](/images/pasted-145.png)

![upload successful](/images/pasted-146.png)

下面填上这个
```
"local_address":"127.0.0.1"
"local_port":1080
```

新建一个情景模式，这次选择自动切换模式


![upload successful](/images/pasted-147.png)


![upload successful](/images/pasted-150.png)

规则列表网站填这个

https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt

点击立即更新情景模式

然后应用更改

然后就可以开始上网了，你以为这就完了吗，没有，下面还有

设置桌面项

我们除了像上面那样使用
```
sudo ./v2ray

```
还可以

```
./v2ray --config=/到这个文件夹的路径/config.json
```
我们甚至还可以建立一个桌面项，然后双击启动

```
[Desktop Entry]

Name=V2Ray

GenericName=V2Ray Client

Comment=A platform for building proxies to bypass network restrictions.

Exec=/到你文件夹的路径/v2ray --config=/到你文件夹的路径/config.json

Icon=/到自定义图标图片的路径

Terminal=true

Type=Application

Categories=Network;Internet;
```

然后记得勾选允许作为程序执行文件
就可以双击执行V2Ray了(关闭终端即关闭程序).

若要想这个桌面项出现在应用程序列表里,那就把 v2ray.desktop 文件复制到 /usr/share/application里即可(需要root)


![upload successful](/images/pasted-151.png)

其实就是复制这篇（害怕到时候链接失效了....就copy下来一份(●'◡'●)）

[Linux 系统下v2ray客户端使用](https://octopuspalm.top/2018/08/18/Linux%20%E7%B3%BB%E7%BB%9F%E4%B8%8Bv2ray%E5%AE%A2%E6%88%B7%E7%AB%AF%E4%BD%BF%E7%94%A8/)