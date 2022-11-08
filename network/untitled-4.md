# HTTP 报文格式

HTTP报文分为**请求报文**与**响应报文**两种

## 维基百科简介

> * 请求行，例如：`GET /logo.gif HTTP/1.1`或[状态码](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)行，例如：`HTTP/1.1 200 OK`，
> * [HTTP头字段](https://zh.wikipedia.org/wiki/HTTP%E5%A4%B4%E5%AD%97%E6%AE%B5)
> * 空行
> * 可选的HTTP报文主体数据
>
> 请求/状态行和标题必须以 结尾（即[回车](https://zh.wikipedia.org/wiki/%E5%9B%9E%E8%BB%8A)后跟一个[换行符](https://zh.wikipedia.org/wiki/%E6%8D%A2%E8%A1%8C%E7%AC%A6)）。 空行必须只包含 ，而不能包含其他[空格](https://zh.wikipedia.org/wiki/%E7%A9%BA%E6%A0%BC)。

## 组成

由请求行，首部行，实体主体三部分组成

![请求报文](https://raw.githubusercontent.com/hongzzz/blog/master/image/http%E8%AF%B7%E6%B1%82%E6%8A%A5%E6%96%87.png)

### 请求行

请求报文 `方法名 + URL + 协议版本` 如`GET /logo.gif HTTP/1.1`

响应报文 `协议版本 + 状态码 + 状态码的文本描述` 如 `HTTP/1.1 200 OK`

### 首部行

如`Accept: text/plain`

### 实体主体

可选，与首部行之间有一个空行，一般存放POST/PUT的信息
