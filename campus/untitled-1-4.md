# 输入网址后发生了什么？

一道很常见的面试题，但是感觉之前回答的时候都不够详细，今天有时间就详细的归纳一下。

1. 解析URL
2. 查询缓存
3. 通过DNS获取IP
4. 建立TCP连接
5. 发送HTTP请求
6. 获取HTTP响应结果
7. 浏览器解析渲染页面

## 1.解析URL

判断用户输入是否为合法的URL，并判断对应协议。若不是合法URL，则用浏览器默认搜索引擎搜索关键字。

## 2.查询缓存

查询浏览器中是否有对应网页的缓存（Expires或Cache-Control未过期），如果有缓存则直接使用缓存中的文件。

## 3.通过DNS获取IP

现在我们有了网站的URL，但是浏览器只能根据IP地址找到服务器的位置，所以需要通过DNS获取URL对应的IP地址。首先，查询浏览器以及操作系统中的DNS缓存，再查询本地host文件，如果还未找到的话，就向自己的DNS服务器查询。

## 4.建立TCP连接

三次握手：首先客户端发送一个SYN=x的包，服务器接收到后返回SYN=y,ACK=x+1的包，最后客户端再回传一个ACK=y+1的包

## 5.发送HTTP请求

用已经建立的TCP连接把HTTP请求报文发送给客户端

> 如果是HTTPS的话还需要经过SSL/TLS层加密

## 6.获取HTTP响应结果

服务器返回HTTP响应报文

> 如果是HTTPS的话还需要先用密钥解密

## 7.浏览器解析渲染页面

解析HTML,CSS,JS，构建CSSOM，DOM树，并渲染

如果有其他资源（如图片等）则跟上述过程一样请求
