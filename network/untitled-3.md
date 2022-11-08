# OSI 七层模型

从上到下分别有应用层，表示层，会话层，传输层，网络层，数据链路层，物理层共七层

(另TCP/IP模型有应用层，传输层，网络互联层，网络接口层共四层)

![OSI七层模型](https://raw.githubusercontent.com/hongzzz/blog/master/image/OSI%E4%B8%83%E5%B1%82%E6%A8%A1%E5%9E%8B.png)

## 应用层

应用层（Application Layer）提供为应用软件而设的接口，以设置与另一应用软件之间的通信。

> HTTP，HTTPS，FTP，TELNET，SSH，SMTP，POP3，DHCP，DNS

## 表示层

表达层（Presentation Layer）把数据转换为能与接收者的系统格式兼容并适合传输的格式。

## 会话层

会话层（Session Layer）负责在数据传输中设置和维护计算机网络中两台计算机之间的通信连接。

## 传输层

传输层（Transport Layer）把传输表头（TH）加至数据以形成数据包。传输表头包含了所使用的协议等发送信息。

> TCP，UDP，TLS

## 网络层

网络层（Network Layer）决定数据的路径选择和转寄，将网络表头（NH）加至数据包，以形成分组。网络表头包含了网络数据。

> IP，ARP

## 数据链路层

数据链路层（Data Link Layer）负责网络寻址、错误侦测和改错。当表头和表尾被加至数据包时，会形成帧。数据链表头（DLH）是包含了物理地址和错误侦测及改错的方法。数据链表尾（DLT）是一串指示数据包末端的字符串。

> 以太网，Wi-Fi

## 物理层

物理层（Physical Layer）在局部局域网上传送[数据帧](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%B8%A7)（data frame），它负责管理计算机通信设备和网络媒体之间的互通。包括了针脚、电压、线缆规范、集线器、中继器、网卡、主机适配器等。

> 线路，无线电，光纤
>
> 参考 [维基百科](https://zh.wikipedia.org/wiki/OSI%E6%A8%A1%E5%9E%8B)
