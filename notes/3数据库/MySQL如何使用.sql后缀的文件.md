原因：用了一个别人的项目，他的数据库保存为.sql后缀的文件，现在要使用这个文件。

没用过SQL后缀的文件的时候，以为是压缩包，里面是数据库；通过了解才知道，这其实就是一个文本；不过复制这个文本到MySQL中就可以创建数据库。

## 1第一个问题就是这个文件怎么打开

教程：https://tech.hqew.com/news_1777645

操作：用三个方式。一是用SQL server，不过这个软件太大了；二是数据库的查询分析器；三是记事本。

如果用记事本打开，内容一般有三部分：数据库情况、创建表、插入数据；

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
-- ---------------------------
INSERT INTO `t_role` VALUES (1, '¹ÜÀíÔ±');
INSERT INTO `t_role` VALUES (2, 'ÐÅÏ¢Ô±');

SET FOREIGN_KEY_CHECKS = 1;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2如何使用这个数据库

根据数据库情况，创建数据库

Create database news;

使用数据库

Use news;

最后把sql文件的内容复制到MySQL中；MySQL自动创建；

如果想查看内容，可以使用

Show tables;//查看有哪些表；

Select * from t_role;//查看表中数据；

也可以在Navicat中查看；



## 3补充：

https://blog.csdn.net/weixin_42875245/article/details/105912850