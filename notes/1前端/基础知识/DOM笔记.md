# DOM笔记

## 前言：

简介、DOM访问、对象

## 一、简介

介绍：DOM（document object model）为文档对象模型，是HTML和XML文档的编程接口。定义了访问和操作HTML文档的标准方法。以树的结构表达HTML文档。

W3C标准：核心DOM、XML DOM、HTML DOM。

 

节点：整个文档是一个文档节点；整个HTML元素是元素节点；HTML元素内的文本是文本节点；每个HTML属性是属性节点；注释是注释节点；

HTML DOM将HTML文档视为树结构，这个结构叫做节点树。节点树中的节点彼此拥有层级关系。父节点、子节点、兄弟节点

 

DOM方法：在节点上执行的动作；

编程接口：编程语言对DOM进行访问的对象方法和对象属性。

对象方法有：getElementById(id)获取指定id的节点、appendChild(node)

 

DOM属性：在节点上设置和修改的值。

对象属性有：innerHTM（节点的文本值）、attributes（节点的属性节点）、parentNode（节点的父节点）、childNodes（节点的子节点）

 

## 二、DOM访问

DOM访问：访问HTML元素

DOM修改：修改元素、属性、样式、事件

document.getElementById("p1").innerHTML="新文本!";

document.getElementById("p2").style.color="blue";

onclick="document.body.style.backgroundColor='lavender';"

 

添加、删除和替换元素：

CreateElement()、insertBefore()、removeChild()、replaceChild()

 

事件：点击onmousedown、onmouseup、onclick、移动在元素上onmouseover、onmouseout

 

导航：通过DOM使用节点关系在节点树中导航

GetElementsByTagNome()方法返回节点列表。

Length属性定义节点列表中节点的数量

节点关系：parentNode、firstChild、lastChild

DOM根节点：document.decumentElement、document.body

除了innerHTml属性，childNodes和nodeValue属性也可以获取元素内容。

 

## 三、对象

Document、anchar、area、base、button、form、frame、imageevent、table、option

 