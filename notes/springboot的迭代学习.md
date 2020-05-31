# springboot的迭代学习

时效性：2019年1月第一次出版，使用版本springboot2.0.4版本

## 前言

把springboot当作主板，把mybatis、springmvc、spring security、Redis、actionMQ当作组件，把这些统一到springboot上。

springboot的前置知识是Java、设计模式、反射、注解以及spring；

mybatis的前置知识是数据库系统概论、mysql、Navicat（非必须）；

springmvc的前置知识是servlet、HTML、CSS、JavaScript、HTTP、jsp、Tomcat；

spring security的前置知识（我也不太懂，但先用着）是加密；

Redis主要靠理解，没特别重要的前置知识，是一个key-value数据库；

actionMQ的前置知识的Java massage service；

当然除了这些，还有一些如maven包括在springboot开发中，如thymeleaf、MongoDB、devtools、websocket等被整合到springboot中；还有一些git、docket、IDEA使用等的知识包括其中，等后期补入。

我的学习方法是先把这些内容跑一遍，熟能生巧；最后再把这些代码敲一遍，查漏补缺；最后从这两步中总结体验，算是入门；

[toc]

## 内容

1springboot入门：创建maven工程、项目构建、项目启动

2基础配置：

 

3整合视图层技术：整合thymeleaf、freemarker

4整合web开发：整合springmvc（json、路径映射、filter、listener）

5整合持久层技术：整合mybatis

 

6整合nosql：整合Redis、MongoDB；

7构建RESTful服务

8开发者工具与单元测试：devtools

 

9缓存：Redis单机缓存、集群缓存

10安全管理：spring security、shiro

11整合websocket

12消息服务：JMS

13企业开发：邮件

 

14应用监控：端点配置、监控信息可视化

15项目构建与部署：jar、war

 

16微人事项目实战：主要使用到mybatis、spring security、Redis、mail+thymeleaf、websocker、打包；

用到了1,2,3,5,6,9,10,11,13,15

没用：3,7,8,12,14

 

前置知识：spring、数据库、IDEA的使用。

## 跑一遍1-8



