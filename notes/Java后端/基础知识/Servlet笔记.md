时间：2020/3/26

来源：https://www.runoob.com/servlet/servlet-environment-setup.html

前言：介绍和安装、使用

## 一、介绍和安装

介绍：运行在服务器的程序，作为HTTP客户端的请求和HTTP服务器上数据库之间的中间层。

可以收集来自网页表单的用户输入，呈现来自数据库的记录，可以动态创建网页。

环境设置：设置Java开发包、web服务器

生命周期：初始化：init；处理客户端的请求：service、doGet\doPoat；终止：destroy

## 二、使用

表单数据：GET方法、POST方法

客户端HTTP请求：

服务器HTTP响应

HTTP状态码

编写过滤器：filter（身份验证、数据压缩、日志记录等）

异常处理<error-page>

Cookie处理：存储在客户端计算机上的文本文件。

三种维持客户端与服务器之间的Session会话跟踪：cookies、隐藏的表单字段、URLC重写

数据库访问：JDBC

文件上传：upload文件上传表单、message上传成功跳转页面、uploadsevlet上传处理servlet

处理日期：date

网页重定向

点击计数器

自动刷新页面：setIntHeader

发送电子邮件

包

调试：system.out.printIn、消息日志、使用JDB调试器、注释、客户端和服务器端头信息