这篇文章主要讲技巧和部分问题的处理。

前言：果然实践出真知，单看eclipse的使用介绍学不到什么，但是遇到bug然后去解决就能很快地学到这个工具的使用。

Eclipse教程：eclipse帮助文档、菜鸟教程、w3c、博客；

eclipse帮助文档：在eclipse中选择help-help contents，官网上也有；缺点是全英文；

https://help.eclipse.org/2020-03/index.jsp

菜鸟教程：界面舒服，不过有些内容不显示图片；

https://www.runoob.com/eclipse/eclipse-debug-configuration.html

w3c：菜鸟和W3C内容基本一致；

https://www.w3cschool.cn/eclipse/

下面我从三个方面讲eclipse的使用：教程的基本内容、处理bug的方法、目前已有的收获（安装、引入项目配置环境、运行、与数据库相关、与网站开发相关）



## 一、教程的基本内容

安装、修改字符集、窗口介绍、菜单、视图、工作空间、运行配置、调试、首选项、插件、快捷键等等；

具体内容请上上面的链接中学。还是挺有帮助的。英语好的之间看帮助文档。



## 二、处理bug的方法

光看上面的教程，出现问题也不会往上面想，还有许多问题在上面也找不着，许多问题甚至跟不上新版本；所以找bug和处理问题的方法很重要。

我目前遇到bug解决bug的方法是；1复制问题；2在百度翻译翻译看什么内容；3然后把关键部分复制到百度去查询；

复制问题（三个地方）：

1是在工作台的markers，在引入项目时，常出现JDK不同等问题的报错；

2是在工作台的console上，在运行项目后，常出现服务器和数据库的报错；

3是双击markers上的问题，然后在代码中悬浮在错误提示和处理方法；常出现库的 引入有误；

复制到百度翻译：英语好的就只需要打开一个TXT文本，在其中编辑问题。

https://fanyi.baidu.com/translate?aldtype=16047&query=&keyfrom=baidu&smartresult=dict&lang=auto2zh#auto/zh/

英语学得再好，有些单词就是不认识，没必要为学一个软件还得把英语从头学好，那样学习成本太高了，入门门槛高。英语的学习可以在后期用软件的过程中去熟能生巧。

并且在markers中的问题不能选择其中一部分去复制，都是整体复制，中间有许多不必要的内容，如文件目录，段落描述等。把这些复制到百度翻译中，然后在百度翻译中再编辑问题，进行第二次复制；

百度上搜索（两个技巧）：（英语好的可以在谷歌上搜索）

第一个是百度有字数限制，需要在百度翻译中编辑文件再百度；

第二个是百度有些问题是很久之前的问题，可能在新版本中不适应，需要在百度的搜索工具中选择最近一年和最近一个月；

一般来说，国内主要是CSDN、博客园、简书等上会有一些处理方法；



## 三、目前已有的收获

1不知道怎么安装

解决方法：下载安装包、点击安装即可。现在好像也用不着配置path了；

教程1：具体教程菜鸟教程中有。

教程2：https://blog.csdn.net/pengxiang1998/article/details/105854656

1jdk安装：https://www.oracle.com/java/technologies/javase-downloads.html

可以安装jdk14、jdk8u（即jdk1.8和jdk8）。

Jdk7的安装https://www.oracle.com/java/technologies/javase/javase7-archive-downloads.html

2eclipse安装：https://www.eclipse.org/downloads/

3tomcat安装：http://tomcat.apache.org/download-70.cgi



2引入项目，markers上出现红×的提示，不解决，连运行都成问题；

解决方法：JDK版本不同的换JDK；Tomcat版本不同的换Tomcat；缺包的引入包；

具体教程：用之前说的方法搜。

jdk切换：在project的properties中选Java build path中修改。

Tomcat切换：在window的preferences中选server-runtime environment中修改。

缺包：build path中apply。



3没有红色警告，但是运行有问题。

目前我知道的运行有两种：一是Junit4运行；二是Tomcat运行。

测试类的运行是@test，用Junit4来进行单元测试；

教程：https://blog.csdn.net/u011054333/article/details/54565664

二是Tomcat运行是server；

教程：自己百度；



4MySQL的连接出错

1安装的版本不同，自己安装的是MySQL8.0，引入的项目时MySQL5.0；

解决方法：按上面的方法搜。

教程：https://blog.csdn.net/liangllhahaha/article/details/89508826

这个教程讲了MySQL的下载和安装、Navicat的安装、Navicat连接MySQL；



5没有报错，但是出现404报错，并且控制台的语句也没显示；

原因：JSP与web-inf平级，在web-inf中会被屏蔽；

解决方法：移到其中；

教程：https://blog.csdn.net/weixin_42223850/article/details/104543803