# 对SSM的理解

## 前言：

前置知识和后续知识，知识是承前启后的。

从三个方面分析，首先从其本质分析，毕竟万变不离其宗，任何东西不是无中生有的，它总有一个前身。分析本质，有利于我们知道这个是干什么的；

然后将与前身相比，它的优越性，毕竟学习是有性价比的。通过对比分析优越性，有利于我们知道我们用这个的理由在哪；

最后分析如何学习。有利于我们掌握这个东西。

 [toc]



## 一、spring的理解

Spring给我的印象是面向对象编程的升级版，核心思想是IOC和AOP，以反射为原理，通过bean和注解来提高Java编程效率。

IOC使得代码的每一个class独立出来，使用对象的时候，不用像以前一样，还需要主动去new一个，现在可通过依赖注入使bean容器帮助自动创建，提高代码的可复用性。

AOP将分散在各个方法中的重复代码提取出来，如事务、日志、异常等。大大提高了开发效率和代码维护性。

总之，与传统的面向对象编程OOP相比，面向切面编程AOP提高了代码的复用性，可维护性，可读性。

所以spring的前置知识是下图中Java的反射和注解。可以通过下面这篇博客来进行全面科普，掌握的话，需要自行深入。

https://blog.csdn.net/qq_36894974/article/details/106010941                               

 ![Java基础](C:\Users\Administrator\Documents\GitHub\Front-end-study-notes\road\Java基础.png)

spring给我的感觉就是Java的进一步发展，从面向对象发展到面向切面，目的是提高代码复用性，让更多人更易上手；提高开发效率和维护性，让开发和维护更快；

入手spring可以先学习DI（构造注入到设值注入）、bean装配（XML到annotation）、AOP（XML到注解），对spring的基本概念有初步掌握，然后学习JDBCTemplate类的使用，事务的使用，对数据库和事务有spring的初步应用。

感觉spring的前置知识的OOP编程的Java，后置知识是springboot的使用（在spring的基础上把配置优化了）。不过学好spring，归根结底需要学好Java。

讲反射：https://blog.csdn.net/Mr_wxc/article/details/105812627

Spring的基本使用：https://blog.csdn.net/weixin_42875245/article/details/106034031

 

## 二、mybatis的理解

Mybatis给我的感觉是JDBCTemplate的升级版，核心思想是对象关系映射ORM，通过配置文件和映射文件为实现映射，通过sqlsessionFactory和sqlsession来使用映射。

配置文件用来配置properties、setting、environment、mapper等；

映射文件用于写映射语句，如select、insert、update、delete、SQL、resultMap；

sqlsessionFactory是单个数据库映射关系经过编译后的内存镜像，用于创建session。

Sqlsession是应用程序与持久层之间执行交互操作的一个单线程对象，用于执行持久化操作。Sqlsession对象包含数据库中所有执行SQL操作的方法。

与JDBCTemplate相比，在XML中进行配置和映射，使用更形象，便于新手入门；每次使用只需调用已设好的映射，降低重复代码，大大提高编程效率。

Mybatis的本质的SQL的映射，归根结底还是需要把SQL语句学好，把数据库学好。数据库和SQL学好了，mybatis的作用只是桥梁，联通数据库和应用程序直接的桥梁。

数据库的学习：《数据库系统概论》等。

MySQL的学习：《MySQL必知必会》等。

MySQL的基本使用：https://blog.csdn.net/weixin_42875245/article/details/105912850

Mybatis的基本使用：

 

## 三、springmvc的理解

Springmvc给我的感觉是servlet的进阶版，核心思想是全部请求统一用一个servlet（dispatcherservlet）去做请求与控制。用spring来写servlet。

Springmvc的执行流程：

1前端控制器dispatchServlet拦截到请求，调用处理器映射器handlerMapping来处理；2处理器映射器根据请求，生成处理器对象返回给前端控制器；

3前端控制器收到信息选择合适的处理器适配器handleAdapter；4处理器适配器执行处理器，也就是程序中编写的后端控制器controller；5后端控制器执行完，返回视图名给处理器适配器，适配器又返回给前端控制器；

6前端控制器收到信息选择合适的视图解析器viewResolve；7视图解析器解析后，返回视图给前端控制器；

8前端控制器对view进行渲染。渲染完成后返回给客户端浏览器。

@requestbody的使用：https://blog.csdn.net/justry_deng/article/details/80972817

通过初步使用，我觉得Springmvc的核心是配置文件（设置前端控制器）和后端控制器controller（@requestMapping）。

与servlet相比，有注解功能的springmvc可读性更好，重复代码更少，编程体验更佳。

要向学好springmvc需要从两方面入手，一是学好servlet和HTTP，二是学好spring或者springboot；

HTTP：https://blog.csdn.net/qq_36894974/article/details/103930478

Servlet：包括servlet、jsp、网络编程

Springmvc：入门、数据绑定、json数据绑定、拦截器

 

 2020/5/18写。



才疏学浅，请大佬指错。后期会不断修改

更新地址：[GitHub](https://github.com/wsdchong/Front-end-study-notes)

更多内容请关注：[CSDN](https://blog.csdn.net/weixin_42875245)、[GitHub](https://github.com/wsdchong/Front-end-study-notes)