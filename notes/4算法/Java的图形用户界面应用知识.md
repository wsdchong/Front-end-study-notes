两个部分：一是理论、二是实践；

这里的Java讲解来源于2010年之前，之后的改变看官网。

Java的基本使用：https://blog.csdn.net/weixin_42875245/article/details/105939720

Java应用基础：https://blog.csdn.net/weixin_42875245/article/details/105939796

Java面向对象基础：https://blog.csdn.net/weixin_42875245/article/details/105939837

## 一、设计原则

1使用图形界面DUI。字符界面采用命令行方式与用户交互；图形界面采用多媒体显示信息，用直观方便的GUI标准组件来接收命令；

2界面构成：容器、标准组件、自定义组件。

容器是用来组织其他界面成分和元素的单位；组件是图形用户界面的基本单位；自定义成分不能被系统识别，只起装饰作用，如文字、图像；

3使用组件的步骤

创建组件类的对象，指定其大小等属性；使用布局策略，确定组件对象在容器里的位置；将该组件对象注册给它所能产生的事件对应的事件监听者，重载事件处理方法，实现利用该组件对象与用户交互的功能。

严格来说，容器也是一种组件，因为容器也可以被视为组件包含在其他容器内容。



## 二、容器与布局

1AWT包（abstract Windows toolkit）

抽象窗口工具提供基本GUI标准组件：选择类组件（复选框）、文字处理类组件（文本框）、命令类组件（按钮、菜单）

2component类

可现实在屏幕上的图形对象，可与用户交互。

Containers容器组件：window（frame、dialog）、panel

3容器的组件布局

依靠布局管理器，例如setLayout(new FlowLayout());还有BorderLayout、GridLayout、CardLayout。



## 三、接口interface

接口定义的仅仅是实现某一特定功能的一组方法的对外接口和规范，而并没有真正地实现这个功能。通常把对接口的继承称为实现。

实现的方法必须指定为public；

实现接口的类要实现接口的全部方法。如果不需要某个方法，也要定义一个空方法体的方法；

利用接口模拟多继承；只说明对象的编程接口，不用揭示实际的类体。



## 四、事件处理

用户操作GUI组件时会引发各种事件。事件、事件源、事件处理程序、监听者

每个事件有一个对应的监听者接口，规定能够接受（处理）该类事件的方法的规范。

actionEvent-actionListener-监听者类-addActionListener

1窗口事件：

关闭窗口框引发windowEvent事件，定义windowListener

2actionEvent

3标准组件：

label、button、textField、CheckBox、CheckBoxGroup、TextArea、list、choice

4菜单menuBar、menu、menultem

5文本对话框fileDialog：parent、title、mode

6绘制自定义成分：graphics、paint、repaint

7font类

8color类



## 五、编程

https://blog.csdn.net/weixin_42875245/article/details/105939271

运行application好像没成功，然后改为用applet，然后成功了。





总结：梳理一下图形用户界面的设计与实现。然后做一个计算器。

下一阶段，梳理一下线程与多线程，顺便补充一下异常处理，最后写一个用到多线程的计时器。