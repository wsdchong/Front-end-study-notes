时间：2020/4/21

前言：课件笔记、JSP的缺点

笔记来源：老师的课件

## 一、课件笔记

1JSP（Java server pages）是一种用于开发动态网页的技术，文件后缀名是.jsp

在JSP页面中可以嵌套Java代码，为用户提供动态数据。

Servlet很难对数据进行排版，而JSP除了可以用Java代码产生动态数据的同时，还可以对数据进行排版。

2JSP表达式：<%= 变量或表达式 %>；out.print()将数据输给客户端；后面不能用分号。

3JSP脚本片段：<% Java代码 %>;脚本片段中只能出现Java代码，多个脚本片段组合后的结果一定是完整的Java语言

4JSP注释：<%- -%>

5JSP指令：page指令、include指令、taglib指令；语法格式为<%@ 指令 属性名=“值” %>

Page指令：

Include指令：用于引入其他JSP页面，JSP引擎会把这些JSP翻译成servlet；

Taglib指令：用于在JSP页面中导入标签库

6JSP九大隐式对象：exception、page、request、espouse、config、application、session、out、pageContext。

7JSP标签：<jsp:include>\<jsp:forward>\<jsp:param>

8映射JSP

## 二、JSP的缺点

简单来说，JSP就是在HTML页面中写一些Java代码；

缺点：

1动态和静态资源放在一起，一旦服务器出问题，前后台一起玩完，用户体验差；

2JSP一旦出现问题，需要前后端开发人员一块解决，效率低；

3JSP不能使用Nginx