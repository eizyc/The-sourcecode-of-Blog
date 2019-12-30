title: node的npm的坑
tags: []
categories:
  - 前端
date: 2019-03-26 18:12:00
author:
---
今天在写Angular项目的时候,想引入jquery和bootstrap，按照正常的,
ng new projectname ,然后angular会自动调npm下载相关的包，但是会卡，因为是npm的国外的源。
所以我换镜像源了cnpm，跳过npm，用cnpm install --save来安装。后面的jquery和bootstrap也是用的cnpm.后来知道错了。
因为angular是用typescript开发的，我们需要先安装类型描述文件，让TypeScript认识jquery。cnpm install @types/query --save-dev
<!--more-->
         
![upload successful](/images/pasted-35.png)
最后在在angular.json里修改上图的路径（angular4以前是angular-cli.json）

最后问题来了，我的样式怎么都显示不了。
最后发现是node_modules里的文件名的问题，比如bootstrap，会有一个_bootstrap@3.7.7的文件夹和bootstrap文件夹

![upload successful](/images/pasted-36.png)
区别在于下划线的是cnpm安装的包，不带的是npm安装的包

最后解决方法是，用nrm给npm换源

参考这篇博客
[用nrm一键切换npm源](https://www.cnblogs.com/wangmeijian/p/7072053.html)

这个和cnpm还是有区别的，总之尽量别用cnpm
有些自动安装脚本的包cnpm也有坑。
最后这样新建项目的node_modules里就没有下划线的文件啦~
可以开心地继续写项目啦