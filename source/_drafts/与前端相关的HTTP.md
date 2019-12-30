title: 与前端相关的HTTP
tags: []
categories: []
date: 2019-03-28 16:21:00
author:
---
###### 1.HTTP发展历史
   + HTTP/0.9
     + 只有一个命令GET
     + 没有HEADER等描述数据的信息
     + 服务器发送完毕，就关闭TCP连接
    
    <!--more-->
   + HTTP/1.0
    + 增加了很多命令
    + 增加status code和header
    + 多字符集支持、多部分发送、权限、缓存等
   + HTTP/1.1（目前主流）
    + 持久连接，创建TCP连接后，可以不关闭
    + pipeline 可以在同一个连接里发多个请求，但是服务端返回必须按请求的顺序返回，所以必须等待前一个请求处理完才能发送，这是一个串行并行处理的问题。在HTTP/2.0中可以解决
    + 增加host和其他一些命令，host字段可以实现在同一个物理服务器，集群上部署请求多个web服务
   + HTTP2
    + 所有数据以二进制传输（以帧传输）
    + 同一个连接里面发送的多个请求不再需要按照顺序来（实现并行）
    + 头信息压缩以及推送（服务端主动）等提高效率的功能，推送的话有一个好处，比如html和css，js可以并行传输，提高效率
    + 推荐参考资料：[前端开发与 HTTP/2 的羁绊——安利篇](https://aotu.io/notes/2016/03/17/http2-char/)

###### 2.HTTP(TCP)的三次握手

![upload successful](/images/pasted-37.png)

为什么需要三次呢？避免端口，网络服务因为网络原因等待而浪费

###### 3.HTTP中的URI、URL、URN
   + URI 统一资源标识符（Uniform Resource Identifier)
     用来唯一标识互联网上的信息资源，包括URL和URN
   + URN 永久统一资源定位符（Uniform Resource Name)
  
  在资源移动之后还能被找到，目前还没有非常成熟的使用方案
   + URL 统一资源定位器（Uniform Resource Locator)
   
   如：
   http://baidu.com:80/path?string=aa#hash
   
   第一部分，模式/协议（scheme）：它告诉浏览器如何处理将要打开的文件。最常用的模式是超文本传输协议（Hypertext Transfer Protocol，缩写为HTTP），这个协议可以用来访问网络。
   
   第二部分，文件所在的服务器的名称或IP地址，后面是到达这个文件的路径和文件本身的名称。服务器的名称或IP地址后面有时还跟一个冒号和一个端口号。它也可以包含接触服务器必须的用户名称和密码。路径部分包含等级结构的路径定义，一般来说不同部分之间以斜线（/）分隔。询问部分一般用来传送对服务器上的数据库进行动态询问时所需要的参数。path是路由，hash代表文档的某个片段，a标签中的href锚点
   
   注意，域名的解析是从后往前的
   如下是百度百科的域名，和www.baidu.com对比，会发现是在最前面发生变化
   
![upload successful](/images/pasted-38.png)
www反而是最后被解析的
其实正确的解析应该是先.。再比如www.baidu.com.,应该是带一个.的，但是现在的ISP运营商会有一个地址的映射备份，就不最先从.开始了，从com开始。
     
###### 4.HTTP的报文形式
 
![upload successful](/images/pasted-40.png)

请求报文：

GET这一行是首行(General)，并不属于 HTTP 的 headers，这个 GET 是 http 的Method，用来定义对资源的操作。其实这些 Method 是一种"协议"，也可以用其他的词，服务器做其他的处理，但是这样是违背HTTP的语义化定义，我们应该规范使用，虽然HTTP没有强制规范。  
红线是url中的路由部分，不会有地址，因为连接已经完成了，之后是协议的版本
下面的一个板块就是header
 
 
请求报文：
 
第一个为协议版本，第二个为HTTP的响应码（参考文末博文）服务器对请求的处理结果，第三个是响应码的含义，用明文告知 。 
好的 HTTP 服务可以通过 CODE 判断结果，而不是统统200，用里面的字段来判断。
 
**注意：request和respone的首部都要空一行，才能到主体部分。**
 
###### 5.HTTP中浏览器的同源策略
 
 参考下一篇
 
###### 6.CORS跨域限制以及预请求验证
 
   + CORS限制（除了下面允许的，其他都需要预请求）
       + 跨域中允许的方法：GET，HEAD，POST
       + 跨域中允许的Content-type：text/plain，multipart/form-data，application/x-www-form-urlencoded
       + 其他限制
       1.请求头的限制（如下是允许的）
       ![upload successful](/images/pasted-41.png)
       2.XMLHttpRequest对象均没有注册任何事件监听器
       3.请求中没有使用ReadableStream对象
       
   + 解决方法（预请求）
   在服务端增加字段，如
   

![upload successful](/images/pasted-44.png)
![upload successful](/images/pasted-42.png)
服务端操作

![upload successful](/images/pasted-47.png)

先发送预请求，预请求通过，再发送正式请求

![upload successful](/images/pasted-48.png)

 + 5.HTTP中的缓存头Cache-control（可以设置多个值）
    + public(Http经过的都可以)，private（发送请求的浏览器可以），no-cache(任何结点都不可以,本地可以存缓存，但是必须服务器验证）
    + 到期 max-age=<seconds>缓存到多少秒之后才会过期，过期后浏览器才会再次请求；s-maxage=<seconds>在代理服务器中，会代替max-age；max-stale=<seconds>在发起端设置，即便缓存过期，在这个时间内，还是可以使用过期的缓存，不需要去服务器请求
    + 重新验证 must-revalidate 缓存过期必须去服务器验证；proxy-revalidate同理，用在缓存服务器中
    + 其他 no-store,本地和代理服务器都不可以存；no-transform代服务器不要改变内容
    + Tip:我们希望浏览器缓存我们的静态资源，但是服务端的更新也要及时反馈，解决方案为：打包完成的js加上一段特别的一串哈希。
  
 + 6.缓存验证Last-Modified和Etag的使用 
 
   + 浏览器对获取资源的过程：
   ![upload successful](/images/pasted-49.png)
   + 如何验证：
     + Last-Modified 上次修改时间
   配合If-Modified-Since或者If-Unmodified-Since使用
   对比上次修改时间以验证资源是否需要更新
    + Etag数据签名
     根据内容产生唯一的签名
     配合If-Match或者If-Non-Match使用
     对比资源的签名判断是否使用缓存
     具体过程大概是，在 "max-age"很大的情况下，不考虑因为超时带来的影响，第一第请求的时候请求头不带Etag和Last-Mpdified，但是返回头回带，下一次请求时，就带着If-Match和If-Modified-Since可以用来判断，服务端的处理可以如下
    
![upload successful](/images/pasted-50.png)
注意如果返回304，是没有返回body的，但是浏览器会从缓冲中找，所以在开发者工具中，是会有显示的，显示的为缓存的值。


###### 7.Cookie和Session
   1. Session
Cookie只是Session的一种表达方式。还可以用JS写在header里
   2. Cookie是服务端通过Set-Cookie这个返回Header，设置到浏览器里的一个内容
 在之后的会话中会一直带着，是键值对，可以很多个
 
 ![upload successful](/images/pasted-51.png)
 
 cookie的一些属性
    + max-age和expires设置过期时间
    + Secure只在https的时候发送
    + HttpOnly无法通过document.cookie访问（防止CSRF攻击，禁止重要数据通过js访问）
    + 可以通过domain来设置二级域名的cookie，注意不能跨域，智能父给子级赋值cookie，不能子给父。
 
 + 8.HTTP的长连接
 只有同域的才会是同链接，一般HTTP1.1有6个信道，当六个HTTP链接都并发被占用时，请求还是要等待的。但是google现在是HTTP2.0，采用信道复用，所以只用一个HTPP链接即可。【google大法好🆗】
 
 
+ 9.数据协商
在客户端发送请求时，会声明自己想要的数据格式和数据限制，服务端会做出判断来返回。 
   + 请求
       + Accept 告诉服务端想要的数据
       + Accept-Encoding 限制服务端如何压缩数据
       + Accept-Language 判断返回的语言
       + User-Agent表示浏览器信息比如移动端，PC端
   + 返回
       + Content-Type 实际返回的数据格式，在Accept里选
       + Content-Encoding 服务端具体压缩方式
       + Content-Language 服务端具体返回语言
       

+ 10.Redirect

302重定向又称之为暂时性转移(Temporarily Moved )，英文名称：302 redirect。 也被认为是暂时重定向（temporary redirect），一条对网站浏览器的指令来显示浏览器被要求显示的不同的URL，当一个网页经历过短期的URL的变化时使用。一个暂时重定向是一种服务器端的重定向，能够被搜索引擎蜘蛛正确地处理.操作如下，如果重定向的话，响应码一定要写成302，不然就算写了location也没用

301转向(或叫301重定向，301跳转)是当用户或搜索引擎向网站服务器发出浏览请求时，服务器返回的HTTP数据流中头信息(header)中的状态码的一种，表示本网页永久性转移到另一个地址。它和302的区别在于，第一次访问时一样，但是第二次就会直接去重定向后的那个网站，而不是中间那个中转站。301会讲数据永久缓存，在用户主动清除之前，是不会被消除缓存的。
![upload successful](/images/pasted-54.png)

链接号
![upload successful](/images/pasted-53.png)
+ 11.CSP（Content Security Policy 内容安全策略）


+ 12.HTTPS
HTTP是明文传输，所以不安全
  + 私钥
  私钥只在服务器上
  + 公钥
  放在互联网上，所有人都可以得到
  
  公钥加密的内容，只有私钥可以解开，私钥加密的内容，所有的公钥都可以解开（当然是指和秘钥是一对的公钥）

这一章不细写了可以参考,
[HTTPS整套加密机制是如何实现的？](https://www.wosign.com/news/httpsjiami_20180817.htm)写的很明白，图文并茂🆗



 
[Http响应码，Http协议报文格式参考](https://blog.csdn.net/holmofy/article/details/68492045)