两个部分：一是理论、二是实践；

这里的Java讲解来源于2010年之前，之后的改变看官网。

Java的基本使用：https://blog.csdn.net/weixin_42875245/article/details/105939720

Java应用基础：https://blog.csdn.net/weixin_42875245/article/details/105939796

Java面向对象基础：https://blog.csdn.net/weixin_42875245/article/details/105939837

Java图形用户界面应用知识：https://blog.csdn.net/weixin_42875245/article/details/105939950

Java的多线程知识：https://blog.csdn.net/weixin_42875245/article/details/105950391



## 一、异常

1异常类的继承

object-throwable-error-awterror\threadDeath

object-throwable-exception-runtimeException/sqlException

2异常

Java把程序运行中可能遇到的错误分为两类，一类是非致命的，通过某种修正后程序还能继续执行。这类错误被称为异常。另一类是致命的，不能简单地恢复执行，类就是错误。

异常类基类throwable派生出两个子类：error类（定义Java程序运行时出现了灾难性失败的异常）、exception类（定义程序可以捕捉的异常。

异常还分为：系统定义的、用户定义的

3异常处理：

对于异常，Java使用一种错误捕获方法进行处理。

处理异常的两种方式，一种是将异常交给异常处理机制的预设处理方法来处理；一种是利用Java提供的try-catch-finally语句对于可能出现的异常作预先处理



## 二、常见的异常情况

Exception类定义可捕捉的异常，exception类派生了两个子类：runtimeException和IOException。

1RuntimeException类的一般是编程原因

如错误的类型转向、数组越界访问、空指针访问

2IOException类的一般是一些意外情况的出现

如试图读文件结尾后的数据、打开一个错误的URL

3算数异常



## 三、异常处理机制

异常处理关键字try-catch-finally

当出现异常时，要进行异常处理。Java语句提供了异常处理机制，用于专门处理异常。一般地，当发生异常时，程序中断执行，并输出一条信息。Java对可能抛出异常的代码段，要使用try语句括住，用catch语句指明要捕捉的异常以及相应的处理代码。



## 四、利用throw、throws创建自定义异常







总结：梳理一下异常处理