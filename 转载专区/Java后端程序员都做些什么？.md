## [Java后端程序员都做些什么？](https://www.cnblogs.com/java1024/p/8193053.html)

前言：这是我转载Java站长三篇文章的第三篇。这篇文章地位没有前两篇高，但是他让我对Java后端的发展历程第一次有了清晰的认识。特别是第二部分讲后端技术，真的把那些技术的起因经过结尾将明白了。而不是我只是一个一个知识点的百度，知识太零散。看了这部分我总是把这些联系在一起了。



这个问题来自于QQ网友，一句两句说不清楚，索性写个文章。

我刚开始做Web开发的时候，根本没有前端，后端之说。

原因很简单，那个时候服务器端的代码就是一切：接受浏览器的请求，实现业务逻辑，访问数据库，用JSP生成HTML，然后发送给浏览器。

即使后来Javascript在浏览器中添加了一些AJAX的效果，那也是锦上添花，绝对不敢造次。因为页面的HTML主要还是用所谓“套模板”的方式生成：美工生成HTML模板，程序员用JSP,Veloctiy,FreeMaker等技术把动态的内容添加上去，仅此而已。

那个时候最流行的图是这个样子：

![image](https://upload-images.jianshu.io/upload_images/4624881-babe61ffd7c5bf18?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在最初的J2EE体系中，这个表示层可不仅仅是浏览器中运行的页面，还包括Java写的桌面端，只是Java在桌面端太不争气， 没有发展起来。

每个程序员都是所谓“全栈”工程师，不仅要搞定HTML, JavaScript, CSS，还要实现业务逻辑，编写访问数据库的代码。等到部署的时候，就把所有的代码打成一个WAR包，往Tomcat指定的目录一扔，测试一下没问题，收工回家！

不差钱的公司会把程序部署到Weblogic，Websphere这样的应用服务器中，还会用上高大上的EJB。

虽然看起来生活“简单”又“惬意”，但实际上也需要实现那些多变的、不讲逻辑的业务需求，苦逼的本质并没有改变。

# 1. 前后端的分离

随着大家对浏览器页面的视觉和交互要求越来越高，“套模板”的方式渐渐无法满足要求，这个所谓的表示层慢慢地迁移到浏览器当中去了，一大批像Angular, ReactJS之类的框架崛起，前后端分离了！

后端的工程师只负责提供接口和数据，专注于业务逻辑的实现，前端取到数据后在浏览器中展示，各司其职。

像Java这样的语言很适合去实现复杂的业务逻辑，尤其是一些MIS系统，行业软件如税务、电力、烟草、金融，通信等等。 所以剥离表示层，只做后端挺合适的。 

但是如果仅仅是实现业务逻辑，那后端也不会需要这么多技术了，搞定SSH/SSM就行了。 

# 2. 后端技术

互联网，尤其是移动互联网开始兴起以后，海量的用户呼啸而来，一个单机部署的小小War包肯定是撑不住了，必须得做分布式。 

原来的单个Tomcat得变成Tomcat的集群，前边弄个Web服务器做请求的负载均衡，不仅如此，还得考虑状态问题，session的一致性。

业务越来越复杂，我们不得不把某些业务放到一个机器（或集群）上，把另外一部分业务放到另外一个机器（或集群）上，虽然系统的计算能力，处理能力大大增强，但是这些系统之间的通信就变成了头疼的问题，消息队列（MQ)，RPC框架（如Dubbo）应运而生，为了提高通信效率，各种序列化的工具(如Protobuf)也争先空后地问世。

单个数据库也撑不住了，那就做数据库的读写分离，如果还不行，就做分库和分表，把原有的数据库垂直地切一切，或者水平地切一切， 但不管怎么切，都会让应用程序的访问非常麻烦，因为数据要跨库做Join/排序，还需要事务，为了解决这个问题，又有各种各样“数据访问中间件”的工具和产品诞生。

为了最大程度地提高性能，缓存肯定少不了，可以在本机做缓存(如Ehcache)，也可以做分布式缓存(如Redis)，如何搞数据分片，数据迁移，失效转移，这又是一个超级大的主题了。

互联网用户喜欢上传图片和文件，还得搞一个分布式的文件系统（如FastDFS），要求高可用，高可靠。

数据量大了，搜索的需求就自然而然地浮出水面，你得弄一个支持全文索引的搜索引擎(如Elasticsearch ,Solr)出来。

林子大了，什么鸟都有，必须得考虑安全，数据的加密/解密，签名、证书，防止SQL注入，XSS/CSRF等各种攻击。

# 3. “大后端”

前面提到了这么多的系统，还都是分布式的，每次上线，运维的同学说：把这么多系统协调好，把老子都累死了。

得把持续集成做好，能自动化地部署，自动化测试（其实前端也是如此），后来出现了一个革命化的技术docker， 能够让开发、测试、生成环境保持一致，系统原来只是在环境（如Ngnix, JVM,Tomcat,MySQL等）上部署代码，现在把代码和环境一并打包， 运维的工作一下子就简化了。

公司自己购买服务器比较贵，维护也很麻烦，又难于弹性地增长，那就搞点虚拟的服务器吧，硬盘、内存都可以动态扩展（反正是虚拟的）， 访问量大的时候多用点，没啥访问量了就释放一点，按需分配，很方便，这就是云计算的一个场景。

随着时间的推移，各个公司和系统收集的数据越来越多，都堆成一座大山了，难道就放在那里白白地浪费硬盘空间吗？

有人就惊奇地发现，咦，我们利用这些数据搞点事情啊， 比如把数据好好分析一下，预测一下这个用户的购买/阅读/浏览习惯，给他推荐一点东西嘛。

可是这么多数据，用传统的方式计算好几天甚至好几个月才能出个结果，到时候黄花菜都凉了，所以也得利用分布式的技术，想办法把计算分到各个计算机去，然后再把计算结果收回来， 时势造英雄，Hadoop及其生态系统就应运而生了。

之前听说过一个大前端的概念，把移动端和网页端都归结为“前端”，我这里造个词“大后端”，把那些用户直接接触不到的、发生在服务器端的都归结进来。

# 4. 怎么学？

现在无论是前端还是后端，技术领域多如牛毛，都严重地细分了，所以我认为真正的全栈工程师根本不存在，因为一个人精力有限，不可能搞定这么多技术领域，太难了。

培训机构所说的“全栈”，我认为就是前后端还在拉拉扯扯，藕断丝连，没有彻底分离的时候的“全栈”工程师。

那么问题来了， 后端这么多东西，我该怎么学？

## Java后端学习流程

首先，我个人比较推崇的学习方法是：先学java前端，也就是HTML，css，js，因为学习java以后肯定是往java ee方向发展的，学习完前端，在学习后端很多东西比计较容易理解！

其中J2SE是关键，如果学好了java se 部分，基础扎实了，后面进阶学习也比较轻松！

补充说明一下：我觉得学习java比较合适的方法是先把所有的知识点过一遍，然后把所有的知识点串起来，边做开发边补充，就像写文章一样，先写好框架，然后再去润色填充。因为前期在学习的时候你不知道用在哪里，不知道用途，没有学习的目的，所以很多概念就很难理解，时间久了也容易遗忘。但是如果你直接从实践开始学习，很多知识点都充串联起来了，而且会印象深刻，当然前提条件是你已经入门，已经能写一些简单的程序，我个人现在也是按照这个方式在学习了，感觉很有效。

**说明：**本文介绍的内容过于详尽，这里我补充一些基本的学习路线，相对比较简略，但是比较可行：

1. 基础语法。也就是我们常说，各种编程语言都有的部分，数据类型，数组，for循环，do-while,switch……等等，是学习任何编程语言的基础，很关键；
2. 面对对象：①类和对象；②Java的三大特性（封装、继承、多态）；
3. 工具类：①异常和异常处理；②集合框架（主要是List和Map）；
4. 常用的流（stream）：①输入流；②输出流；③缓冲流；
5. 网络与线程：①Socket ； ②多线程（Thread，Runnable）；
6. 数据操作：①Mysql、Oracle; ②JDBC；
7. web基础：①Html/css；②Javascript；③JQuery；
8. 框架。

只要学会上面的前7条，基本上从前台到后台开发常见的应用还是没太大问题的，当然学习了框架以后，那就最好了，但关键还是要学好基础，说实话，像下面这个表格中所列的知识点，真正能全面掌握还是有难度的，所以凡事还是要踏踏实实的静下心学习，不要只看学习的进度，要看学习的效果。

| **第一阶段**                            | **技术名称**                                                 | **技术内容**                                                 |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **J2SE**** ****(java****基础部分****)** | java开发前奏                                                 | 计算机基本原理，Java语言发展简史以及开发环境的搭建，体验Java程序的开发，环境变量的设置，程序的执行过程，相关反编译工具介绍，java开发工具Eclipse的安装和使用，javadoc的说明。 |
| Java基础语法                            | Java语法格式，常量和变量，变量的作用域，方法和方法的重载，运算符，程序流程控制，数组和操作数组的类，对数组循环遍历以及针对数组的常用查找、排序算法原理，最后使用Java程序进行功能实现。 |                                                              |
| 面向对象编程                            | 理解对象的本质，以及面向对象，类与对象之间的关系，如何用面向对象的思想分析和解决显示生活中的问题，并java程序的手段编写出来。 如何设计类，设计类的基本原则，类的实例化过程，类元素：构造函数、this关键字、方法和方法的参数传递过程、static关键字、内部类，Java的垃圾对象回收机制。 对象的三大特性：封装、继承和多态。子类对象的实例化过程、方法的重写和重载、final关键字、抽象类、接口、继承的优点和缺点。对象的多态性：子类和父类之间的转换、父类指向子类的引用、抽象类和接口在多态中的应用、多态优点。常用设计模式如单利、模版等模式。什么是异常 异常的捕捉和抛出 异常捕捉的原则 finally的使用，package的应用 import关键字。 |                                                              |
| 多线程应用                              | 多线程的概念，如何在程序中创建多线程(Thread、Runnable)，线程安全问题，线程的同步，线程之间的通讯、死锁问题的剖析。 |                                                              |
| javaAPI详解                             | JavaAPI介绍、String和StringBuffer、各种基本数据类型包装类，System和Runtime类，Date和DateFomat类等。 常用的集合类使用如下：Java Collections Framework：Collection、Set、List、ArrayList、Vector、LinkedList、Hashset、TreeSet、Map、HashMap、TreeMap、Iterator、Enumeration等常用集合类API。 |                                                              |
| IO技术                                  | 什么是IO，File及相关类，字节流InputStream和OutputStream，字符流Reader和Writer，以及相应缓冲流和管道流，字节和字符的转化流，包装流，以及常用包装类使用，分析java的IO性能。 |                                                              |
| 网络编程                                | Java网络编程，网络通信底层协议TCP/UDP/IP，Socket编程。网络通信常用应用层协议简介：HTTP、FTP等，以及WEB服务器的工作原理。 |                                                              |
| java高级特性                            | 递归程序，Java的高级特性：反射、代理和泛型、枚举、Java正则表达式API详解及其应用。 |                                                              |

 

| **第二阶段**     | **技术名称**                                                 | **技术内容**                                                 |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **数据库技术**   | Oracle 基础管理                                              | Oracle背景简介，数据库的安装，数据库的用户名和密码，客户端登录数据库服务SQLPLUS，数据库基本概。 |
| SQL语句          | 数据库的创建，表的创建，修改，删除，查询，索引的创建，主从表的建立，数据控制授权和回收，事务控制，查询语句以及运算符的详解，sql中的函数使用。 |                                                              |
| 多表连接和子查询 | 等值和非等值连接，外连接，自连接；交叉连接，自然连接，using子句连接，完全外连接和左右外连接，子查询使用以及注意事项。 |                                                              |
| 触发器、存储过程 | 触发器和存储过程使用场合， 通过实例进行详解。                |                                                              |
| 数据库设计优化   | WHERE子句中的连接顺序，选择最有效率的表名顺序，SELECT子句中避免使用 ‘ * ‘ 计算记录条数等等。 |                                                              |
| 数据备份与移植   | 移植技巧，备份方案；导入导出等。                             |                                                              |

 

| **第三阶段**     | **技术名称**                                           | **技术内容**                                                 |
| ---------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| **jdbc****技术** | JDBC基础                                               | JDBC Connection、Statement、PreparedStatement、CallableStatement、ResultSet等不同类的使用。 |
| 连接池技术       | 了解连接池的概念，掌握连接池的建立、治理、关闭和配置。 |                                                              |
| ORM与DAO封装     | 对象关系映射思想，jdbc的dao封装，实现自己的jdbc。      |                                                              |

可以把第四阶段的知识提前一点，特别是对哪些刚开始接触面向对象编程的同学，我刚开始就学java se，感觉入门很不容易。先学web部分，有利于理解面向对象的概念，另外，web部分相对比较简单，也比较直观，写完直接就可以看见效果，有助于提升大家的学习积极性。

| **第四阶段**           | **技术名称**                                                 | **技术内容**                                                 |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| web基础技术 (项目实战) | Xml技术                                                      | 使用jdom和dom4j来对xml文档的解析和生成操作，xml 的作用和使用场合。 |
| html/css               | Java掌握基本的html标签的格式和使用，css层叠样式表对div的定义，实现对网站布局的基本实现。 |                                                              |
| Javascript             | 了解javascript的基本语法以及相关函数的使用，并结合html页面实现流程控制和页面效果展示。 什么是异常 异常的捕捉和抛出 异常捕捉的原则 finally的使用，package的应用 import关键字。 |                                                              |
| jsp/servlet            | Servlet和SP 技术、上传下载、 Tomcat 服务器技术、servlet 过滤器和监听器。 |                                                              |
| jstl和EL               | JSTL核心标签库、函数标签库、格式化标签库、自定义标签技术、EL表达式在jsp页面的使用。 |                                                              |
| ajax及框架技术         | 了解和属性原生态的ajax的使用，ajax使用的场合，使用ajax的好处，ajax框架jquery渲染页面效果和相关的强大的第三方类库，dwr如何和后台服务进行数据传输，以及页面逻辑控制等。 |                                                              |
| JSON高级应用           | Java使用json支持的方式对字符串进行封装和解析，实现页面和java后台服务的数据通信。 |                                                              |
| Fckeditor编辑器        | FCKEditor在线编辑器技术、配置、处理图片和文件上传。          |                                                              |
| javaMail技术           | 了解域名解析与MX记录、电子邮件工作原理、邮件传输协议：SMTP、POP3、IMAP、邮件组织结构：RFC822邮件格式、MIME协议、邮件编码、复合邮件结构分析、JavaMail API及其体系结构、编程创建邮件内容：简单邮件内容、包含内嵌图片的复杂邮件、包含内嵌图片和附件的复杂邮件。 |                                                              |
| JfreeChart报表         | 统计报表；图表处理。                                         |                                                              |
| BBS项目实战            | 采用Jquery+dwr+jsp+servlet+Fckeditor+JfreeChart+tomcat+jdbc(oracle) 完成BBS项目的实战。 |                                                              |
| 实战价值               | 学完此课程你至少已经是拥有近1年开发经验的程序员了，但是你不应该满足现状，下面的课程会更加吸引你！ |                                                              |

 

| **第五经典阶段**           | **技术名称**                                                 | **技术内容**                                                 |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| web主流框架技术 (项目实战) | struts2.x                                                    | struts2框架的工作原理和架构分析，struts-default.xml与default.properties文件的作用，struts。Xml中引入多个配置文件。OGNL表达式、Struts2 UI和非UI标签、输入校验、使用通配符定义action、动态方法调用、多文件上传、自定义类型转换器、为Action的属性注入值、自定义拦截器、异常处理、使用struts2实现的CRUD操作的案例。 |
| hibernate3.x               | Hibernate应用开发基础； ORM基础理论； 关系映射技术； 性能调优技术； 性能优化 一级缓存 二级缓存 查询缓存 事务与并发 悲观锁、乐观锁。 |                                                              |
| spring3.x                  | Spring IoC技术； Spring AOP技术； Spring 声明事务管理； Spring 常用功能说明，spring3.0的新特性， Spring整合struts2和hibernate3的运用。 |                                                              |
| Log4j和Junit               | Logging API； JUnit单元测试技术； 压力测试技术：badboy 进行测试计划跟踪获取以及JMeter压力测试。 |                                                              |
| 在线支付技术               | 完成支付宝的支付接口的在线支付功能。                         |                                                              |
| 电子商务网实战             | 采用spring3+hibernate3+struts2+jquery+dwr+FckEditor+tomcat 完成电子商务网站实战开发。 |                                                              |
| 实战价值                   | 项目实战价值完全高标准的高要求的迎合企业的需求，学完此课程，全部消化了，你已经就是一个地地道道的高级程序员，已经为你的职业生涯铺平了道路，你还等什么，向着高薪冲刺吧！ |                                                              |

 

| **第六进阶阶段**       | **技术名称**                                                 | **技术内容**                                                 |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| web高级进阶 (项目实战) | openJpa技术                                                  | JPA介绍及开发环境搭建、单表实体映射、一对多/多对一、一对一、多对多关联、实体继承、复合主键、JPQL语句、EntityManager API、事务管理，了解一下jpa2.0的新特性以及应用。 |
| lucene搜索引擎         | 了解全文搜索原理、全文搜索引擎、什么是OSEM、OSEM框架Compass、基于使用Lucene使用Compass实现全文增量型索引创建和搜索、探索Lucene 3.0以及API。 |                                                              |
| 电子商务网重构         | 此项目采用了Lucene+compass+openJpa+上一版电子商务网站的技术进行重构。 |                                                              |
| 实战价值               | 此项目的实战价值是前所未有的超值，已经超越了企业的实际要求，你已经是企业的抢手人才，一旦进入企业，便让你立于不败之地，轻松成为公司的技术骨干和精英，技术已经改变了你一生！ |                                                              |
| Excel/PDF文档处理技术  | java对excel和pdf文档分别利用poi和itext来进行解析和生成。此技术在企业级系统的报表中经常使用。 |                                                              |
| OA工作流技术JBPM       | 工作流是什么、JBPM介绍、JBPM的主要用法、各类节点的用法、任务各种分派方式、JBPM的整体架构原理、工作流定义模型分析、运行期工作流实例模型分析、数据库表模型分析、流程定义管理、流程实例监控、对JBPM的相关接口进行封装，构建自己的工作流应用平台等。 |                                                              |
| WebService技术         | WebService技术原理、WebService技术的应用、Soap服务的创建与管理、WSDL描述文档规范、UDDI 注册中心运行原理;使用Axis和Xfire创建WEB服务、Webservice客户端的编写、使用TCPMonitor监听SOAP协议、异构平台的整合。 |                                                              |
| Linux技术              | Linux 系统安装，卸载、linux 使用的核心思想、linux下的用户管理，文件管理,系统管理、程序的安装，使用，卸载。linux下作为server的基本应用：web服务器，j2ee服务器，ftp服务器的安装和项目的部署。 |                                                              |
| CRM项目实战            | 此项目能了解和熟悉客户关系管理的基本流程以及功能的实现，采用上面几个阶段学到的主流框架实现，同时加入了JBPM的技术。 |                                                              |
| 实战价值               | 学完这个系统会让你轻松进入企业级的大型项目的开发，倍感得心应手。完备的知识体系和最前沿的开发技术，带给你的将是在精神上不同目光的瞻望和物质上高薪资回报的喜悦，带你进入人生的新的转折点和起点！ |                                                              |

 

| **第七架构阶段**                  | **技术名称**                                                 | **技术内容**                                                 |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 大型高并发网站优化方案 (项目实战) | 如何构建一个高性能网站详解                                   | 什么样的网站需要高性能，高性能的指标体系，构建高性能网站需要做哪些工作，注意哪些细节。 |
| SSI技术                           | 什么是SSI，使用他有什么好处，什么样的系统才使用SSI，SSI技术详解和使用，应用到项目中。 |                                                              |
| 生成静态页技术                    | 什么是静态页，为什么需要静态页以及带来的好处，生成静态页的模版技术Velocity和Freemark，生成静态页的访问规则等。 |                                                              |
| 缓存技术                          | 为什么使用缓存技术，oscache缓存技术的介绍和使用，memcached缓存技术的介绍和使用、两者缓存技术的比较和如何去使用。 |                                                              |
| 经典web服务器                     | 什么是web服务器，什么是javaweb服务器，他们存在什么关系，当前技术主流中常用的web服务器有哪些， web服务器apache和nginx的应用。 |                                                              |
| nginx架构实战                     | 什么是反向代理，负载均衡以及集群，在nginx中如何实现这些高性能的系统架构。 |                                                              |
| 实战价值                          | 此课程已经将你领入了技术经理和主管以及架构师的门槛了，稍微用心学习加上实战你就是技术牛人了，薪水非常高，同时很快你就是公司的技术中层管理者，你的人生就此又一次的发生巨大的转折！ |                                                              |

如果你把上面这些东西全部掌握了，那不用说你已经算是java界比较NB的人了，因为一般能掌握这些知识的人，基本上有5-10年的工作经验，不过也不好说，说不定你就是那个天才呢，加油吧少年！

往深度挖掘，可以成为某个技术领域的专家，如搜索方面的专家、安全方面的专家，分布式文件的专家等等，不管是哪个领域，重点都不是学会使用某个工具和框架， 而是保证你可以自己的知识和技术去搞定这个领域的顶尖问题。

往广度发展，各个技术领域都要了解，对于某种需求，能够选取合适的软件和技术架构来实现它，把需求转化成合适的技术组件，让这些组件以合适的方式连接、部署、运行，这也需要持续地学习和不断的经验积累。

最后，以一张漫画来结束吧！

![img](https://upload-images.jianshu.io/upload_images/4624881-e53240201e865382?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

后端是你看不到的那条“巨龙”

（完）

我有一个微信公众号，经常会分享一些Java技术相关的干货。如果你喜欢我的分享，可以用微信搜索“Java团长”或者“javatuanzhang”关注。