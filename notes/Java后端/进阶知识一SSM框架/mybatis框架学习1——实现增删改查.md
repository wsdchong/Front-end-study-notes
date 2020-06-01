前言：这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

写这篇文章的出发点一个是为了保障自己学以致用，一个是查漏补缺。

而且很多教程虽然说按照那个步骤可以成功，但也可能不成功，要么是自己操作有误，要么是版本变了，还有可能自己基础没学好，前置知识不够。我最开始写Java的时候连创建父类和接口类都不会，直接创建一个类，然后复制粘贴，最后报错。僵硬~

写这类博客，即写步骤，又写操作过程中遇到的问题，然后从中吸取教训，可以让成功的概率更大。

同时sprig框架学习我打算按照五部分（IOC、bean、AOP、数据库、事务）进行梳理，最后加个综合大应用。学前在注意的情况下，会写前置知识。

Java基础：https://blog.csdn.net/weixin_42875245/article/details/105951858

IDE使用：https://blog.csdn.net/weixin_42875245/article/details/105867499

Spring学习笔记：https://blog.csdn.net/weixin_42875245/article/details/105631818

Spring见解：https://blog.csdn.net/Haidaiya/article/details/105611801

Spring使用：https://blog.csdn.net/weixin_42875245/article/details/106034031

数据库基础：https://blog.csdn.net/weixin_42875245/article/details/105786562

MySQL和Navicat的安装与使用

https://blog.csdn.net/weixin_42875245/article/details/105912850

https://blog.csdn.net/weixin_42875245/article/details/105913078



## 一、引入包

1在eclipse基础开发环境创建一个mybatistest01的动态web项目，将mybatis的核心包、依赖包以及MySQL的驱动包复制到lib目录中，并发布到类路径下。



## 二、创建数据库

1在MySQL中修改我在第四个笔记中的数据库

Create database db_mybatis;

User db_mybatis;

Create table t_user(id int(32) primary key auto_increment,username varchar(50),jobs varchar(50),phone varchar(16));

Insert into t_user values (1,’one’,’teacher’,’1111’);

Insert into t_user values (2,’two’,’doctor’,’2222’);

Insert into t_user values (3,’three’,’student’,’3333’);



## 三、mybatis的四种操作——查找

1在src目录下创建log4j.properties文件；代码如下。

2在src目录下创建com.ssm.po包，在包中创建持久化类User。代码如下

3在src目录下创建com.ssm.mapper包，在包中创建映射文件UserMapper.xml。代码如下。

4在src目录下创建配置文件mybatis-config.xml。代码如下

5在src目录下创建com.ssm.test包，在包中创建测试类MybatisTest。

6运行：用Junit运行，可以实现单个查找和模糊查找



## 四、mybatis的四种操作——添加

1在映射文件中添加insert元素。

2在MybatisTest中添加测试方法；



## 五、mybatis的四种操作——更新

1在映射文件中添加update元素。

2在MybatisTest中添加测试方法；



## 六、mybatis的四种操作——删除

1在映射文件中添加insert元素。

2在MybatisTest中添加测试方法；



## 七、实验

1数据库的操作就不赘述了，

https://blog.csdn.net/weixin_42875245/article/details/105912850

2创建log4j.properties

\# Global logging configuration

log4j.rootLogger=ERROR, stdout

\# MyBatis logging configuration...

log4j.logger.com.ssm=DEBUG

Console output...

log4j.appender.stdout=org.apache.log4j.ConsoleAppender

log4j.appender.stdout.layout=org.apache.log4j.PatternLayout

log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n

3创建持久层对象User

**package** com.ssm.po;

**public** **class** User {

  **private** Integer id;

  **private** String username;

  **private** String jobs;

  **private** String phone;

  **public** Integer getId() {

​    **return** id;

  }

  **public** **void** setId(Integer id) {

​    **this**.id = id;

  }

  **public** String getUsername() {

​    **return** username;

  }

  **public** **void** setUsername(String username) {

​    **this**.username = username;

  }

  **public** String getJobs() {

​    **return** jobs;

  }

  **public** **void** setJobs(String jobs) {

​    **this**.jobs = jobs;

  }

  **public** String getPhone() {

​    **return** phone;

  }

  **public** **void** setPhone(String phone) {

​    **this**.phone = phone;

  }

  **public** String toString() {

​    **return** "User [id=" + id + ", username=" + username + ", jobs=" + jobs + ", phone=" + phone + "]";

  }

}

4创建映射文件UserMapper.xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"

  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace=*"com.ssm.mapper.UserMapper"*>

  <!--根据用户编号获取用户信息 -->

  <select id=*"findUserById"* parameterType=*"Integer"* resultType=*"com.ssm.po.User"*>

​    select * from t_user where id=#{id}

  </select>

  <!--根据用户名模糊查询用户信息 -->

  <select id=*"findUserByName"* parameterType=*"String"* resultType=*"com.ssm.po.User"*>

​    select * from t_user where username like '%${value}%'

  </select>

  <!--添加客户信息 -->

  <insert id=*"addUser"* parameterType=*"com.ssm.po.User"*>

​    insert into t_user(username,jobs,phone) values(#{username},#{jobs},#{phone})

  </insert>

  <!--更新用户信息 -->

  <update id=*"updateUser"* parameterType=*"com.ssm.po.User"*>

​    update t_user set username=#{username},jobs=#{jobs},phone=#{phone} where id=#{id}

  </update>

  <!--删除用户信息-->

  <delete id=*"deleteUser"* parameterType=*"Integer"*>

​    delete from t_user where id=#{id}

  </delete>   

</mapper>

5创建配置文件mybatis-config.xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"

  "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>

  <settings>

​    <setting name=*"logImpl"* value=*"LOG4J"*/>

  </settings>

  <environments default=*"mysql"*>

​    <environment id=*"mysql"*>

​      <transactionManager type=*"JDBC"* />

​      <dataSource type=*"POOLED"*>

​        <property name=*"driver"* value=*"com.mysql.jdbc.Driver"* />

​        <property name=*"url"* value=*"jdbc:mysql://localhost:3308/db_mybatis"* />

​        <property name=*"username"* value=*"root"* />

​        <property name=*"password"* value=*"root"* />

​      </dataSource>

​    </environment>

  </environments>

  <mappers>

​    <mapper resource=*"com/ssm/mapper/UserMapper.xml"* />

  </mappers>

</configuration>

6创建测试类

**package** com.ssm.test;

**import** java.io.InputStream;

**import** java.util.List;



**import** org.apache.ibatis.io.Resources;

**import** org.apache.ibatis.session.SqlSession;

**import** org.apache.ibatis.session.SqlSessionFactory;

**import** org.apache.ibatis.session.SqlSessionFactoryBuilder;

**import** org.junit.Test;



**import** com.ssm.po.User;

**public** **class** MybatisTest {

  @Test

  **public** **void** findUserByIdTest() **throws** Exception {

​    String resource = "mybatis-config.xml";

​    InputStream inputStream = Resources.*getResourceAsStream*(resource);

​    SqlSessionFactory sqlSessionFactory = **new** SqlSessionFactoryBuilder().build(inputStream);

​    SqlSession sqlSession = sqlSessionFactory.openSession();

​    User user = sqlSession.selectOne("com.ssm.mapper.UserMapper.findUserById", 1);

​    System.***out\***.println(user.toString());

​    sqlSession.close();

  }

  @Test

  **public** **void** findUserByNameTest() **throws** Exception {

​    String resource = "mybatis-config.xml";

​    InputStream inputStream = Resources.*getResourceAsStream*(resource);

​    SqlSessionFactory sqlSessionFactory = **new** SqlSessionFactoryBuilder().build(inputStream);

​    SqlSession sqlSession = sqlSessionFactory.openSession();

​    List<User> users = sqlSession.selectList("com.ssm.mapper.UserMapper.findUserByName", "g");

​    **for** (User user : users) {

​      System.***out\***.println(user.toString());

​    }

​    sqlSession.close();

  }

  @Test

  **public** **void** addUserTest() **throws** Exception {

​    String resource = "mybatis-config.xml";

​    InputStream inputStream = Resources.*getResourceAsStream*(resource);

​    SqlSessionFactory sqlSessionFactory = **new** SqlSessionFactoryBuilder().build(inputStream);

​    SqlSession sqlSession = sqlSessionFactory.openSession();

​    User user = **new** User();

​    user.setUsername("wsdchong");

​    user.setJobs("worker");

​    user.setPhone("12344321");

​    **int** rows = sqlSession.insert("com.ssm.mapper.UserMapper.addUser", user);

​    **if** (rows > 0) {

​      System.***out\***.println("成功添加" + rows + "条数据！");

​    } **else** {

​      System.***out\***.println("添加数据失败!");

​    }

​    sqlSession.commit();

​    sqlSession.close();

  }

  @Test

  **public** **void** updateUserTest() **throws** Exception {

​    String resource = "mybatis-config.xml";

​    InputStream inputStream = Resources.*getResourceAsStream*(resource);

​    SqlSessionFactory sqlSessionFactory = **new** SqlSessionFactoryBuilder().build(inputStream);

​    SqlSession sqlSession = sqlSessionFactory.openSession();

​    User user = **new** User();

​    user.setId(4);

​    user.setUsername("csdn");

​    user.setJobs("teacher");

​    user.setPhone("5432112345");

​    **int** rows = sqlSession.update("com.ssm.mapper.UserMapper.addUser", user);

​    **if** (rows > 0) {

​      System.***out\***.println("成功修改了" + rows + "条数据！");

​    } **else** {

​      System.***out\***.println("修改数据失败!");

​    }

​    sqlSession.commit();

​    sqlSession.close();

  }

  @Test

  **public** **void** deleteUserTest() **throws** Exception {

​    String resource = "mybatis-config.xml";

​    InputStream inputStream = Resources.*getResourceAsStream*(resource);

​    SqlSessionFactory sqlSessionFactory = **new** SqlSessionFactoryBuilder().build(inputStream);

​    SqlSession sqlSession = sqlSessionFactory.openSession();

​    **int** rows = sqlSession.delete("com.ssm.mapper.UserMapper.deleteUser", 4);

​    **if** (rows > 0) {

​      System.***out\***.println("成功删除了" + rows + "条数据！");

​    } **else** {

​      System.***out\***.println("删除数据失败!");

​    }

​    sqlSession.commit();

​    sqlSession.close();

  }

}



结论：没遇到问题