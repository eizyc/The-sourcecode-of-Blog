title: SHELL编程
tags: []
categories:
  - 嵌入式
date: 2019-03-31 11:18:00
author:
---


参考这个视频进行学习，[shell编程从入门到精通](https://www.bilibili.com/video/av17384556/?spm_id_from=333.788.videocard.3)


Linux Shell种类非常多，最常用的就是bash。#!是特殊的表示符，其后面跟的是此解释此脚本的shell的路径
<!--more-->

[shell脚本头,#!/bin/sh与#!/bin/bash的区别.](https://www.cnblogs.com/jonnyan/p/8798364.html)

vi first_shell.sh
进入vi后
```shell
#!/bin/bash
#Filename:first_shell.sh
#auto echo hello world!
#by authors cyz 2019

echo "Hello world!"
```
上面#这些都是注解，#!/bin/bash是定义这是一个shell脚本

：wq！之后执行

![upload successful](/images/pasted-60.png)



---
###### shell编程的变量详解
shell变量分为局部变量和环境变量。局部变量只在创建它们的shell脚本中使用，而环境变量在创建它们的shell及其派生出来的任意子进程中使用。有些变量是用户创建的，其他的则是专用shell变量


![upload successful](/images/pasted-61.png)


![upload successful](/images/pasted-62.png)



![upload successful](/images/pasted-63.png)


![upload successful](/images/pasted-65.png)

![upload successful](/images/pasted-64.png)
 
这种效果 [格式: echo -e "\033[字背景颜色;字体颜色m字符串\033[0m"](https://blog.csdn.net/panpan639944806/article/details/23930553/)
有两个\033,一个对应它们后面的一串字符串，如果把后面那个删掉，效果为：

![upload successful](/images/pasted-68.png)
下面那一行会这样是因为，没有\033就会和上面一样的样式输出。

---
###### shell编程之IF条件语句

```shell
if（表达式）  #if（Varibale in Array）
语句1
else
语句2
fi
```
在if里两个小括号(())和比较大小有关，比如

```shell
if(($num1 > $num2));then
	echo "This $num1 is greater than $num2"
else
	echo "This $num1 is less than $num2"
fi
```
关于判断目录和文件
![upload successful](/images/pasted-66.png)

![upload successful](/images/pasted-67.png)

![upload successful](/images/pasted-69.png)
两个[[]]是判断大小，[]是判断文件，两个(())是计算


![upload successful](/images/pasted-70.png)
-z是判断字符串不为空

/bin/bash -n xx.sh，-n是测试的意思

"-n"可用于测试shell脚本是否存在语法错误，但不会实际执行命令。在shell脚本编写完成之后，实际执行之前，首先使用"-n"选项来测试脚本是否存在语法错误是一个很好的习惯。因为某些shell脚本在执行时会对系统环境产生影响，比如生成或移动文件等，如果在实际执行才发现语法错误，您不得不手工做一些系统环境的恢复工作才能继续测试这个脚本。

---
###### 编写MySQL备份脚本
``代表反引号里的字符串按照指令返回，返回的结果作为值


![upload successful](/images/pasted-71.png)
如何每天按时运行

![upload successful](/images/pasted-73.png)

![upload successful](/images/pasted-74.png)
添上这个指令，前5个数字是分时日月星期,,>>是输出写到log里

---
###### LAMP一键安装脚本