# AJAX笔记

## 前言：

## 一、简介

介绍：AJAX(Asynchronous javascript and xml)是一种使用现有标准的新方法，最大的优点是不重新加载整个页面的情况下和服务器交换数据并更新部分网页内容。

 

应用：用HTML+CSS表达咨询；用JavaScript操作DOM来执行动态效果；新浪微博、谷歌地图、开心网

 

工作原理：

XMLHttpRequest对象（异步的与服务器交换数据）

JavaScript/DOM（信息显示/交互）

CSS（给数据定义样式）

XML（作为转换数据的格式）

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

## 二、实例

创建XHR对象：XMLHttpRequest用于在后台与服务器交互数据。

请求： 使用XMLHttpRequest 对象的 open() 和 send() 方法；请求类型（与 POST 相比，GET 更简单也更快）、URL（服务器上的文件）、async参数

响应：使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性

Onreadystatechange事件：readystate属性存有XHR对象的三种属性（回调、状态、静态）

PHP/ASP：网页与web服务器进行通信。ShowHint()函数

数据库：AJAX从数据库读取数据。showCustomer()函数

XML：AJAX读取XML文件的信息：loadXMLDoc()函数

 

 

 

 

 

 

 

 