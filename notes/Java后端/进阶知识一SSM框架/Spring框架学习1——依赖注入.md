前言：这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

写这篇文章的出发点一个是为了保障自己学以致用，一个是查漏补缺。

而且很多教程虽然说按照那个步骤可以成功，但也可能不成功，要么是自己操作有误，要么是版本变了，写的内容也要与时俱进。写这类博客，即写步骤，又写操作过程中遇到的问题，然后从中吸取教训，可以让成功的概率更大。



## 一、引入包

1在eclipse基础开发环境创建一个springtest01的动态web项目，将spring的4个基本包以及commons-logging的包复制到lib目录中，并发布到类路径下。



## 二、用构造注入

1在src创建一个com.ssm.ioc_di包，在包中创建接口UserDao，然后在接口中定义一个login（）方法。代码如下：

2在com.ssm.ioc_di包创建usergo的实现类UserDaoImpl，在该类实现接口中的login方法。代码如下

3在src目录下创建Spring的配置文件applicationContext.xml，并在配置文件中创建一个UserDao的bean。代码如下：

4在com.ssm.ioc_di包中创建测试类IOC，并在类中编写main()方法以及实现IOC的代码。代码如下

5测试：控制台成功输出UserDaoImpl类的输出语句，代表成功。在main方法中，没通过new一个UserDao接口的实现类，而是通过spring容器来获取实现类对象。这就是spring的控制反转。



## 三、用set方法注入

1在com.ssm.ioc_di包中创建接口UserService，并编写一个login方法。代码如下

2在com.ssm.ioc_di包中创建接口UserService的实现类UserServiceImpl，在类汇总申明userDao属性，并添加属性的setter方法。代码如下：

3在配置文件中创建一个id为userService的bean，该bean用于实例化UserServiceImpl类的信息，并将name为userDao的实例注入userService中，代码如下：

4在com.ssm.ioc_di包中创建测试类DI，并在类中编写main()方法以及实现DI的代码。代码如下

5测试：这两个的区别好像接口类与配置文件不同。

不过核心意思就是用这个依赖注入和控制反转，可以实现依赖关系对象之间的解耦。每次使用一个对象的时候不要再去主动声明他的父类（假如有的话），这个交给IOC容器来帮助申明。好处有1复用性好，把普遍使用的组件独立出来，反复用到项目中；2可维护。



## 四、第一部分中遇到的问题

1创建接口类：new-interface；

**package** com.ssm.ioc_di;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** IoC {

  **public** **static** **void** main(String[] args) {

​    //1.初始化Spring容器，加载配置文件

​    ApplicationContext applicationContext=**new** ClassPathXmlApplicationContext("applicationContext.xml");

​    //2.通过容器获取userDao实例

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    //3.调用实例中的login()方法

​    userDao.login();

  }

}

2创建接口实现类：new-class-add interfaces

**package** com.ssm.ioc_di;



**public** **class** UserDaoImpl **implements** UserDao {



  @Override

  **public** **void** login() {

​    // **TODO** Auto-generated method stub

​    System.***out\***.println("UserDao login.");

  }

}

3配置文件：new-xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"* 

​    xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*   

​    xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​      *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd"*>

​      <!-- 将指定类配置给Spring，让Spring创建其对象的实例 -->

​    <bean id=*"userDao"* class=*"com.ssm.ioc_di.UserDaoImpl"*>

​    </bean>



</beans>

4测试类：new-class

**package** com.ssm.ioc_di;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** IoC {

  **public** **static** **void** main(String[] args) {

​    //1.初始化Spring容器，加载配置文件

​    ApplicationContext applicationContext=**new** ClassPathXmlApplicationContext("applicationContext.xml");

​    //2.通过容器获取userDao实例

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    //3.调用实例中的login()方法

​    userDao.login();

  }

}

5测试：成功。



## 五、第二部分遇到的问题

1创建接口

**package** com.ssm.ioc_di;



**public** **interface** UserService {

  **public** **void** login();

}

2创建接口实现类

**package** com.ssm.ioc_di;



**public** **class** UserServiceImpl **implements** UserService {

  //声明userDao属性

  **private** UserDao userDao;

  //添加userDao属性的setter方法，用于实现依赖注入

  **public** **void** setUserDao(UserDao userDao) {

​    **this**.userDao = userDao;

  }

  //实现接口中的方法

  @Override

  **public** **void** login() {

​    // 调用userDao中的login方法，并执行输出语句

​    **this**.userDao.login();

​    System.***out\***.println("userService login");

  }

}

3再applicationContext中加入bean

​    <!-- 添加一个id为userService的Bean -->

​    <bean id=*"userService"* class=*"com.ssm.ioc_di.UserServiceImpl"*>

​      <!-- 将id为userDao的Bean实例注入到userService实例中 -->

​      <property name=*"userDao"* ref=*"userDao"*/>

  </bean>

4创建测试类

**package** com.ssm.ioc_di;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** DI {

  **public** **static** **void** main(String[] args) {

​    // 1.初始化Spring容器，加载配置文件

​    ApplicationContext applicationContext = **new** ClassPathXmlApplicationContext("applicationContext.xml");

​    // 2.通过容器获取userService实例

​    UserService userService = (UserService) applicationContext.getBean("userService");

​    // 3.调用实例中的login()方法

​    userService.login();

  }

}

5运行

成功



总结：没遇到报错。看之后会不会遇到