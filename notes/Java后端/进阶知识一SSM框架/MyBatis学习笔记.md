前言：学编程和学绘画一样，都是从模仿开始。

初识mybatis、mybatis的核心配置、动态SQL、mybatis的关联映射、与spring的整合。



## 一、初识mybatis

### 概念：

1mybatis是一个支持普通SQL查询、存储过程以及高级映射的持久层框架。它消除了几乎所有JDBC代码和参数的手动设置以及对结果集的检索，只需要手动配置提供POJO、SQL和映射关系，就可以使得Java开发人员使用面向对象的编程思想操作数据库。

Mybatis的使用，只需在应用程序中引入核心包和依赖包即可。

2MyBatis入门程序：查询用户（单条数据的精确查询、多条数据的模糊查询）select、添加用户insert、更新用户update、删除用户delete。

在MySQL中创建数据库db_mybatis.db；在src目录创建log4j.properties文件、核心配置文件mybatis-config.xml。



### 使用：

1调试一个具有增删改查的mybatis入门程序



## 二、mybatis的核心配置

1核心对象：SqlSessionFactory、SqlSession。

SqlSessionFactory是单个数据库映射关系经过编译后的内存镜像，用于创建SqlSession。

SqlSession是应用程序与持久层之间执行交互操作的一个单线程对象，用于执行持久层操作。包含了数据库中所有执行SQL操作的方法，底层封装了JDBC连接，可以使用其实例执行已映射的SQL语句。

2配置文件元素：<configuration>元素是配置文件的根元素。其子元素必须从上到下进行配置。

<properties>：配置属性，用子元素property连接数据库的4个属性

<settings>：设置，开启耳机缓存、延迟加载等

<typeAliases>：定义别名，为了减少全限定类的冗余

<typeHandlers>：类型处理器，将预处理语句中传入的参数从Java类型转换为JDBC类型，或者从数据库取出结果时将JDBC类型转换为Java类型。

<objectFactory>：对象工厂，实例化目标类

<plugins>：插件

<environment>：对数据源配置。<dataSource>、<transactionManage>r

<databaseIdProvider>

<mappers>：指定mybatis映射文件的位置。

3映射文件：<mapper>元素是映射文件的根元素。

<select>：映射查询语句

<insert>：映射插入语句

<update>：更新

<delete>：删除

<sql>：定义可重用的SQL代码片段。

<cache>

<cache-ref>

<resutMap>：结果映射集（用于一对一或一对多关联）



## 三、动态SQL

1MySQL提供对SQL语句动态组装的功能。

<if>：常用的判断语句。用于实现简单的条件选择

<choose>(<when>\<otherwise>)：从多个选项中选择一个执行

<where>\<thrim>：保证当条件不成立时拼接起来的SQL语句在执行中不报错

<set>：更新操作

<foreach>：用于数字和集合循环遍历的方式。

<bind>：使只使用mybatis的语言即可与所需参数连接。



## 四、mybatis的关联映射

1一对一：通过<resultMap>元素中的<association>子元素处理。有嵌套查询和嵌套结果两种配置方式

2一对多：通过<resyltMap>元素中的<collection>子元素处理。

3多对多：使用一个中间表来维护。



## 五、mybatis和spring的整合

1整合环境搭建：导入所需包；编写配置文件；

导入所需包：spring框架（4个核心模块的包、AOP开发使用的包、IDBC和事务的包）、mybatis框架（核心包和依赖包）、mybatis-spring-1.3.1.jar、mysql-cnnector-java-5.1.7-bin.jar、数据源所需包

编写配置文件：db.properties、ApplicationContext.xml、mybatis-config.xml



2传统DAO方式的开发整合：实现持久层、实现DAO层、整合测试。

在实现类中会出现大量重复代码，在方法中也需要指定映射文件中执行语句的ID，并且不能保证编写ID的正确性。



3mapper接口方式的开发整合：基于MapperFactoryBean的整合、基于MapperScannerConfigurer的整合。