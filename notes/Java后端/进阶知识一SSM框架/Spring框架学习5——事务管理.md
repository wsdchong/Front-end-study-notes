前言：这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

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

1在eclipse基础开发环境创建一个springtest04的动态web项目，将spring的4个基本包和commons-logging的包，还有spring-jdbc-4.3.6.RELEASE.jar、spring-tx-4.3.6.RELEASE.jar、mysql-connector-java-5.1.7-bin.jar，以及实现AOP的四个包复制到lib目录中，并发布到类路径下。



## 二、创建数据库

1在MySQL中修改我在第四个笔记中的数据库

Alter table user add jf int(11) null;

补充一个删除字段的语句；

Alter table user drop ‘jf’;

还有一个查看表结构的语句（desc user）;

2插入四条语句，默认积分为1000；



## 三、基于XML的声明式事务

1在src目录下创建配置文件applicationContext.xml，把数据源注入到JDBC中。（需要注意两个地方，一是数据库驱动，MySQL5.0与8.0的驱动不同；二是数据库的URL，我用的是3308端口，3306端口给8.0用），代码如下

2在com.ssm.jdbc包中创建User类，代码如下

3在com.ssm.jdbc包中创建接口UserDao代码如下。

4在com.ssm.jdbc包中创建接口实现类UserDaoImpl。代码如下

5在src目录下创建ApplicationContext.xml，添加命名空间并编写事务管理，代码如下

6在com.ssm.jdbc包中创建TransactionManager的事务管理器，代码如下。

7运行：在Junit控制台可以看见by zero的算数异常信息。说明spring的事务管理配置生效了。



## 四、基于annotation的声明式事务

1在src目录下创建spring配置文件applicationContext-annotation.xml。在该文件中声明事务管理器等配置信息。

2在UserDaoImpl类中正价事务注解

4添加测试方法annotationTest。

5运行：和XML一样的 效果

用注解的 好处是，节省了在配置文件中的书写，提高配置文件的可读性。



## 五、实验

1数据库的操作就不赘述了，

https://blog.csdn.net/weixin_42875245/article/details/105912850

2创建applicationContext.xml。代码如下

```
<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"*

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xmlns:aop=*"http://www.springframework.org/schema/aop"*

  xmlns:tx=*"http://www.springframework.org/schema/tx"*

  xmlns:context=*"http://www.springframework.org/schema/context"*

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​    *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd*

​    *http://www.springframework.org/schema/tx*

​    *http://www.springframework.org/schema/tx/spring-tx-4.3.xsd*

​    *http://www.springframework.org/schema/context*

​    *http://www.springframework.org/schema/context/spring-context-4.3.xsd*

​    *http://www.springframework.org/schema/aop*

​    *http://www.springframework.org/schema/aop/spring-aop-4.3.xsd"*>

  <!--1.配置数据源 -->

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

  <!--2.配置JDBC模板 -->

  <bean id=*"jdbcTemplate"* class=*"org.springframework.jdbc.core.JdbcTemplate"*>

​    <!--默认必须使用数据源 -->

​    <property name=*"dataSource"* ref=*"dataSource"* />

  </bean>

  <!--3.定义id为userDao的Bean -->

  <bean id=*"userDao"* class=*"com.ssm.jdbc.UserDaoImpl"*>

​    <!--将 jdbcTemplate注入到 userDao实例中 -->

​    <property name=*"jdbcTemplate"* ref=*"jdbcTemplate"* />

  </bean>

  <!--4.事务管理器，依赖于数据源 -->

  <bean id=*"transactionManager"* class=*"org.springframework.jdbc.datasource.DataSourceTransactionManager"*>

​    <property name=*"dataSource"* ref=*"dataSource"*/>

  </bean>

  <!--5.编写通知：对事务进行增强（通知），需要编写对切入点和具体执行事务细节 -->

  <tx:advice id=*"txAdvice"* transaction-manager=*"transactionManager"*>

​    <tx:attributes>

​      <tx:method name=*"\*"* propagation=*"REQUIRED"* isolation=*"DEFAULT"* read-only=*"false"*/>

​    </tx:attributes>

  </tx:advice>

  <!--6.编写aop,让spring自动对目标生成代理，需要使用AspectJ的表达式 -->

  <aop:config>

​    <!--切入点 -->

​    <aop:pointcut expression=*"execution(\* com.ssm.jdbc.\*.*(..))"* id=*"txPointCut"* />

​    <!--切面 -->

​    <aop:advisor advice-ref=*"txAdvice"* pointcut-ref=*"txPointCut"*/>

  </aop:config>   

</beans>
```

3创建对象User

```
package** com.ssm.jdbc;

**public** **class** User {

  **private** Integer id;

  **private** String username;

  **private** String password;

  **private** Integer jf;

  **public** Integer getJf() {

​    **return** jf;

  }

  **public** **void** setJf(Integer jf) {

​    **this**.jf = jf;

  }

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

​    **return** "User [id=" + id + ", username=" + username + ", password=" + password + ", jf=" + jf + "]";

  }

}
```



4创建接口UserDAO

```
package** com.ssm.jdbc;

**import** java.util.List;

**public** **interface** UserDao {

  **public** **int** addUser(User user);

  **public** **int** updateUser(User user);

  **public** **int** deleteUser(**int** id);

  //通过id查询用户

  **public** User findUserById(**int** id);

  //查询所有用户

  **public** List<User> findAllUser();

  //赠送积分

  **public** **void** transfer(String outUser, String inUser, Integer jf);

}
```



5创建接口实现类UserDaoImpl

```
package** com.ssm.jdbc;

**import** java.util.List;



**import** org.springframework.jdbc.core.BeanPropertyRowMapper;

**import** org.springframework.jdbc.core.JdbcTemplate;

**import** org.springframework.jdbc.core.RowMapper;

**import** org.springframework.transaction.annotation.Isolation;

**import** org.springframework.transaction.annotation.Propagation;

**import** org.springframework.transaction.annotation.Transactional;

**public** **class** UserDaoImpl **implements** UserDao {

  **private** JdbcTemplate jdbcTemplate; 

  **public** **void** setJdbcTemplate(JdbcTemplate jdbcTemplate) {

​    **this**.jdbcTemplate = jdbcTemplate;

  }

  **public** **int** addUser(User user) {

​    String sql="insert into user(username,password) value(?,?)";

​    Object[] obj=**new** Object[]{

​        user.getUsername(),

​        user.getPassword()

​    };

​    **int** num=**this**.jdbcTemplate.update(sql,obj);

​    **return** num;

  }

  **public** **int** updateUser(User user) {

​    String sql="update user set username=?,password=? where id=?";

​    Object[] params=**new** Object[]{

​        user.getUsername(),

​        user.getPassword(),

​        user.getId()

​    };

​    **int** num=**this**.jdbcTemplate.update(sql,params);

​    **return** num;

  }

  **public** **int** deleteUser(**int** id) {

​    String sql="delete from user where id=?";   

​    **int** num=**this**.jdbcTemplate.update(sql,id);

​    **return** num;

  }

  //通过id查询用户数据信息

  **public** User findUserById(**int** id) {

​    String sql="select * from user where id=?";

​    RowMapper<User> rowMapper=**new** BeanPropertyRowMapper<User>(User.**class**);

​    **return** **this**.jdbcTemplate.queryForObject(sql,rowMapper,id);

  }

  //查询所有用户数据信息

  **public** List<User> findAllUser() {

​    String sql="select * from user";

​    RowMapper<User> rowMapper=**new** BeanPropertyRowMapper<User>(User.**class**);

​    **return** **this**.jdbcTemplate.query(sql,rowMapper);

  }

  //赠送积分

@Transactional(propagation=Propagation.***REQUIRED\***,isolation=Isolation.***DEFAULT\***,readOnly=**false**)

  **public** **void** transfer(String outUser, String inUser, Integer jf) {

​    //接收积分

​    **this**.jdbcTemplate.update("update user set jf=jf+? where username=?",jf,inUser);

​    //模拟系统运行时的突发性问题

​    **int** i=1/0;

​    //赠送积分

​    **this**.jdbcTemplate.update("update user set jf =jf-? where username=？", jf, outUser);

  }

}
```

6创建测试类TransactionTest

```
package** com.ssm.jdbc;

**import** org.junit.Test;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** TransactionTest {

  @Test

  **public** **void** xmlTest(){

​    ApplicationContext applicationContext = **new** ClassPathXmlApplicationContext("applicationContext.xml");

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    userDao.transfer("zhangsan","lisi", 100);

​    System.***out\***.println("赠送积分成功！");

  }

  @Test

  **public** **void** annotationTest(){

​    ApplicationContext applicationContext = **new** ClassPathXmlApplicationContext("applicationContext-annotation.xml");

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    userDao.transfer("zhangsan","lisi", 200);

​    System.***out\***.println("赠送积分成功！");

  }

}
```

7创建配置文件applicationContext-annotation.xml

```
<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"*

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xmlns:aop=*"http://www.springframework.org/schema/aop"*

  xmlns:tx=*"http://www.springframework.org/schema/tx"*

  xmlns:context=*"http://www.springframework.org/schema/context"*

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​    *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd*

​    *http://www.springframework.org/schema/tx*

​    *http://www.springframework.org/schema/tx/spring-tx-4.3.xsd*

​    *http://www.springframework.org/schema/context*

​    *http://www.springframework.org/schema/context/spring-context-4.3.xsd*

​    *http://www.springframework.org/schema/aop*

​    *http://www.springframework.org/schema/aop/spring-aop-4.3.xsd"*>

  <!--1.配置数据源 -->

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

  <!--2.配置JDBC模板 -->

  <bean id=*"jdbcTemplate"* class=*"org.springframework.jdbc.core.JdbcTemplate"*>

​    <!--默认必须使用数据源 -->

​    <property name=*"dataSource"* ref=*"dataSource"* />

  </bean>

  <!--3.定义id为userDao的Bean -->

  <bean id=*"userDao"* class=*"com.ssm.jdbc.UserDaoImpl"*>

​    <!--将 jdbcTemplate注入到 userDao实例中 -->

​    <property name=*"jdbcTemplate"* ref=*"jdbcTemplate"* />

  </bean>

  <!--4.事务管理器，依赖于数据源 -->

  <bean id=*"transactionManager"* class=*"org.springframework.jdbc.datasource.DataSourceTransactionManager"*>

​    <property name=*"dataSource"* ref=*"dataSource"*/>

  </bean>

  <!--5.注册事务管理器驱动 -->

  <tx:annotation-driven transaction-manager=*"transactionManager"*/>

</beans>


```



结论：没遇到问题