title: SSR 服务端渲染以及技术栈的一点思考
date: 2019-12-04 17:11:55
tags:
author:
---
> 我之前就一直有一个疑问，SSR 是不是意味着网站开发从现在的这种前后端分离，又要回到 JSP 模式去了。当然我知道不可能，所以我就去看了看哪些网站在用 SSR 。  
<!--more--> 
##### 1.关于 SSR
SSR：Server Side Render 服务端渲染。  
页面 = 模板 + 数据  
这里的加号就是“渲染”。
+ 服务端渲染：渲染过程在服务器端完成，返回给客户端的是渲染好的页面。
+ 客户端渲染：把一个初始的页面返回给客户端，客户端再发送请求（Ajax），拿到数据后，再渲染。  
两者都有优缺点，具体可以看文章最后的[知乎链接](#refer)。

> 这里我想说一下我的观点，我认为我们前端想要的不完全等同于服务端渲染，因为完全的服务端渲染是类似写 Java 时的 JSP、Thymeleaf的这种不分前端后端的模式。我们只要在我们的 SPA 的模式下，解决客户端的一些弊端就是就好了。所以说，现在前端所说的服务端渲染，是吸取了服务端渲染优点的客户端渲染。要解决的问题有：
+ 首屏性能差
+ SEO
+ 白屏...

由于现在这种纯服务端渲染的的开发模式（不分前后端）已经很少了，所以后面提到的 SSR 指的都是我们前端想要的这种~

##### 2.如何确定一个网站是不是用了 SSR 呢?
我大概就是下面这三步
###### 2.1肯定用了服务端渲染的网页  
首先在 Chrome 的开发者工具里请求一个网页时，选择 Network 板块，只选择请求的 Doc 文件，你就会看到一个 html，点击 Preview 预览就好。如果预览里是有内容的，那就是服务端渲染了。
![upload successful](/images/pasted-212.png)
比如 github 的我打马赛克的部分，就是 SSR 了，它解决的就是首屏性能差和白屏的问题，可以看到旁边的 activity 板块还是异步请求的。 
###### 2.2根据 Preview 不能判断的网页
![upload successful](/images/pasted-211.png)  
这是掘金的首屏，就不像 github，它是全白，所以这其实是掘金可以优化的一个点。但是其实它也用了 SSR 在 SEO 上。比如：

![upload successful](/images/pasted-213.png)
其中 vue-meta 是一个 Vue 里优雅的方式设置 title 与 meta。
> 但是我也有不明白的地方，这个data-vue-meta如果查看请求，它的确是动态加载的，那这样的异步请求对 SEO 还有效？难道说 SEO 是访问页面的时候等待个几秒再读取页面的 meta 信息？ 这个问题 mark 一下。

###### 2.3如果没有 meta 也没有呢？

那就是纯 SPA 了，当然如果是个人网站不求曝光量的话无所谓，如果是公司，你赶快去面试，说这个可以优化，你绝对进（当然现在没有哪个公司会这么愚蠢了2333） 

##### 3.一些 SSR 的解决方案
github单独挑出来说、其他公司
###### 3.1Github的解决方案  
其实它根本没有什么解决方案，人家就是 Ruby 的 Rails 后端渲染的，需要解决啥问题？但是这也有一个弊端它的移动端还是用了基于 Jquery 的 Pjax，关于Pjax 实际上已经很少见了，它主要是用了 *pushState* 和 *replaceState*。这个强大的特性后来用到了单页面应用如：vue-router，react-router-dom。其实我也不是很清楚， github 明明在 2018 年就说了完全移除了Jquery,那为什么我的 Wappalyzer 还是检测到了 Pjax 插件...
###### 3.2其他公司
个人感觉国内的很多公司都没有像Github这种纯后端渲染的，就都是 Vue 用Nuxt，React 用 next.js吧。

参考资料：<span id="refer">
+ [知乎：有必要使用服务器端渲染(SSR)么？](https://www.zhihu.com/question/308792091?sort=created)
+ [每日 30 秒 ⏱ 掘金SEO大揭秘](https://juejin.im/search?query=%E6%8E%98%E9%87%91SEO&type=all)
+ [Ruby:后端渲染还是前后端分离？Listen to yourself.](https://ruby-china.org/topics/36915)