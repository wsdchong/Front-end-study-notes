前言：理解了基础，就去用轮子，用熟了轮子就再了解基础，然后造轮子。

Spring基础、spring的bean、spring AOP、spring的数据库开发、spring的事务管理



## 一、spring基础

### 概念：

1spring是以IOC（控制反转）和AOP为内核的框架。

2IOC是spring的基础，是一种控制。实现具有依赖关系对象之间的解耦。

一般情况下，对象B依赖对象A，创建B的时候还需要主动创建A，但引入IOC容器后，创建对象B，IOC容器就会把对象A注入到对象B，不用另外去创建A；

好处有：1可维护性好，代码中每一个class都可以单独测试；2可复用性好，把具有普遍性的常用组件独立出来，反复应用到项目中其他部分；

3spring框架的主要功能是通过其核心容器来实现的。Spring框架提供的两种核心容器分别是BeanFactory和ApplicationContext。两个最基本的包是org.springframework.beans.factory和org.springframework.context；spring IOC框架的主要组件有beans、配置文件、BeanFactory接口及相关类、ApplicationContext接口及相关类；

4IOC/DI实现方式：一种是（setter）设值注入；一种是（constructor）构造注入；



### 使用：

1下载spring框架包（四个）和第三方依赖包（Commons-logging-1.2.jar）；

2用setter方法实现IOC/DI；



## 二、spring的bean

### 概念：

1bean的配置：常采用XML文件来注册并管理bean之间的依赖关系。

2bean的作用域：通过<bean>元素的scope属性来指定。该属性值有singleton、prototype、request、session、globalSession、application、websocket七个值。两种常用的作用域。

3bean的装配方式：XML的装配、基于annotation的装配、自动装配



### 使用：

1两种常用的作用域

2三种bean的装配方式；



## 三、spring AOP

### 概念：

1AOP：面向切面编程，是面向对象编程的补充。采用横向抽取机制，把分散在各个方法中的重复代码提取出来，然后在程序编译时在把提取出的代码应用到需要执行的地方。而传统面向对象编程采用纵向重用。

通过切面可以分别在不同类的方法中加入事务、日志、权限和异常等功能。

好处是：提高开发效率和代码可维护性。

2AspectJ开发：是基于Java语言的AOP框架。实现AOP的两种方式：基于XML的、基于注解的。



### 使用：

1基于XML的声明式AspectJ

2基于注解的声明式AspectJ



## 四、spring的数据库开发

### 概念：

1JDBC是spring数据访问和集成中的重要模块。Spring的JDBC模块负责数据库资源管理和错误处理，大大简化了开发人员对数据库的操作。

针对数据库的操作，spring框架提供了JdbcTemplate类，该类是spring JDBC的核心类。继承自抽象类JdbcAccessor，同时提供JdbcOperations接口。

Spring JDBC模块主要由4个包组成，分别为care、DataSource、object、support。在ApplicationContext.xml中定义三个bean，分别为DataSource、JDBCTemplate和需要注入类的bean。

2spring JDBCTemplate的常用方法：execute、update、query



### 使用：

1spring JDBC的配置

2Spring Jdbc Template类的三种常用方法的作用。



## 五、spring的事务管理

1spring中的事务管理分为两种方式：传统的编程序事务管理（通过编写代码实现）、声明式事务管理（通过AOP技术实现）

最大的优点在于开发者无须通过编程的方式来管理事务，只需要配置文件中的进行相关的事务规则声明，就可以将事务规则应用到业务逻辑中。

Spring的jar包中有个名为spring-tx-4.3.6.RELEASE.jar为spring提供用于事务管理的依赖包。该包有三个接口文件：PlatformTransactionManager（提供平台事务管理器）、TransactionDefinition（事务描述的对象）、TransactionStatus（事务的状态）

2声明式事务管理：通过两种方式实现：基于XML的方式、基于Annotation的方式。



### 使用：

1使用Annotation方式进行声明式事务管理。