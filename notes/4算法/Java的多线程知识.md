两个部分：一是理论、二是实践；

这里的Java讲解来源于2010年之前，之后的改变看官网。

Java的基本使用：https://blog.csdn.net/weixin_42875245/article/details/105939720

Java应用基础：https://blog.csdn.net/weixin_42875245/article/details/105939796

Java面向对象基础：https://blog.csdn.net/weixin_42875245/article/details/105939837

Java图形用户界面应用知识：https://blog.csdn.net/weixin_42875245/article/details/105939950



## 一、进程与线程

1进程：

程序的一次执行过程，是系统进行调度和资源分配的一个独立单位

线程是比进程更小的执行单位。一个进程在执行过程中，可以产生多个线程。线程不能独立存在，必须存在于进程中。

线程是轻量级的进程，系统负担小，主要是CPU的分配。

2多线程

指同时存在几个执行体，按几条不同的执行线索共同工作的情况。多线程实现单个进程中的并发计算。各线程之间共享进程空间的数据。

多线程的程序能够更好地表述和解决现实时间的具体问题，是计算机应用开发和程序设计的一个必然发展的趋势。

3Java与多线程

Java语句的一个重要功能特点就是内置对多线程的支持，它使得编程人员开发具有多线程功能，能同时处理多个任务的功能强大的应用程序。

Java的所有类都是在多线程的思想下定义的，Java利用线程使得整个系统成为异步。

每个Java程序都有一个隐含的主线程。Application中有main方法；applet中，主线程指挥浏览器加载并执行Java小程序。

4使用线程的好处

是UI响应更快，执行异步或后台处理，



## 二、线程的概念模型

线程的三个组成部分：线程代码、被操作数据、线程控制（虚拟CPU）

1Thread类

Thread类综合了Java程序中一个线程需要拥有的属性和方法。生成一个Thread类的对象后，一个新的线程就诞生了。

**public class ThreadTest {**

  **public static void main(String[] args){**

   **Job1 j = new Job1();**

   **Thread t1 = new Thread(j) ;**

   **t1.start() ;**

  **}   }**

**class Job1 implements Runnable {**

  **int i ;**

  **public void run() {**

   **while (i<50) { System.out.println(i++) ; }**

 **}** 

每个线程都是通过目标对象的方法run来完成其操作的。方法run被称为线程体；

提供线程体的目标对象是在初始化一个线程时指明的；

任何实现了runnable接口（实现run方法）的类的对象都可以作为线程的目标对象。

线程代码（由实现runnable接口的类提供的run方法）

被操作数据（实现runnable接口的类的实例）

线程控制（Thread的实例）

2Thread类构造函数



## 三、线程的同步与互斥

具体看操作系统的处理机调度与死锁

https://blog.csdn.net/weixin_42875245/article/details/105722990



## 四、线程

具体看操作系统的进程调度，如上一个链接



## 五、编程

https://blog.csdn.net/weixin_42875245/article/details/105939330



看到extend Frame，然后还superclass了一下Frame。

运行后报错。

后来没superclass后，直接写程序，有成功了。





总结：梳理一下线程与多线程，最后写一个用到多线程的计时器。

下一阶段，梳理一下异常处理，简单顺一下，不写代码。