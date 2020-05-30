# eclipse如何发布网站？

前言：之前做毕业设计的时候做了一个网站，数据库用mysql5.5，服务器用eclipse开发，后端用到SSM框架，前端用bootstrap框架。在自己的电脑上可以运转正常。

然后现在我想把这个打包发布到网站上。对了，我还有一个百度的百度云主机和一个已通过审核的域名。去年还买了一个三个月的云服务器，但是平时不怎么用，就干脆没续费了。

猜想：我估计有两种发布方式。第一种是云服务器，这个我比较熟悉，就是在云服务器（Windows或Linux）上搭建环境（数据库和服务器），然后把数据库和后端代码运行在服务器上，这就可以了；第二种是云主机，我猜是把数据库弄到PHPMyadmin上，服务器的话靠eclipse导出的jar，然后用FTP上传到服务器，这样应该可以；其实还有一种就是docker，把网站打包，然后在任何一个平台都可以运行（没试过，脑海中猜的）；

计划：通过百度和谷歌，借鉴博客和官网的资料。书的话，暂时不考虑。

[toc]

## 方法一：打包成war包，发布到Tomcat

#### 百度一下：eclipse如何发布网站？

然后给出了诸如eclipse开发好的web项目部署到服务器Tomcat的回答。还好有个打包、部署、发布的教程。

有个回答是1用eclipse用file-export出war包；2把包放到Tomcat的webapp下，启动Tomcat即可。

第一步：file-export打包出war包

屁，我还以为一直点next就可以了，点开export后需要点web-war file；然后按默认导出；

接着我打开这个包，我发现里面只包括webcontent里的文件，那些src目录里的代码没在里面，这样发布到Tomcat会不会不能用。管它了，开始下一步；虽然通过web.xml或者其他设置一下，应该可以把src中的代码打包出来，但是先将错就错，看会发生什么。

第二步：把包放到Tomcat的webapp中，然后启动Tomcat，试试。

细节不太确定，百度一下，[Eclipse开发好的Web项目如何部署到服务器的Tomcat上？](https://blog.csdn.net/weixin_40327259/article/details/80467049),根据步骤，把包放到webaps中。

然后运行一下Tomcat：我在bin点击Tomcat7.exe，然后没用，接着我点tomcat7w.exe，然后弹出“指定的服务未安装”，

#### 百度了一下：[启动tomcat7w.exe提示"指定的服务未安装“](https://jingyan.baidu.com/article/647f0115e85cb07f2148a8b7.html)

接着按照教程试了试。然后我成功了，但是启动Tomcat后，我不知道用什么网址来访问我的网站。还好之前用eclipse运行Tomcat的时候，复制过网址在谷歌浏览器。我在历史记录里找到打开（http://localhost:8080/news_publish/index.action），发现居然可以。神奇。存储数据库都不受影响。那个打包出的war包，明明没有src中的代码。

不，我重新看了看webapps文件夹，发现里面解压了我的war包。在web-if里出现了一个classes文件夹，打开一看，果然，src目录下的代码都在这。interest。

没想到今天的尝试这么顺利。但是我想用我的域名来绑定到这个服务器，或者把这个发布到云主机里，然后把域名绑定上去。具体怎么操控肯定比较不容易。

### 百度一下：[tomcat发布项目绑定域名总结](https://blog.csdn.net/kongnan93/article/details/50461810)

第一步是查自己电脑的IP，自己在电脑上搜一下就知道。

第二步是把IP绑到我的域名上；

第三步是在Tomcat的conf文件夹中编辑server.xml文件。

把8080端口改为80端口，修改host的name，增加<context>；

第四步是用域名解析解析到这个服务器。

这样就可以通过域名来访问这个网址项目。我按照这个操作后，首先stop这个Tomcat7w，然后start，结果没有start了。然后我把<context>删除，发现可以start，但是输入地址，我尝试改localhost为域名，后面加上80端口；

没办法，我又修改回去。再想想其他办法。

唯一有用的是把8080改为80后，的确在URL中不用写端口号了。后面那个配host的没起作用。我再找找其他的教程对比一下。看是版本问题吗。

[Tomcat中部署网站和绑定域名](https://blog.csdn.net/lduzhenlin/article/details/91344822)，参考这个我在同级加一个host。然后，虽然Tomcat7w.exe可以start，但是输入域名还是不能跑到网站上。

[tomcat绑定域名](https://blog.csdn.net/weixin_43466575/article/details/89672712?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)，我参考了一下，发现如果同级添加host，则localhost任然可以，但是域名还是不可用，我想会不会是我绑定出了问题。或者host应该只有一个，亦或者有东西设置优先级。

哎，今天暂时这样，来日方长



