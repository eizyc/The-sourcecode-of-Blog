title: Webpack4
tags:
  - Webpack
  - ''
categories:
  - 前端
date: 2019-03-31 23:09:00
author:
---
安装本地的webpack，指令 npm install webpack webpack-cli -D



1. 打包的配置文件
![upload successful](/images/pasted-96.png)
<!--more-->

2. 默认配置文件的名字是webpack.config.js和package.json放在一个级别下。具体的流程是在命令行里执行npx webpack执行打包，这时webpack会去node_modules里的webpack_cli的

![upload successful](/images/pasted-93.png)
在这一行可以修改配置文件的名字（这里就是配置文件的配置文件）

![upload successful](/images/pasted-94.png)

使用这个指令选择配置文件来打包
![upload successful](/images/pasted-97.png)

还可以在package.json里,改

![upload successful](/images/pasted-99.png)
在命令行里执行 npm run build


![upload successful](/images/pasted-100.png)
为了实现通过服务器来访问资源，安装插件
它并不生成打包文件，将打包的文件放在缓存中，供服务器加载

![upload successful](/images/pasted-101.png)
在webpack.config.js里配置服务器,别忘了服务器根目录会默认找index.html


但是呢，如果dist目录不存在，server就找不到，就不会运行，我们希望源码在src里（html和js），希望能够打包后的js能插到html并且把结果放在dist目录下
这时需要引入插件，HtmlWebpackPlugin，但是


![upload successful](/images/pasted-102.png)
在webpack.config.js里require


![upload successful](/images/pasted-103.png)
配置plugins
注意这个插件，会根据模板，生成打包，但是这个结果在缓存中，打包文件是不可见的。

![upload successful](/images/pasted-104.png)


-------
#### 压缩


![upload successful](/images/pasted-108.png)

这时再打包，就会在目标文件夹里（contentBase文件夹），没有的话会新建，index.html以及入口js打包的js，并将打包的js插到html里，其中hash是生成哈希戳
![upload successful](/images/pasted-105.png)
如果需要文件名修改hash,如下若是hash：8表示，8位hash，这可以解决缓存问题
如果文件没有改，这个文件后的hash是不会改的
![upload successful](/images/pasted-109.png)

-----
#### 加载css模块

首先不能在html里写一个<link src="./style.css">原因在于，html将作为模板，最后输出到目标的输出文件夹里，也就是说，webpack会解析为纯文本，那么css并不会被当中模块被加载进来，所以我们要将css包装成一个模块，我们才能引入。所以我们需要loader
注意node里css里是可以引css的，如下（一定要注意；号不可以省略）
![upload successful](/images/pasted-115.png)
先安装loader
![upload successful](/images/pasted-110.png)
在webpack的配置文件里配置插件
![upload successful](/images/pasted-113.png)
这样在浏览器里查看时，会发现在head标签底部

![upload successful](/images/pasted-116.png)
修改配置文件

![upload successful](/images/pasted-117.png)
就会插到自己写在head里的css样式（pink）的上面

![upload successful](/images/pasted-118.png)
还可以解析less，和上面同理,但是要注意顺序，从右到左执行，所以要放在最右，记得在js文件里require，less文件和npm install less less-loader -D

![upload successful](/images/pasted-119.png)

如果我想抽离css样式，写成link的形式，安装这个插件

![upload successful](/images/pasted-120.png)

在webpack配置文件里引入
![upload successful](/images/pasted-121.png)
将loader修改
![upload successful](/images/pasted-122.png)
最终效果
![upload successful](/images/pasted-123.png)

如果需要给浏览器自动加前缀，叫postcss-loader和autoprefixer
![upload successful](/images/pasted-125.png)
和上面一样写在rules里，可以给一个options，参考[webpack4 css添加浏览器前缀 postcss-loader](https://www.cnblogs.com/RoadAspenBK/p/9342850.html)，也可以像下面这样，和package.json文件一个位置创建postcss.config.js
![upload successful](/images/pasted-126.png)
效果如下
![upload successful](/images/pasted-124.png)

再来压缩css，安装插件
![upload successful](/images/pasted-128.png)
配置，其实这些具体还是要去npm官网查看，因为也不知道什么时候会换标准
![upload successful](/images/pasted-129.png)
![upload successful](/images/pasted-130.png)
效果
![upload successful](/images/pasted-131.png)
tips： optimization: 优化项,只有在生产模式才会生效，如果是development就不会走optimization

压缩js

引入bable-loader，@babel/core核心模块，@babel/preset-env转换模块
![upload successful](/images/pasted-132.png)
增加配置文件
![upload successful](/images/pasted-133.png)
如果需要添加es7的语法（如类，装饰器），需要添加插件
![upload successful](/images/pasted-137.png)
类
![upload successful](/images/pasted-138.png)
装饰器
类转换的
![upload successful](/images/pasted-134.png)
写入rules
![upload successful](/images/pasted-136.png)
装饰器的,在babel网站搜索
![upload successful](/images/pasted-140.png)
按照文档配置
![upload successful](/images/pasted-141.png)

![upload successful](/images/pasted-142.png)
其实我没有弄成功，因为不知道装饰器是个啥...等以后回来再配置