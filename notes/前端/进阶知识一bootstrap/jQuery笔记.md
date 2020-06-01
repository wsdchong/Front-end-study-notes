# jQuery笔记

## 前言：

介绍和使用（安装、语法、选择器、事件）、效果（淡入淡出）、操作HTML、遍历、Ajax；

## 一、 介绍和使用

介绍：jQuery是JavaScript库，简化了JavaScript编程。

 

安装：

方法一：下载jQuery库。用script标签引用：<script src=”jquery-1.10.2.min.js”></script>

方法二：用内容分发网络CDN。用script标签引用

https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js或

https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js

在浏览器的console窗口使用$.fn.jquery命令可以查看当前jQuery使用的版本。

 

语法：$(选择符选择HTML元素).action()

例如：$(this).hide();$(“p”).hide();p.test;#test

 

选择器：

基于已经存在的CSS选择器，还可以自定义选择器，以$开头；

 

事件：

鼠标事件：click、dbclick、mouseenter、mouseleave、mousedown、mouseup、hover

键盘事件：keypress、keydown、keyup

表单事件：change

文档/窗口事件：scroll

 

使用：

$(document).ready(function(){

 $("p").click(function()

{ $(this).hide();

 }); });

 

## 二、效果

隐藏/显示：

隐藏：$(“#hide”).click(function(){$(“p”).hide();});

显示：$(“#show”).click(function(){$(“p”).show(speed,function);});

Toggle()

 

淡入淡出：

FadeIn()：淡入已隐藏的元素

fadeout()：淡出可见元素

fadeToggle()：切换

fadeTo()：设定透明度（0-1）

 

滑动

SlideDown()

slideUp()

slideToggle()

 

动画：

Animate()

Stop()

 

Callback的使用

方法链接：$("#p1").css("color","red").slideUp(2000).slideDown(2000);

 

## 三、操作HTML

捕获和设置内容和属性：用于DOM操作的jQuery方法

获取内容：Text、html、val表单

获取属性：attr

 

添加元素：Append、prepend、after、before

 

删除元素：remove、empty

 

操作CSS：addClass、removeClass、toggleClass、css

如：$("p").css({"background-color":"yellow","font-size":"200%"});

 

尺寸：width、height、innerWidth、innerHeight、outerWidth、outerHeight

 

## 四、遍历

根据其相对于其他元素的关系来查找html元素。

 

遍历祖先：向上遍历DOM树

Parent、parents、parentsUntil

 

遍历后代：向上遍历DOM树

Children、find

 

遍历同胞：同层遍历

Siblings、next、nextAll、nextUntil、prev、prevAll、preUntil

 

过滤：基于某一组元素的位置来选择特定的一个元素

First、last、eq、filter、not

 

## 五、AJAX

异步JavaScript和XML是与服务器交换数据的技术、在不重载全部页面的情况下，实现对部分网页的更新。

从服务器加载数据，并把返回的数据放入被选元素中

$(selector).load(URL,data,callback);

通过HTTP get或post请求从服务器请求数据：

$.get(*URL*,*callback*);

$.post(*URL,data,callback*);

 

## 六、其他

在页面同时使用jQuery和其他框架：onConflict

 

Jsonp（json with padding）是json的一种使用模式，可以从其他网站获取资料。

 