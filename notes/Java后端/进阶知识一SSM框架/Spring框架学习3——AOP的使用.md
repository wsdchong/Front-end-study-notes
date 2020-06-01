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

1在eclipse基础开发环境创建一个springtest03的动态web项目，将spring的4个基本包以及commons-logging的包，还有spring-aop-4.3.6.RELEASE.jar、spring-aspects-4.3.6.RELEASE.jar、aspectjweaver-1.8.10.jar复制到lib目录中，并发布到类路径下。



## 二、基于XML的声明式AspectJ

1在src创建一个com.ssm.aspectj包，在包中创建接口UserDAO，并在接口中编写添加和删除的方法。代码如下：

2在com.ssm.aspectj包中创建接口实现类UserDaoImpl，并实现接口中的方法。代码如下：

3在src目录下创建在com.ssm.aspectj.xml包，在包中创建切面类MyAspect，并在类中分别定义不同类型的 通知。代码如下

4在com.ssm.aspectj.xml包中创建配置文件applicationContext.xml，并编写相关配置，代码如下。

5在com.ssm.aspectj.xml包中创建测试类TestXmlAspectJ，代码如下

6测试：



## 三、基于注解的声明式aspectj

1在src目录下创建在com.ssm.aspectj.annotation包，在包中创建切面类MyAspect。代码如下。（在UserDaoImpl中添加注解@Repository（“UserDao”））

2在com.ssm.aspectj.annotation包中创建配置文件applicationContext.xml，并编写相关配置，代码如下。

3在com.ssm.aspectj.annotation包中创建测试类TestAnotation，代码如下

4测试：

与XML相比，使用注解的方式更加方便和简单，且可以不用写实现AOP功能所配置的代码，提高开发效率。



## 四、第一个实验

1创建接口类UserDao

**package** com.ssm.aspectj;

**public** **interface** UserDao {

  **public** **void** addUser();

  **public** **void** deleteUser();

}

2创建接口实现类UserDaoImpl

**package** com.ssm.aspectj;

**import** org.springframework.stereotype.Repository;

@Repository("userDao")//用于注解方式

**public** **class** UserDaoImpl **implements** UserDao {

  **public** **void** addUser() {

​    System.***out\***.println("添加用户");

​    // 用于设置异常

​    // int i=10/0;

  }

  **public** **void** deleteUser() {

​    System.***out\***.println("删除用户");

  }

}

3创建MyAspect类

**package** com.ssm.aspectj.xml;

**import** org.aspectj.lang.JoinPoint;

**import** org.aspectj.lang.ProceedingJoinPoint;

/**

 \* 切面类，在此类中编写通知

 */

**public** **class** MyAspect {

  //前置通知

  **public** **void** myBefore(JoinPoint joinPoint){

​    System.***out\***.print("前置通知：模拟执行权限检查..，");

​    System.***out\***.print("目标类是："+joinPoint.getTarget());

​    System.***out\***.println("，被植入增强处理的目标方法为："+joinPoint.getSignature().getName());

  }

  //后置通知

  **public** **void** myAfterReturning(JoinPoint joinPoint) {

​    System.***out\***.print("后置通知：模拟记录日志..，");

​    System.***out\***.println("被植入增强处理的目标方法为：" + joinPoint.getSignature().getName());

  }

  /**

   \* 环绕通知

   \* ProceedingJoinPoint是JoinPoint的子接口，表示可执行目标方法

   \* 1.必须是Object类型的返回值

   \* 2.必须接收一个参数，类型为ProceedingJoinPoint

   \* 3.必须throws Throwable

   */

  **public** Object myAround(ProceedingJoinPoint proceedingJoinPoint) **throws** Throwable{

​    //开始

​    System.***out\***.println("环绕开始：执行目标方法之前，模拟开启事务..，");

​    //执行当前目标方法

​    Object obj=proceedingJoinPoint.proceed();

​    //结束

​    System.***out\***.println("环绕结束：执行目标方法之后，模拟关闭事务..，");

​    **return** obj;

  }

  //异常通知

  **public** **void** myAfterThrowing(JoinPoint joinPoint,Throwable e){

​    System.***out\***.println("异常通知：出错了"+e.getMessage());

  }

  //最终通知

  **public** **void** myAfter(){

​    System.***out\***.println("最终通知：模拟方法结束后释放资源..");

  }

}

4创建配置文件applicationContext.xml

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"*

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xmlns:aop=*"http://www.springframework.org/schema/aop"*

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​    *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd*

​    *http://www.springframework.org/schema/aop*

​    *http://www.springframework.org/schema/aop/spring-aop-4.3.xsd"*>

  <!-- 1 目标类 -->

  <bean id=*"userDao"* class=*"com.ssm.aspectj.UserDaoImpl"* />

  <!-- 2 切面 -->

  <bean id=*"myAspect"* class=*"com.ssm.aspectj.xml.MyAspect"* />

  <!-- 3 aop编程 -->

  <aop:config>

​    <!-- 1.配置切面 -->

​    <aop:aspect id=*"aspect"* ref=*"myAspect"*>

​      <!-- 2.配置切入点 -->

​      <aop:pointcut expression=*"execution(\* com.ssm.aspectj.\*.*(..))"*  id=*"myPointCut"* />

​      <!-- 3.配置通知 -->

​        <!-- 前置通知 -->

​        <aop:before method=*"myBefore"* pointcut-ref=*"myPointCut"* />

​        <!--后置通知-->

​        <aop:after-returning method=*"myAfterReturning"* pointcut-ref=*"myPointCut"* returning=*"returnVal"*/>

​        <!--环绕通知 -->

​        <aop:around method=*"myAround"* pointcut-ref=*"myPointCut"* />

​        <!--异常通知 -->

​        <aop:after-throwing method=*"myAfterThrowing"* pointcut-ref=*"myPointCut"* throwing=*"e"* />

​        <!--最终通知 -->

​        <aop:after method=*"myAfter"* pointcut-ref=*"myPointCut"* />

​    </aop:aspect>

  </aop:config>

</beans>

5创建测试类TestXmlAprectJ

**package** com.ssm.aspectj.xml;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**import** com.ssm.aspectj.UserDao;

**public** **class** TestXmlAspectJ {

  **public** **static** **void** main(String[] args) {

​    String xmlPath="com/ssm/aspectj/xml/applicationContext.xml";

​    ApplicationContext applicationContext=**new** ClassPathXmlApplicationContext(xmlPath);

​    //从容器中获得内容

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    //执行方法

​    userDao.addUser();

  }

}



## 五、第二个实验

1创建切面类

**package** com.ssm.aspectj.annotation;

**import** org.aspectj.lang.JoinPoint;

**import** org.aspectj.lang.ProceedingJoinPoint;

**import** org.aspectj.lang.annotation.After;

**import** org.aspectj.lang.annotation.AfterReturning;

**import** org.aspectj.lang.annotation.AfterThrowing;

**import** org.aspectj.lang.annotation.Around;

**import** org.aspectj.lang.annotation.Aspect;

**import** org.aspectj.lang.annotation.Before;

**import** org.aspectj.lang.annotation.Pointcut;

**import** org.springframework.stereotype.Component;

/**

 \* 切面类，在此类中编写通知

 */

@Aspect

@Component

**public** **class** MyAspect {

  //定义切入点表达式

  @Pointcut("execution(* com.ssm.aspectj.*.*(..))")

  //使用一个返回值为void、方法体为空的方法来命名切入点

  **public** **void** myPointCut(){}

  //前置通知

  @Before("myPointCut()")

  **public** **void** myBefore(JoinPoint joinPoint){

​    System.***out\***.print("前置通知：模拟执行权限检查..，");

​    System.***out\***.print("目标类是："+joinPoint.getTarget());

​    System.***out\***.println("，被植入增强处理的目标方法为："+joinPoint.getSignature().getName());

  }

  //后置通知

  @AfterReturning(value="myPointCut()")

  **public** **void** myAfterReturning(JoinPoint joinPoint) {

​    System.***out\***.print("后置通知：模拟记录日志..，");

​    System.***out\***.println("被植入增强处理的目标方法为：" + joinPoint.getSignature().getName());

  }

  /**

   \* 环绕通知

   \* ProceedingJoinPoint是JoinPoint的子接口，表示可执行目标方法

   \* 1.必须是Object类型的返回值

   \* 2.必须接收一个参数，类型为ProceedingJoinPoint

   \* 3.必须throws Throwable

   */

  @Around("myPointCut()")

  **public** Object myAround(ProceedingJoinPoint proceedingJoinPoint) **throws** Throwable{

​    //开始

​    System.***out\***.println("环绕开始：执行目标方法之前，模拟开启事务..，");

​    //执行当前目标方法

​    Object obj=proceedingJoinPoint.proceed();

​    //结束

​    System.***out\***.println("环绕结束：执行目标方法之后，模拟关闭事务..，");

​    **return** obj;

  }

  //异常通知

  @AfterThrowing(value="myPointCut()",throwing="e")

  **public** **void** myAfterThrowing(JoinPoint joinPoint,Throwable e){

​    System.***out\***.println("异常通知：出错了"+e.getMessage());

  }

  //最终通知

  @After("myPointCut()")

  **public** **void** myAfter(){

​    System.***out\***.println("最终通知：模拟方法结束后释放资源..");

  }

}

2创建配置文件

<?xml version=*"1.0"* encoding=*"UTF-8"*?>

<beans xmlns=*"http://www.springframework.org/schema/beans"*

  xmlns:xsi=*"http://www.w3.org/2001/XMLSchema-instance"*

  xmlns:aop=*"http://www.springframework.org/schema/aop"*

  xmlns:context=*"http://www.springframework.org/schema/context"*

  xsi:schemaLocation=*"http://www.springframework.org/schema/beans* 

​    *http://www.springframework.org/schema/beans/spring-beans-4.3.xsd*

​    *http://www.springframework.org/schema/aop*

​    *http://www.springframework.org/schema/aop/spring-aop-4.3.xsd*

​    *http://www.springframework.org/schema/context*

​    *http://www.springframework.org/schema/context/spring-context-4.3.xsd"*>

  <!-- 指定需要扫描的包，使注解生效 -->

  <context:component-scan base-package=*"com.ssm"* />

  <!-- 启动基于注解的声明式AspectJ支持 -->

  <aop:aspectj-autoproxy />

</beans>

3创建测试类

**package** com.ssm.aspectj.annotation;

**import** org.springframework.context.ApplicationContext;

**import** org.springframework.context.support.ClassPathXmlApplicationContext;

**import** com.ssm.aspectj.UserDao;

**public** **class** TestAnnotation {

  **public** **static** **void** main(String[] args) {

​    String xmlPath="com/ssm/aspectj/annotation/applicationContext.xml";

​    ApplicationContext applicationContext=**new** ClassPathXmlApplicationContext(xmlPath);

​    //从容器中获得内容

​    UserDao userDao=(UserDao)applicationContext.getBean("userDao");

​    //执行方法

​    userDao.addUser();

  }

}



结论：有些僵硬，没遇到问题，还想着与报错斗智斗勇。回头从eclipse转IDEA试试。