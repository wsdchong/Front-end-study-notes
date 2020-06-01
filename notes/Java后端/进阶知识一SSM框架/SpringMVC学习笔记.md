前言：

SpringMVC入门、SpringMVC数据绑定、JSON数据交互和RESTful支持、拦截器、SSM框架整合、

## 一、SpringMVC入门

1SpringMVC是spring提供的一个轻量级web框架，实现了webMVC设计模式。

它的好处是：提供了前段控制器DispatcherServlet，使开发人员无须额外开发控制器对象；基于XML的配置文件，在编辑后不需要重新编译应用程序；内置常见的校验器；

2入门实例：引入包；配置前端控制器web.xml；创建controller类；创建配置文件springmvc-config.xml，配置控制器映射信息；创建视图页面；测试；

3SpringMVC的注解：DispatcherServlet、controller注解类型、requestMapping注解类型、视图解析器

4基于注解的SpringMVC应用：搭建环境、修改配置文件、修改controller类、测试



## 二、SpringMVC数据绑定

1在数据绑定的过程中，SpringMVC框架会通过数据绑定组件（DataBinder）将请求参数串进行类型转换，然后将转换后的值赋给控制器类的方法的形参，这样后台就可以接收到客户端的参数。

具体的信息处理过程是：SpringMVC将servletRequest对象传递给dataBinder；DataBinder调用ConversionService组件进行处理，将ServletRequest对象中的消息填充到参数对象中；最后调用Validator组件对以及绑定请求消息数据的参数对象进行合法性校验。

2简单数据绑定：绑定默认数据类型、绑定简单数据类型、绑定POJO类型、绑定包装POJO

步骤：导入包、配置web.xml、springmvc-config.xml、创建controller、视图页面、绑定简单数据类型、POJO类型、绑定包装POJO。

3复杂数据绑定：绑定数组、绑定集合。



## 三、JSON数据交互和RESTful支持

1JSON和XML类似，用于存储数据，不过JSON的解析速度更快、占用空间更小。JSON有两种数据结构：对象结构{}和数组结构[]

2为了实现浏览器与控制器类（Controller）之间的数据交互，spring提供了一个HTTPMessageConverter<T>接口来完成此工作。SpringMVC默认处理JSON格式请求响应的实现类是MappingJacksona2HttpMessageConverter，利用JackSon开源包读写JSON数据，将Java对象转换为JSON对象和XML文档，同时将JSON对象和XML文档转换为Java对象。

3RESTful是一种软件架构风格或设计风格，把请求参数变成请求路径的一种风格。



## 四、拦截器

概念：

1拦截器的使用是普遍的，如用拦截器拦截未登录的用户，或者使用它验证已登录用户的权限。SpringMVC的拦截器（Interceptor）类似servlet中的过滤器（Filter），用于拦截用户请求并做相应的处理。

2要使用拦截器（Interceptor），需要对拦截器类进行定义和配置。通常通过HandlerInterceptor接口或WebRequestInterceptor接口定义。

3拦截器的执行过程：单个的、多个的



应用：

1用户登录权限验证



## 五、SSM框架整合

1整合思路：通过spring实例化bean，然后调用实例对象中的查询方法执行mybatis映射文件中的SQL语句，如果能够正确查询出数据库中的数据，则spring与mybatis整合成功；

2准备所需包：

Spring包

Mybatis包

数据库连接池

MySQL驱动包

SpringMVC包

3编写配置文件

数据库常量配置文件db.properties

Spring配置文件ApplicationContext.xml

Mybatis配置文件mybatis-config.xml

SpringMVC配置文件SpringMVC-config.xml

前端控制器Web.xml：配置文件监听器、过滤器和前端控制器

4测试