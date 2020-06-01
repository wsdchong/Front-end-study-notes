# springboot代码使用

## 前言

把《springboot+Vue全栈开发实战》跑一遍。记录跑一遍过程中遇到的问题。

[toc]

## 第一章 入门

共用三个项目。

chapter01应该是用maven工程来创建的。

chapter01-2应该是用spring initializr插件创建的。

通过file-open导入chapter01；然后就报错。我看了看IDEA的界面，看是不是maven在导入我之前没安装过的springboot。一看底部，果然，event log报了三个错。

```
Error Loading Project: Cannot load facet Spring (chapter01) Details...

Error Loading Project: Cannot load facet Web (chapter01) Details...

Features covered by IntelliJ IDEA Ultimate Spring Support, Java EE: EJB, JPA, Servlets are detected
			Try IntelliJ IDEA Ultimate
			Do not suggest Ultimate
```

前两个说我无法加载spring和web；后一个问我要不要尝试IDEA终极版（付钱版）；后一个我当然选择No，前两个我点了details，然后它问我忽略不，然后我也选择不忽略。应该和我没安装过springboot有关。

```
IDEA三个版本：
Community：社区版，免费，但是功能有限制，Android Studio就是基于这个版本定制的。

Ultimate：终极版，收费，功能无限制。

EAP：终极版的免费版，免费，功能无限制，但是每隔30天要重装一次。
```

最后我等这个下载，等了十分钟，算了，我还是干干其他事。这个先等着。

哈哈哈，等了34分钟，终于下载完了。

我运行一下APP类，发现可行。这个比用eclipse舒服些，eclipse还需要自己配置环境，引入包。

### 用maven创建springboot的步骤

1用IDEA创建一个maven工程。groupid创建为org.sang，artifactID和project name创建为chapter01；

2添加依赖。在pom.xml中添加spring-boot-starter-parent依赖和引入一个web的 starter；

3编写启动类。在src-java中创建APP类还有一个HelloController类。

4运行。在IDE中运行APP类的main方法。然后浏览器中输入http://localhost:8080/hello。结果我的没没显示。我猜和我昨天弄Tomcat7的server.xml有关，我好像把8080端口改为80了。我看了一下server.xml，没呀，我改回来了。那么会是什么情况呢。我觉得和IDEA默认配置的Tomcat相关，也不知道它连的是哪个。点开file-settings-tomcatserver，一看是Tomcat9.0.33。最后我决定好好看看日志。发现

```
Tomcat initialized with port(s): 8081 (http)

Starting Servlet Engine: Apache Tomcat/8.5.31
```

看了看src-resources里的application.properties。发现显示server.port=8081。

于是尝试了一下http://localhost:8081/hello。果然成功了。

### 用spring initializr创建springboot的步骤。

可惜这个插件在社区版的IDEA中不存在。但是没关系，第一个都都实现，这第二个就简单了解一下即可。

我依然是file-open打开chapter01-2；然后就是等待环节又要下载。等待的过程中，我看到了pom.xml和maven-plugin的内容都标红了，我猜要么是我的IDEA是社区版的，要么是没加载完。依旧是用了34分钟，好神奇，

然后给我显示

```
Cannot resolve plugin org.springframework.boot:spring-boot-maven-plugin:<unknown>
```

无法解析插件。

百度一下：[spring-boot-maven-plugin not found的解决方案](https://www.cnblogs.com/vevy/p/12246679.html)

然后这个对于我遇到的问题没用。应该和我版本不同

然后那本书还说，以后都用这个方式创建。看来我得入手正式版了。

不过第一章中学到用maven来创建springboot也是足够了。

还有一个chapter01-3项目，我打开一下，估计又得34分钟，我猜会不会是IDEA设置的，为了让用户买他们的终极版。好吧，这次是47分钟。

然后这个项目虽然没那个报错了，但是没有运行类。僵硬。可能也没打算写吧。亏我还去每个文件夹中找。

## 第二章 springboot 基础配置

这一章就是讲讲springboot的细枝末节，算是过渡章节。

```
1不使用spring-boot-starter-parent。因为有些公司开发微服务项目或多模块项目时一般是用公司自己的parents。这个时候如果还想进行项目依赖版本的统一管理，就需要用dependencyManagement来实现。配置Java版本、编码格式等。

2@spring bootApplication。springboot的注解加在项目的启动类，避免代码的重复书写，提高可读性和可维护性。其中@spring bootApplication是一个组合注解，这个注解由三个注解构成：@spring bootconfiguaration（顾名思义，配置类）、@EnableAutoConfiguration（自动化配置）、@ComponentScan（包扫描）。

3定制banner。banner是spring boot项目启动时打印出的logo。书上讲了如何更改logo和关闭。

4web容器配置。在application.properities配置端口、项目名等。在spring boot项目中默认Tomcat为web容器。也可以配置使用jetty、Undertow。

5Properities配置。按照优先级有config、root、src-main-resources-config、src-main-resources。还可以使用application.yml作为配置文件。

6类型安全配置属性。将配置（properties或者yaml)加载到spring environment中。

7YAML配置。yaml是json的超集，一种专门书写配置文件的语言，可以代替properties。使用yaml，需要在spring-boot-starter-web依赖间接引入snakeyaml依赖，snakeyaml实现对yaml配置的解析。使用简单、利用缩进来表示层级关系，并且大小写敏感。

8profile。开发者在发布项目之前，一般会在开发环境、测试环境、生产环境之间进行切换。这个时候就需要进行大量的配置修改。spring用@profile注解来解决。
```

之后就是尝试运行chapter02、chapter02-1、chapter02-2.

打开chapter02的时候，弹出了一个maven build script found。然后我选择import。接下来就是等待了。好奇怪，不应该啊，我之前都加载了三个项目了，应该只需要resolving，不用download的。然后对比里面的文件，发现这个项目主要讲第六部分的类型安全配置属性。方便理解properties文件如何被引入。

打开chapter02-1的时候，成功运行，虽然配置文件是服务器的端口是80，但是我用8080进去的。这个项目对于第七部分的内容：yaml配置

打开chapter02-2的时候，成功运行。这个项目对于第五部分的内容，讲properties文件的优先级。

## 第三章 springboot整合视图层技术

这章讲了两个内容：整合Thymeleaf、整合FreeMarker；

它的项目有chapter03、chapter03-1、chapter03-2、chapter03-3、chapter03-4、chapter03-4-2.

第一个chapter03项目中已经整合了两个。点击impact。项目就resolving。

然后我打开其他五个项目，看看内容。

其中chapter03-1里的pom.xml中有Jackson和fastjson的引用，神奇，估计是写着玩的项目。

chapter03-2里pom.xml和本章内容无关，僵硬。

chapter03-3里有thymeleaf的配置。应该是个正式的例子。还写了不少类和HTML。比chapter03更全面。

chapter03-4里有freemarker的配置。虽然也很正式，但是看得出作者是以thymeleaf为主，freemarker只是了解而已。其中没有HTML文件。有主类但是不能运行。

chapter03-4-2里有thymeleaf的配置。比chapter03-3更具体。

综上所述，这一章用chapter03-4-2来了解thymeleaf。

### 整合thymeleaf

1创建工程，添加依赖。

2配置thymeleaf。在ThymeleafProperties类中自动化配置，路径、后缀、编码等。

3配置控制器。

4创建视图。在src-resources中创建视图。

5运行。

## 第四章 整合web开发



[前言](#前言)