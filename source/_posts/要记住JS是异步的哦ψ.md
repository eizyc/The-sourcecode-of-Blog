title: 要记住JS是异步的哦ψ(._. )>
tags: []
categories:
  - 前端
date: 2019-03-30 19:28:00
author:
---
今天在写uni项目的时候，心态崩了

![upload successful](/images/pasted-55.png)
反正大概就是一个导航有三个tab，一个tab里的数据对应一个aryItem，一个aryItem里有loadingType（int）和data（array）属性。然后因为后端的接口这几个tab的接口是分开写的，所以第一个tab请求某某接口，第二个和第三个请求另外的，但是这里先写成空。
看似很合理，但是.....
<!--more-->

![upload successful](/images/pasted-56.png)
报错了耶QAQ
然后....调试了半天，问了大佬才明白
但是你这是异步的呀！！！！如果你ajax还没返回的时候后面的先执行了那就有可能第一个被后面两个顶掉了，就为空了呗，就取不到了呗(●'◡'●)

所以先初始化，再赋值就好啦

![upload successful](/images/pasted-57.png)
大概就是这样。

总结就是：
1.永远都要初始化用到的所以值，永远都不要信任后端给你返回的东西，自己要判空

2.充分理解异步的真正含义，虽然平时在学校里学的都是C，JAVA这些都是同步的语言（虽然也有异步的机制），但是在做前端的时候一定要时刻记住，异步！

3.连续用点取值的时候数据稍微不正常一点儿就会出事（ 指这样resdata.datas.a.b取值 ），中间某个undefined了后面就报错了。一般这种问题，不用库的话通常会写成  if(resdata&&resdata.datas&&resdata.datas.a) {你的逻辑}  或者用lodash的_.get  或者不想引入Lodash的话自己实现一个类似的工具函数用比如这样
![upload successful](/images/pasted-58.png)（对象，路径，默认值）

[Lodash
是一个一致性、模块化、高性能的 JavaScript 实用工具库。](https://www.lodashjs.com/)


最后，你觉得自己菜只是因为你踩的坑还不够多，加油

下个星期开启一周一章《数据可视化系列》周日准时更新( •̀ ω •́ )y