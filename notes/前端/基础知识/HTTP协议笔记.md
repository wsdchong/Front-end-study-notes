# HTTP协议笔记

## 前言：

介绍

## 一、介绍

HTTP（超文本传输协议Hypertext transfer protocol）

 

超文本：不仅传输文字，还传输图片、音频、超链接。

 

传输：请求方把传输数据包发给应答方

 

协议：网络传递的规范

 

网络模型：物理层、链路层、网络层、传输层、应用层

应用层：HTTP、电子邮件传输协议SMTP、端系统文件上传协议FTP、域名解析协议DNS

运输层：TCP协议、UDP协议

网络层：IP协议

链路层：

物理层

 

各大邮箱使用电子邮件传输协议，浏览器是使用HTTP协议的主要载体。

我们在地址栏输入URL，浏览器就向域名服务器提供网址（完成URL到IT地址的映射），在有服务器返回结果（HTML编码格式），浏览器执行HTML编码。

 

Web服务器、内容分发系统CDN

Web应用程序防护系统（web application firewall）是应用层面的防火墙

 

HTTPS（hyper text transfer protocol over securesocket layer）：HTTPS是以安全为目标的HTTP通道，在HTTP基础上通过传输加密和身份认证保证传输过程的安全性，在HTTP的基础上增加了SSL层。

 

HTTP报文：起始行（描述请求或响应的基本信息）、头部字段（使用key-value形式更详细地说明报文；消息正文（实际传输数据，纯文本或二进制数据）

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

HTTP请求方法：8种

GET获取资源

POST传输实体

PUT传输文件

HEAD获得响应首部

DELETE删除文件

OPTIONS询问支持的方式

TRACE追踪路径

CONNECT要求用隧道协议连接代理。

 

HTTP请求URL：

协议、主机、端口、路径、查询、片段。

响应状态码

 

## 二、HTTP优缺点

优点：

简单、灵活、易于扩展

应用广泛、环境成熟

无状态

 

缺点：

无状态

明文：协议中的报文不使用二进制数据，而是文本形式。用wireshark抓包，直接用肉眼查看和修改，方便调试。但是不安全，无法判断通信双方的身份。

性能

 

