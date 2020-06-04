# mysql 存储中文显示？？，如何解决       

方法一：

改数据库编码

https://www.cnblogs.com/ditf/p/11318653.html

结果：没用，继续？？？

show variables like '%character%';

 

 

方法二：

改数据表编码。

https://jingyan.baidu.com/article/86112f13a02bf0273797879c.html

结果：有的有用，有的没用。需要保存，退出去再登进去。

 

无解

insert t_user (userName, loginName, password, status, roleId) values ('开心','kaixin','kaixin','2',1);

insert t_news (newsId,title,content,categoryId) values (73,'kaix开心','kaixin开心',2);

 

方法三：

类似方法二，在MySQL中操作

https://blog.csdn.net/tzh476/article/details/52644271

 

eclipse连接MySQL存储中文显示？？

方法一：改配置文件

https://blog.csdn.net/linshenshijianlu/article/details/78076869

结果：无用

 

方法二：修改MySQL配置文件

https://blog.csdn.net/whd526/article/details/54894559

部分有用，部分没用；5.5版本和5.7版本不一样；

set character_set_database=utf8;

set character_set_server=utf8;

set character_set_database=gbk;

set character_set_server=gbk;

set character_set_client=gbk;

set character_set_connection=gbk;

set character_set_results=gbk;

 

在Navicat中有用，在MySQL中报错；

ERROR 1366 (HY000): Incorrect string value: '\xBF\xAA\xD0\xC4' for column 'userName' at row 1

 

查看mysql的字符集：show variables where Variable_name like '%char%';

 

查看某一个数据库字符集：show create database enterprises;(注：enterprises为数据库)

 

查看某一个数据表字符集：show create table employees;(注：employees为数据表)

 

梳理过程

补充一个知识点：gbk与utf8：https://blog.csdn.net/yangfengjueqi/article/details/79486162

 

乱码表现，用Java开发出网站，在其中输入中文，但是保存到MySQL数据库中却是？？？？。

1先解决在MySQL中插入看能不能插入；

用Navicat中的操作，修改数据表的字符集为utf8；

https://jingyan.baidu.com/article/86112f13a02bf0273797879c.html

还挺有用的，在Navicat中使用终端输入的时候可以输入中文显示中文；

但是又出现两个新的问题，

第一个是在MySQL仍然不能插入，报出1366错误；

ERROR 1366 (HY000): Incorrect string value: '\xBF\xAA\xD0\xC4' for column 'userName' at row 1

第二个错误是在Navicat可以正常显示中文，但是在MySQL中不能显示。

 

2处理1366报错。

方法一：修改数据库的字符集，在直接修改my.ini。

https://www.cnblogs.com/ditf/p/11318653.html

不可行，可能和版本有关系，我的是5.5版本，教程的版本是5.7；MySQL5.5好像就是不能修改server和database的字符集。这两个的字符集一直都是Latin1;

方法二：修改数据库的字符集，在MySQL中用语句修改，修改字符集为gbk；

https://blog.csdn.net/geilivablemental/article/details/45034229

误打误撞把显示问题显示问题解决了，把utf8编码改为gbk就可以在MySQL正常显示。

同时用MySQL修改server和database的字符集后，还真的可以输入了。

虽然重启之后，这个server和database又是latin1；但是还是可以输入中文的。

然后我到Java中输入中文，看保存在MySQL是不是中文，结果还是显示？？。我估计和我之前把eclipse中的字符集设置为utf8有关。或者和之前只在控制台修改，没有在my.ini中修改有关。在控制台中修改是临时修改，不能根治。但是我的MySQL5.5就是不能修改client和mysqld的默认字符集，设置了不起作用，在显示中，server和database仍然是latin1.或许我该装MySQL5.7.

 

3eclipse动态网站项目，输入中文，保存到数据库就显示？？

创建数据库的时候把字符集设为utf8，保证前端页面编码格式也为UTF-8；

https://blog.csdn.net/weixin_43912972/article/details/96877222

无解，我在my.ini中把字符集设为utf8后，MySQL又开始乱码，所以MySQL5.5中只能设置为gbk.。故此方法仅供参考，我再去想想其他办法。

 

4MySQL5.5闪退，Navicat报出2003错误

http://blog.sina.com.cn/s/blog_a07521a00102wgou.html

我的MySQL存在C盘，所以用cd..来退出目录，最后用 cd C:\Program Files\MySQL\MySQL Server 5.5\bin 进入MySQL客户端的目录。

有效。退出后，再用client登录没有闪退了。

莫名其妙server和database设置成了gbk；

莫名其妙问题解决了，在eclipse中输入中文可以保存到数据库中，并且没有乱码。

 

出现新的问题：text类别不能显示

介绍text类别：https://blog.csdn.net/geniussnail/article/details/7753256

 

第二天又闪退，然后用第一天的方法操作，再次可行，但是每次都需要自己启动MySQL，觉得好像不能根治。并且database居然变成了latin1，

 

Mysql出现无限回车，无法执行命令；

网上说是用中文分号结尾导致的，也不知道是不是；

然后用’\c结束这个；有效。

 

接着处理text类别的问题。好难找到解决方法，难道没人遇到这个问题？

唯一的一个回答是set names utf8;

我的设置的是gbk，所以我尝试用set names gbk;试试，没用；

show full fields from t_news;

发现我的content中的text类别的collation是latin1_swedish_ci；所以我需要把这个改为utf8_general_ci。

alter table t_news change content content text character set “utf8”;

僵硬，无效，连之前有效的类别都不能插入中文了；可能和我set names utf8;有关

于是我重新把所有的都从头设置一遍。全部设置为gbk。结果解决了

这个讲解不错：https://zhidao.baidu.com/question/136633057177811405.html

完美解决

 

 

 

 