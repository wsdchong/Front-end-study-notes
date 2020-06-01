# JavaScript笔记

## 前言：

第一部分：基础JavaScript实例、JavaScript语句、代码块、注释；

第二部分：变量条件语句、消息框、函数、循环、事件、错误处理、

第三部分：高级实例（计算器、登录表单）。

## 一、JavaScript基础

可插入HTML页面的编程代码。

输出：document.write(“<h1>page</h1>”);

对事件的反应：<button type=”button” onclick=”alert(‘welcome’)”>click</button>

修改HTML内容：x=document.getElementById(“demo”);x.innerHTML=”hello”;

改变HTML图像：<img id=”myimage” onclick=”changeimage()” src=” “>

修改HTML样式：x=document.getElementById(“demo”);x.style.color=”#ff0000”;

验证输入：if isNaN(x){alert(“on numbor”);

 

用法：放在<script>标签中；外部的JavaScript：<script src=”myscript.js”></script>

 

输出：

弹出警告框：window.alert();

将内容写入HTML文档：document.write();

写入到HTML元素中：innerHTML;

写入浏览器的控制台：console.log();

 

语法：

数字number字面量：3.14、1001、123e5

字符串string字面量：“hello”、‘hello’；

表达式字面量：5+6、5*10

数组array字面量：[10,2,3];

对象object字面量：{firstName:”amelia”,lastName:”harry”,age:50}

函数字面量：function myFuntion(a,b){return a*b;}

变量：使用关键字var定义，用=赋值。

变量是名称、字面量是值。

操作符：赋值、算数和位运算符，条件、比较及逻辑运算符。

 

语句：

分号、代码、代码块、语句标识符（for、if、var、return、function、break、try）

空格：var person=“Hege”;

对代码行进行折行：在文本字符串用\来换行

 

注释

单行用//；多行用/**/

 

变量：var firstName=”amelia”,age=22;

没赋值的值为undefined；

 

数据类型：

基本类型：字符串string、数字number、布尔Boolean（true、false）、对空null、未定义undefined、symbol

引用数据类型：对象object、数组array、函数function

 

对象：

Var car={type:“fiat”,model:500};

访问：car.type;car[“type”];

 

函数：

Function functionname（var1，var2）{}

 

作用域：可访问变量、对象、函数的集合

JavaScript函数作用域：作用域在函数内修改。

局部作用域：在函数内声明变量。

全局作用域：在函数外定义的变量，网页中所以脚本和函数均可使用。

 

事件：

 

 ##  二、JavaScript使用

条件语句：if(){}else{}

Switch(n){case 1: break;default:}

循环语句：for(var i=0;i<cars.length;i++){};

While(i<5){}

Do{}while(i<5);

 

Break和Continue

 

操作符：

Typeof操作符：用于检测变量的数据类型。Typeof null //返回object

Null操作符：只有一个值的特殊类型，表示一个空对象引用。

Undefined操作符：是一个没有设置值的变量。

 

类型转换

Number（）可以转换数字、string转换为字符串，Boolean转换为布尔值。

6种不同的数据类型、

3种对象类型

2个不含任何值的数据类型

Typeof操作符

Constructor属性返回所有JavaScript变量的构造函数

 

正则表达式：使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。搜索模式用于文本搜索和文本替换。

Var patt=/runoob/i

使用字符串办法：search和replace

 

错误

Try语句测试代码块的错误

Catch语句处理错误

Throw语句创建自定义错误

Finally语句在try和catch语句之后，无论是否触发异常，该语句都会执行。

Try{//异常的抛出}catch(e){//异常的捕获和处理}finally{结束处理}

 

调试：

按下F12，在调试菜单中选择console

设置断点

 

 

 

 

 