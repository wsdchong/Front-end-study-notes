两个部分：一是理论、二是实践；

这里的Java讲解来源于2010年之前，之后的改变看官网。

## 一、Java的基本概念

1Java发展历史

由sun（Stanford university network）开发，1982年2月成立，2009年4月被Oracle收购；

Java不仅仅是一种编程语言，更是一种功能强大的开发和运行环境

JDK（Java development kit）包括运行环境、编译工具和类库等；

JRE（Java runtime environment）包含JVM以及Java核心类库，是运行Java程序所需的环境的集合；

JVM（Java virtual machine）是Java虚拟机，一个虚拟出来的计算机。让Java程序可以在多种平台上不加修改地运行

2Java语言特点

面向对象：完全基于类和对象，以类的形式组织代码；

简单：类似C++，摒弃C++中容易引发程序错误的一些特性，提供了丰富的类库、自动垃圾回收；

健壮：自动内存管理，垃圾收集，例外控制机制

安全：applet安全控制机制、安全策略管理器；

多线程：支持多任务

3工作原理

Java半编译半解释，字节码运行在虚拟机上；

首先从源文件program.java通过编译器编译成字节码文件program.class；然后通过解释器解释为二进制程序；

Java平台有两个重要的组件：一个是JVM，一个是Java API；

JVM是Java平台的基础；

Java API是预先建立的软件组件的集合，提供丰富的功能，如GUI组件。JavaAPI被分为相关类和接口的库，这些库被称为包。

4运行系统

Java的运行系统是各平台厂商对JVM的具体实现。对Java中两类程序：Java application和Java applet，存在两种不同类型的运行系统；对于Java application，运行环境是Java解释器；对于Java applet，运行环境是Java兼容的web浏览器；



## 二、Java的使用

1开发工具

JDK（官网下载）、IDE（eclipse或者IDEA）

2下载

jdk安装：https://www.oracle.com/java/technologies/javase-downloads.html

可以安装jdk14、jdk8u（即jdk1.8和jdk8）。

Jdk7的安装https://www.oracle.com/java/technologies/javase/javase7-archive-downloads.html

eclipse安装：https://www.eclipse.org/downloads/

IDEA下载：https://www.jetbrains.com/idea/

tomcat安装：http://tomcat.apache.org/download-70.cgi

3安装JDK后产生的目录

Bin目录：Java开发工具，如Java编译器，解释器；

Lib目录：Java开发类库

JRE目录：Java运行环境，如Java虚拟机，运行类库

4JDK实用程序

Javac：Java编译器，将Java源程序编译成字节码；

Java：Java解释器，直接从类文件（字节码）执行Java应用程序（application）。启动命令行程序或阻塞程序；

Javaw：启动窗口程序或非阻塞程序；

Appletviewer：小程序浏览器，执行HTML文件上的Java小程序（applet）



## 三、第一个Java程序

1创建一个Java program：

file-new-java program；或者file-new-other-Java-Java project；

第一次使用的时候，我直接创建了一个program，里面没包括JRE。然后创建类的时候一直报错；

2在src中创建class：

new-class；

第一次没用class，以为是字节码，编写的文件是.class的；然后又想class还表示类的意思，于是创建了一下，发现就是源文件（.java后缀）。

3编写代码和运行

System.out.println("Hello World"); // 打印 Hello World

然后也没弹出命令窗口，也没显示日志。

于是我想是不是没引入IO库；于是**import** java.util.*; 结果没用

于是我点击window-show view-console，看控制台显示不；结果没用；

百思不得其解，百度一下；https://jingyan.baidu.com/article/95c9d20d0da0e1ec4f75614a.html。发现我也按照这个步骤来的。为什么控制台不显示语句。

网上还有一种教程，就是把eclipse的show关闭再打开，不过没用

https://blog.csdn.net/qq_38046655/article/details/81040781

但是我file-restart后，居然可以了。后来回想一下，应该是没保存的原因。



总结：梳理了一下Java的基本概念、安装、以及运行一下程序。

中间遇到了奇奇怪怪的问题，现在回想应该是我以前做的项目中有一些配置，然后在新的项目中可能配置有冲突。还有就是我以为保存了，但是没保存就运行，自然也显示；

下一阶段，梳理一下Java的语言基础（数据类型、表达式、流程控制语句），然后运行一下排序算法。