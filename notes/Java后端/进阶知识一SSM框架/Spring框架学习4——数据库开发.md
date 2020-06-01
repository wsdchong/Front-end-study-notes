前言：今天终于遇到了第一个报错，记录一下。之前三次都没遇到。

这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

写这篇文章的出发点一个是为了保障自己学以致用，一个是查漏补缺。

而且很多教程虽然说按照那个步骤可以成功，但也可能不成功，要么是自己操作有误，要么是版本变了，还有可能自己基础没学好，前置知识不够。我最开始写Java的时候连创建父类和接口类都不会，直接创建一个类，然后复制粘贴，最后报错。僵硬~

写这类博客，即写步骤，又写操作过程中遇到的问题，然后从中吸取教训，可以让成功的概率更大。

同时sprig框架学习我打算按照五部分（IOC、bean、AOP、数据库、事务）进行梳理，最后加个综合大应用。学前在注意的情况下，会写前置知识。

Java基础：https://blog.csdn.net/weixin_42875245/article/details/105951858

IDE使用：https://blog.csdn.net/weixin_42875245/article/details/105867499

Spring学习笔记：https://blog.csdn.net/weixin_42875245/article/details/105631818

Spring见解：https://blog.csdn.net/Haidaiya/article/details/105611801

数据库基础：https://blog.csdn.net/weixin_42875245/article/details/105786562

MySQL和Navicat的安装与使用

https://blog.csdn.net/weixin_42875245/article/details/105912850

https://blog.csdn.net/weixin_42875245/article/details/105913078



## 一、引入包

1在eclipse基础开发环境创建一个springtest04的动态web项目，将spring的4个基本包以及commons-logging的包，还有spring-jdbc-4.3.6.RELEASE.jar、spring-tx-4.3.6.RELEASE.jar、mysql-connector-java-5.1.7-bin.jar复制到lib目录中，并发布到类路径下。



## 二、创建数据库

在MySQL中创建一个名为db_spring的数据库

Create db_spring；

Use db_spring;

Show tables;



## 二、jdbcTemplate的三种方法——execute

1在src目录下创建配置文件applicationContext.xml，把数据源注入到JDBC中。（需要注意两个地方，一是数据库驱动，MySQL5.0与8.0的驱动不同；二是数据库的URL，我用的是3308端口，3306端口给8.0用），代码如下

2在src目录下创建一个com.ssm.jdbc包，并在包中创建测试类JdbcTemplateTest。在该类的main中通过spring容器获取在配置文件中定义的 JDBCTemplate实例，然后用实例的execute方法执行创建数据表的SQL语句。代码如下

3运行：运行程序，然后查询数据库（show tables；），如果插入了表，说明成功了。



## 三、jdbcTemplate的三种方法——update

1在com.ssm.jdbc包中创建User类，代码如下

2在com.ssm.jdbc包中创建接口UserDao，并定义添加、更新和删除用户的方法，代码如下。

3在com.ssm.jdbc包中创建接口实现类UserDaoImpl。代码如下

4在ApplicationContext.xml定义UserDAO的bean，代码如下

5在测试类中添加测试方法addUserTest，代码如下

6运行：运行Junit（当初不懂这个单元测试，直接用application来运行，僵硬），然后查询数据库的user表（select * from user；），若有数据，说明插入成功。

7在测试类中添加测试方法updateUserTest。

8运行：运行Junit，然后查询user表。若没数据，说明更新成功。

9在测试类中议案家测试方法deleteUserTest。

10运行：运行Junit，然后查询user表。若没数据，说明更新成功。



## 四、jdbcTemplate的三种方法——query

1用MySQL向数据库插入4条数据。

Insert into user(1,’one’,’1111’);

Insert into user(2,’two’,’2222’);

Insert into user(3,’three’,’3333’);

Insert into user(4,’four’,’4444’);

2在接口UserDAO中粗行家一个通过ID查询单个用户和查询所有用户的方法

3在实现类UserDaoImpl，实现接口方法；

4添加测试方法findUserByTest。

5运行：实现单个用户的查询；

6添加测试方法findAllUser。

7运行：实现所有用户的查询。



## 五、实验

1数据库的操作就不赘述了，

https://blog.csdn.net/weixin_42875245/article/details/105912850

2创建applicationContext.xml。代码如下

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"*

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​    *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd"*>

  <!--1配置数据源 -->

  <bean id=*"dataSource"*

​    class=*"org.springframework.jdbc.datasource.DriverManagerDataSource"*>

​    <!--数据库驱动 -->

​    <property name=*"driverClassName"* value=*"com.mysql.jdbc.Driver"* />

​    <!--连接数据库的ur1 -->

​    <property name=*"url"* value=*"jdbc:mysql://localhost:3308/db_spring"* />

​    <!--连接数据库的用户名 -->

​    <property name=*"username"* value=*"root"* />

​    <!--连接数据库的密码 -->

​    <property name=*"password"* value=*"root"* />

  </bean>

  <!--2配置JDBC模板 -->

  <bean id=*"jdbcTemplate"* class=*"org.springframework.jdbc.core.JdbcTemplate"*>

​    <!--默认必须使用数据源 -->

​    <property name=*"dataSource"* ref=*"dataSource"* />

  </bean>

  <!-- 定义id为userDao的Bean -->

  <bean id=*"userDao"* class=*"com.ssm.jdbc.UserDaoImpl"*>

​    <!--将 jdbcTemplate注入到 userDao实例中 -->

​    <property name=*"jdbcTemplate"* ref=*"jdbcTemplate"* />

  </bean>

</beans>

3创建对象User

**package** com.ssm.jdbc;

**public** **class** User {

  **private** Integer id;

  **private** String username;

  **private** String password;

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

  **public** String getPassword() {

​    **return** password;

  }

  **public** **void** setPassword(String password) {

​    **this**.password = password;

  }

  **public** String toString() {

​    **return** "User [id=" + id + ", username=" + username + ", password=" + password + "]";

  }  

}



4创建接口UserDAO

**package** com.ssm.jdbc;

**import** java.util.List;

**public** **interface** UserDao {

  **public** **int** addUser(User user);

  **public** **int** updateUser(User user);

  **public** **int** deleteUser(**int** id);

  //通过id查询用户

  **public** User findUserById(**int** id);

  //查询所有用户

  **public** List<User> findAllUser();

}



5创建接口实现类UserDaoImpl

package com.ssm.jdbc;

import java.util.List;



import org.springframework.jdbc.core.BeanPropertyRowMapper;

import org.springframework.jdbc.core.JdbcTemplate;

import org.springframework.jdbc.core.RowMapper;

public class UserDaoImpl implements UserDao {

​    private JdbcTemplate jdbcTemplate; 

​    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {

​       this.jdbcTemplate = jdbcTemplate;

​    }

​    public int addUser(User user) {

​       String sql="insert into user(username,password) value(?,?)";

​       Object[] obj=new Object[]{

​              user.getUsername(),

​              user.getPassword()

​       };

​       int num=this.jdbcTemplate.update(sql,obj);

​       return num;

​    }

​    public int updateUser(User user) {

​       String sql="update user set username=?,password=? where id=?";

​       Object[] params=new Object[]{

​              user.getUsername(),

​              user.getPassword(),

​              user.getId()

​       };

​       int num=this.jdbcTemplate.update(sql,params);

​       return num;

​    }

​    public int deleteUser(int id) {

​       String sql="delete from user where id=?";    

​       int num=this.jdbcTemplate.update(sql,id);

​       return num;

​    }

​    //通过id查询用户数据信息

​    public User findUserById(int id) {

​       String sql="select * from user where id=?";

​       RowMapper<User> rowMapper=new BeanPropertyRowMapper<User>(User.class);

​       return this.jdbcTemplate.queryForObject(sql,rowMapper,id);

​    }

​    //查询所有用户数据信息

​    public List<User> findAllUser() {

​       String sql="select * from user";

​       RowMapper<User> rowMapper=new BeanPropertyRowMapper<User>(User.class);

​       return this.jdbcTemplate.query(sql,rowMapper);

​    }

}

6创建测试类jdbcTemplateTest

package com.ssm.jdbc;

import java.util.List;



import org.junit.Test;

import org.springframework.context.ApplicationContext;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import org.springframework.jdbc.core.JdbcTemplate;

/**

 *使用excute()方法创建表

 */

public class JdbcTemplateTest {

​    public static void main(String[] args) {

​       //加载配置文件

​       ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");

​       //获取JdbcTemplate实例

​       JdbcTemplate jdbcTemplate = (JdbcTemplate) applicationContext.getBean("jdbcTemplate");

​       //使用execute()方法执行SQL语句，创建用户表user

​       jdbcTemplate.execute("create table user(" +

​                 "id int primary key auto_increment," +

​                    "username varchar(40)," +

​                 "password varchar(40))");

​    }

​    @Test

​    public void addUserTest(){

​       ApplicationContext applicationContext=new ClassPathXmlApplicationContext("applicationContext.xml");

​       UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​       User user = new User();

​       user.setUsername("wsdchong");

​       user.setPassword("123456");

​       int num=userDao.addUser(user);

​       if(num>0){

​           System.out.println("成功插入了"+num+"条数据。");

​       }else{

​           System.out.println("插入操作执行失败。");

​       }      

​    }

​    @Test

​    public void updateUserTest(){

​       ApplicationContext applicationContext=new ClassPathXmlApplicationContext("applicationContext.xml");

​       UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​       User user = new User();

​       user.setId(1);

​       user.setUsername("csdn");

​       user.setPassword("666666");

​       int num=userDao.updateUser(user);

​       if(num>0){

​           System.out.println("成功更新了"+num+"条数据。");

​       }else{

​           System.out.println("更新操作执行失败。");

​       }      

​    }

​    @Test

​    public void deleteUserTest(){

​       ApplicationContext applicationContext=new ClassPathXmlApplicationContext("applicationContext.xml");

​       UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​       int num=userDao.deleteUser(1);

​       if(num>0){

​           System.out.println("成功删除了"+num+"条数据。");

​       }else{

​           System.out.println("删除操作执行失败。");

​       }      

​    }   

​    @Test

​    public void findUserByldTest(){

​       ApplicationContext applicationContext=new ClassPathXmlApplicationContext("applicationContext.xml");

​       UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​       User user=userDao.findUserById(2); 

​       System.out.println(user);  

​    }   

​    @Test

​    public void findAllUserTest(){

​       ApplicationContext applicationContext=new ClassPathXmlApplicationContext("applicationContext.xml");

​       UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​       List<User> list=userDao.findAllUser();

​       for(User user:list){

​           System.out.println(user);  

​       }

​    }   

}



## 六、报错

已经做了三个spring的项目了，一直没遇到报错，今天终于遇到了。

1运行Junit出现问题，应该是没引入Junit4的包。

解决方法：在项目上右键build path-add library中选择Junit



结论：终于遇到了一个之前没遇到过的问题。