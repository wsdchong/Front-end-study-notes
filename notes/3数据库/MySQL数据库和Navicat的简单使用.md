前言：学习数据库的简单使用前

先梳理一下数据库的基础知识，这是前置内容；然后学习MySQL和Navicat的安装（工具），最后就是我要讲的简单使用。

数据库基础知识：https://blog.csdn.net/weixin_42875245/article/details/105786562

MySQL和Navicat的安装：https://blog.csdn.net/liangllhahaha/article/details/89508826



这个简单使用讲了三件事，也是三个技巧；

一是MySQL的使用：创建一个数据库，四个表，主键、外键；

二是Navicat的使用：在Navicat中写MySQL；使用可视化软件Navicat导出sql文件；用sql文件创建一个数据库；



## 一、MySQL的简单使用

Create database news；//创建数据库

Use news;//使用数据库；

Create table t_role(roleId into primary key,roleName varchar(20));//创建表t_role；

Insert into t_role values(1,’admin’);//给t_role插入数据；

Create table t_user (

userId int primary key auto_incremaent,     //设为主键，可以唯一确认元组；

username varchar(20),loginName varchar(20),password varchar(20),tel varchar(50),

registerTime datetime,  //注册时间，我有一次把date写为data，然后就是不对，扎心；

status char(1),

roleId int,foreign key (roleId) references t_role(roleId)  /插入外键，有一次我把foreign写为了foreing，检查了两次才发现。



除此之外，还有一些常出现的报错

1064：SQL语句出现问题，一般是因为不用逗号是时候用了逗号；

1056：没有定义的语句，一般是字段写错了。



还有两个常用的查看数据的语句

Show tables；//看数据库中建了几个表；

Select * from t_role;//看表里的数据；

下面那张图用了这两个查看的语句



## 二、Navicat的简单使用

### 1在Navicat中写MySQL；

在菜单栏选择工具-命令列界面；

在界面使用MySQL语句控制语句。

![img](https://img-blog.csdnimg.cn/20200504090554755.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg3NTI0NQ==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2使用可视化软件Navicat导出sql文件；

在数据库的表上（如t_role）右键，选择转储SQL文件-数据和结构，最后确认输出；

然后用记事本打开SQL文件，内容一般有三部分：数据库情况、创建表，插入数据

```
/*

 Navicat Premium Data Transfer



 Source Server         : localhost_3308

 Source Server Type    : MySQL

 Source Server Version : 50562

 Source Host           : localhost:3308

 Source Schema         : news



 Target Server Type    : MySQL

 Target Server Version : 50562

 File Encoding         : 65001



 Date: 04/05/2020 08:28:49

*/



SET NAMES utf8mb4;

SET FOREIGN_KEY_CHECKS = 0;



-- ----------------------------

-- Table structure for t_role

-- ----------------------------

DROP TABLE IF EXISTS `t_role`;

CREATE TABLE `t_role`  (

  `roleId` int(11) NOT NULL,

  `roleName` varchar(20) CHARACTER SET latin1 COLLATE latin1_swedish_ci DEFAULT NULL,

  PRIMARY KEY (`roleId`) USING BTREE

) ENGINE = InnoDB CHARACTER SET = latin1 COLLATE = latin1_swedish_ci ROW_FORMAT = Compact;



-- ----------------------------

-- Records of t_role

-- ----------------------------

INSERT INTO `t_role` VALUES (1, '¹ÜÀíÔ±');

INSERT INTO `t_role` VALUES (2, 'ÐÅÏ¢Ô±');



SET FOREIGN_KEY_CHECKS = 1;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3用sql文件创建一个数据库；

将SQL文件复制到MySQL中，就可以自动创建。