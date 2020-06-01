# XML和JSON笔记

前言：分两个部分。

XML笔记：介绍、使用

## 一、XML笔记

介绍：XML（extensible markup language）可扩展标记语言。被设计用于传输和储存数据。

用途：把数据从HTML文档中分离出来，简化数据共享和传输

树结构：从根部开始，扩展到枝叶

第一行是声明

根元素

子元素

 

 

使用：

```
<?xml version="1.0" encoding="UTF-8"?>

 <note> 

<to>Tove</to> 

<from>Jani</from> 

<heading>Reminder</heading> 

<body>Don't forget me this weekend!</body> 

</note>
```

 

## 二、JSON笔记

介绍：json(JavaScript object notation)JavaScript对象表达法。类似xml，但比XML更小、更快、更易解析。常用于与服务端交换数据，在接收服务器数据时一般是字符串。

对象：{}

访问对象值、循环对象、嵌套json对象

修改值：myobj.sites[“site1”]=”hello”;

删除对象属性：delete

 

数组：[]

对象中的数组、循环数组、修改数组值、删除数组元素。

 

将数据转换为JavaScript对象：JSON.parse(text[,reviver])

将JavaScript对象转换为字符串：JSON.stringify[,replacer[,space]])

 

使用：

{ "sites": [ 

{ "name":"菜鸟教程" , "url":"www.runoob.com" }, 

{ "name":"google" , "url":"www.google.com" }, 

{ "name":"微博" , "url":"www.weibo.com" } 

] }

 