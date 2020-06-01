前言：这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

写这篇文章的出发点一个是为了保障自己学以致用，一个是查漏补缺。

而且很多教程虽然说按照那个步骤可以成功，但也可能不成功，要么是自己操作有误，要么是版本变了，还有可能自己基础没学好，前置知识不够。我最开始写Java的时候连创建父类和接口类都不会，直接创建一个类，然后复制粘贴，最后报错。僵硬~

写这类博客，即写步骤，又写操作过程中遇到的问题，然后从中吸取教训，可以让成功的概率更大。

同时mybatis框架学习我打算按照四部分（增删改查、动态SQL、关联映射、与spring整合）进行梳理，最后加个综合大应用。学前在注意的情况下，会写前置知识。

Java基础：https://blog.csdn.net/weixin_42875245/article/details/105951858

IDE使用：https://blog.csdn.net/weixin_42875245/article/details/105867499

Spring学习笔记：https://blog.csdn.net/weixin_42875245/article/details/105631818

Spring见解：https://blog.csdn.net/Haidaiya/article/details/105611801

Spring使用：https://blog.csdn.net/weixin_42875245/article/details/106034031

Mybatis学习笔记：https://blog.csdn.net/weixin_42875245/article/details/105631915

数据库基础：https://blog.csdn.net/weixin_42875245/article/details/105786562

MySQL和Navicat的安装与使用

https://blog.csdn.net/weixin_42875245/article/details/105912850

https://blog.csdn.net/weixin_42875245/article/details/105913078



## 一、引入包

1在eclipse基础开发环境创建一个mybatistest04的动态web项目，将spring与mybatis的驱动包复制到lib目录中，并发布到类路径下。



## 二、创建数据库

1在MySQL中创建数据库。

Create database db_mybatis;

Use db_mybatis;

Create table t_user(id int(32) primary key auto_increment,username varchar(50),jobs varchar(50),phone varchar(16));

Insert into t_user values (1,'one','teacher','1111');

Insert into t_user values (2,'two','doctor','2222');

Insert into t_user values (3,'three','student','3333');



## 三、编写配置文件

1在src目录下创建db.properties；代码如下。

2在src目录下创建applicationContext.xml；代码如下。

3在src目录下创建mybatis-config.xml；代码如下。



## 四、以传统DAO方式的开发整合

1在src目录下创建com.ssm.po包，在包中创建持久化类User和映射文件UserMapper。代码如下

2在src目录下创建com.ssm.dao包，在包中创建接口类UserDao。代码如下。

3在src目录下创建com.ssm.dao.impl包，在包中创建接口实现类UserDaoImpl。代码如下。

4在src目录下创建com.ssm.test包，在包中创建测试类UserDaoTest。

5运行：用Junit运行，findUserById方法查询出用户信息，说明整合成功



四、Mapper接口方式的开发整合

1在spring配置文件中配置下面的属性

  <bean class=*"org.mybatis.spring.mapper.MapperScannerConfigurer"*>

​    <property name=*"basePackage"* value=*"com.ssm.mapper"* />

</bean>

优点：传统的DAO开发方式会产生大量重复代码，在方法中也需要指定映射文件中执行语句的ID，并且不能保证编写时ID的正确性。用Mapper接口的方式，可以自动实现mybatis与spring的整合。



结论：没遇到问题



## 五、操作

不想写了。

没与遇到报错。