前言：在整合三大框架的基础上实现系统后台的用户管理、用户登录、登录验证、新闻发布管理。

前台页面使用jQuery+bootstrap框架完成新闻展示；

## 一、系统概述

1系统功能需求：

用户管理（角色设置和登录验证）、新闻类别管理、新闻发布管理和前台新闻展示

2系统架构设计：

持久对象层：持久化类（实体类）

数据访问层：DAO接口和mybatis映射文件。接口统一DAO结尾；映射文件与接口名称相同

业务逻辑层：service接口和实现类。接口统一Service结尾，其他实现类统一在接口名后加Impl。

Web表现层：SpringMVC的controller类和JSP页面。Controller类主要负责拦截用户请求、调用业务逻辑层的相应组件来处理用户请求，并把结果返回给JSP。

3数据分析和设计：

角色实体：角色表t_role

用户实体：用户表t_user

新闻类别实体：新闻类别表t_category

新闻实体：新闻类别t_news

4系统功能设计与实现

开发环境与框架搭建

角色管理模块

用户管理模块

新闻类别管理模块

新闻发布管理模块

前台新闻展示模块



## 二、实现

1开发环境与框架搭建

创建项目，引入包；

编写配置文件；

创建项目相关目录（包）和文件，并引入相关文件资源

2角色管理模块

创建持久化类：role、user

实现DAO：role、user及映射文件

实现Service：role、user接口及实现类

实现UserController：通过@Autowired注解将RoleService对象和UserService对象注入本类，然后创建对用户进行增删改查、登录、退出的方法；

实现页面功能login.jsp、user_list.jsp、add_user.jsp、edit_user.jsp

测试：将项目发布到Tomcat服务器并启动。

3新闻管理模块

创建持久化类：category、news、分页工具类pageBean

实现DAO：

实现Service：

实现NewsController：将两个对象注入NewsController中

实现页面功能：news、add_news、edit_news

测试

4登录验证

创建登录拦截器类LoginInterceptor

配置拦截器

测试