前言：这个文章的定位不是实现的步骤，而是实现过程中遇到的问题。并且我写的步骤是别人的步骤的记录，算不了什么，后面对使用过程中遇到的问题以及解决的方法才是自己写的，有价值的地方。

写这篇文章的出发点一个是为了保障自己学以致用，一个是查漏补缺。

而且很多教程虽然说按照那个步骤可以成功，但也可能不成功，要么是自己操作有误，要么是版本变了，还有可能自己基础没学好，前置知识不够。我最开始写Java的时候连创建父类和接口类都不会，直接创建一个类，然后复制粘贴，最后报错。僵硬~

写这类博客，即写步骤，又写操作过程中遇到的问题，然后从中吸取教训，可以让成功的概率更大。

同时sprig框架学习我打算按照五部分（IOC、bean、AOP、数据库、事务）进行梳理，最后加个综合大应用。学前在注意的情况下，会写前置知识。

Java基础：https://blog.csdn.net/weixin_42875245/article/details/105951858

IDE使用：https://blog.csdn.net/weixin_42875245/article/details/105867499

Spring学习笔记：https://blog.csdn.net/weixin_42875245/article/details/105631818

Spring见解：https://blog.csdn.net/Haidaiya/article/details/105611801



## 一、引入包

1在eclipse基础开发环境创建一个springtest02的动态web项目，将spring的4个基本包以及commons-logging的包，还有spring-aop-4.3.6.RELEASE.jar复制到lib目录中，并发布到类路径下。



## 二、bean的作用域（singleton和prototype）

1在src创建一个com.ssm.scope包，在包中创建Scope类，不定义方法。代码如下：

2在src目录下创建Spring的配置文件applicationContext.xml，并在配置文件中创建一个scope的bean，且指定class属性所对应的实现类为Scope。代码如下：

3在com.ssm.scope包中创建测试类ScopeTest来测试singleton作用域。代码如下

4测试：控制台输出两次的结果相同，说明spring容器只创建了一个Scope类的实例。

5 把scope的bean定义为作用域为prototype；

6测试：控制台输出的两次bean实例不相同，说明在prototype作用域下创建了两个不同的scope实例。

最后分析为什么要了解这个作用域，用东西要知其然亦知其所以然。

https://www.cnblogs.com/amunamuna/p/10959796.html

这个里面讲了五种，实际上不止，最好上官网上了解，不过这个文章还是可以借鉴其角度来学习。



## 三、基于XML的装配

1在scr目录下，创建一个com.ssm.assemble包中创建User类，并在类中定义userName、password和list集合3个属性以及对于的setter方法。代码如下

2在配置文件中，通过增加构造注入和设置注入的方法装配User实例的两个bean。代码如下：

3在com.ssm.assemble包中创建测试类XMLAssembleText，在类中分别获取并输出配置文件的user1和user2实例。代码如下

5测试：成功输出基于XML装配的构造注入和设值注入两个方式装配的user实例。



## 四、基于annotation的装配

1在scr目录下，创建一个com.ssm.annotation包，在该包中创建接口UserDAO，并在接口中定义一个save方法。代码如下

2在com.ssm.annotation包中创建接口实现类UserDAOImpl，在该类中实现接口中的save方法。用到repository注解，代码如下

3在com.ssm.annotation包中创建接口UserService，在接口中定义定义一个save 方法。代码如下

4在com.ssm.annotation包中创建接口实现类UserServiceImpl，在该类中实现接口中的save方法。用到@service注解和@resource注解，代码如下

5在com.ssm.annotation包中创建控制类UserController。用到@controller注解和@resource，代码如下：

6创建配置文件bean1.xml，在配置文件中编写基于annotation装配的代码。代码如下

7在com.ssm.annotation包中创建测试类annotationAssembleTest，在类中编写测试方法并定义配置文件的路径，然后通过spring容器加载配置文件并不去userController实例。代码如下

8测试：spring容器成功获取了userController的实例。并且调用实例的方法执行各层中的输出语句。

对比一下基于XML的装配方式，Annotation的装配方式可以减少配置文件的代码量，使编写程序的人效率提高，且代码阅读性高（程序的进步，就是写且写一次，大量提高效率）



## 五、第一个实验

1创建Scope类

**package** com.ssm.scope;

**public** **class** Scope {

}

2创建配置文件applicationContext.xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"* 

​    xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*   

​    xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​      *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd"*>

​    <!-- 将指定类配置给Spring，让Spring创建其对象的实例 -->

​    <!-- <bean id="scope" class="com.ssm.scope.Scope"/> -->

  <bean id=*"scope"* class=*"com.ssm.scope.Scope"* scope=*"prototype"*/>

</beans>

3创建测试类ScopeTest来测试作用域

**package** com.ssm.scope;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** ScopeTest {

  **public** **static** **void** main(String[] args) {

​    // 1.初始化Spring容器，加载配置文件

​    ApplicationContext applicationContext = **new** ClassPathXmlApplicationContext("applicationContext.xml");

​    // 2.输出获得的实例

​    System.***out\***.println(applicationContext.getBean("scope"));

​    System.***out\***.println(applicationContext.getBean("scope"));

​    System.***out\***.println("");

​    System.***out\***.println("");

​    System.***out\***.println("");

​    System.***out\***.println("");

  }

}



## 六、第二个实验

1创建类User

**package** com.ssm.assemble;

**import** java.util.List;

**public** **class** User {

  **private** String userName;

  **private** String password;

  **private** List<String> list;

  /**

   \* 1.使用构造注入

   \* 1.1提供带所有参数的构造方法

   */

  **public** User(String userName, String password, List<String> list) {

​    **super**();

​    **this**.userName = userName;

​    **this**.password = password;

​    **this**.list = list;

  }

  @Override

  **public** String toString() {

​    **return** "User [userName=" + userName + ", password=" + password + ", list=" + list + "]";

  }

  /**

   \* 2.使用设值注入

   \* 2.1提供默认空参构造方法

   \* 2.2为所有属性提供setter方法

   */

  **public** User() {

​    **super**();

  }

  **public** **void** setUserName(String userName) {

​    **this**.userName = userName;

  }

  **public** **void** setPassword(String password) {

​    **this**.password = password;

  }

  **public** **void** setList(List<String> list) {

​    **this**.list = list;

  }

}

2在applicationContext.xml配置文件中加

​    <bean id=*"user1"* class=*"com.ssm.assemble.User"*>

​      <constructor-arg index=*"0"* value=*"wsdchong"* />

​      <constructor-arg index=*"1"* value=*"123456"* />

​      <constructor-arg index=*"2"*>

​        <list>

​          <value>"constructorValue1"</value>

​          <value>"constructorValue2"</value>

​        </list>

​      </constructor-arg>

​    </bean>  

​    <bean id=*"user2"* class=*"com.ssm.assemble.User"*>

​      <property name=*"userName"* value=*"admin"*></property>

​      <property name=*"password"* value=*"rome"*></property>

​      <property name=*"list"*>

​        <list>

​          <value>"listValue1"</value>

​          <value>"listValue2"</value>

​        </list>

​      </property>

  </bean>  

3创建测试类XMLAssembleTest，

**package** com.ssm.assemble;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** XmlAssembleTest {

  **public** **static** **void** main(String[] args) {

​    // 1.初始化Spring容器，加载配置文件

​    ApplicationContext applicationContext = **new** ClassPathXmlApplicationContext("applicationContext.xml");

​    // 2.输出获得的实例

​    System.***out\***.println(applicationContext.getBean("user1"));

​    System.***out\***.println(applicationContext.getBean("user2"));

  }

}



## 六、第三个实验

1创建接口UserDAO

**package** com.ssm.annotation;

**public** **interface** UserDao {

  **public** **void** save();

}

2创建接口实现类UserDaoImpl

**package** com.ssm.annotation;

**import** org.springframework.stereotype.Repository;

@Repository("userDao")

**public** **class** UserDaoImpl **implements** UserDao {

  **public** **void** save() {

​    System. ***out\***. println("执行userDao.save()");

  }

}

3创建接口UserService

**package** com.ssm.annotation;

**public** **interface** UserService {

  **public** **void** save();

}

4创建接口实现类UserServiceImple

**package** com.ssm.annotation;

**import** javax.annotation.Resource;

**import** org.springframework.stereotype.Service;

@Service("userService")

**public** **class** UserServiceImpl **implements** UserService {

  @Resource(name="userDao")

  **private** UserDao userDao;

  **public** **void** save() {

​    **this**.userDao. save();

​    System.***out\***.println("执行userService.save()");

  }

}

5创建控制器类UserContext

**package** com.ssm.annotation;

**import** javax.annotation.Resource;

**import** org.springframework.stereotype.Controller;

@Controller("UserController")

**public** **class** UserController {

  @Resource(name="userService")

  **private** UserService userService;

  **public** **void** save(){

​    **this**.userService.save();

​    System.***out\***.println("运行userController.save()");

  }

}

6创建配置文件bean.xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"* 

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xmlns:context=*"http://www.springframework.org/schema/context"*   

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

  *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd*

  *http://www.springframework.org/schema/context*

  *http://www.springframework.org/schema/context/spring-context-4.3.xsd"*>

  <!-- 使用context命名空间，在配置文件中开启相应的注解处理器 -->

  <context:annotation-config />

  <!-- 分别定义3个Bean实例 -->

  <bean id=*"userDao"* class=*"com.ssm.annotation.UserDaoImpl"* />

  <bean id=*"userService"* class=*"com.ssm.annotation.UserServiceImpl"* />

  <bean id=*"userController"* class=*"com.ssm.annotation.UserController"* />

   <!--可以用第16行代替10-14行/> -->

  <!-- <context: component-scan base-package="com.ssm.annotation"/> -->

   <!-- 也可以使用自动装配来代替10-14行/> -->

</beans>

7创建测试类AnnotationAssembleTest.xml

**package** com.ssm.annotation;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**public** **class** AnnotationAssembleTest {

  **private** **static** ApplicationContext *applicationContext*;

  **public** **static** **void** main(String[] args) {

​    // 定义配置文件路径

​    String xmlPath = "com/ssm/annotation/bean1.xml";

​    *applicationContext* = **new** ClassPathXmlApplicationContext(xmlPath);

​    // 获取 UserController实例

​    UserController userController = (UserController) *applicationContext*.getBean("userController");

​    // 调用 UserController中的save()方法

​    userController.save();

  }

}



结论：有些僵硬，没遇到问题，还想着与报错斗智斗勇。