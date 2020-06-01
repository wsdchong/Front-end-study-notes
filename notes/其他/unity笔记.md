# unity笔记

计算机的发展：1945-1978（计算）、1978-1992（单机）、1992-2008（互联）、2008移动

游戏的发展：单机—网络；2D—3D；

网络游戏编程：

服务端：网络编程、人工智能、数据库、信息安全

客户端：2D游戏编程、3D游戏编程、美工设计、音乐设计

其他必要流程：游戏剧本策划、游戏项目管理、文档编辑等

DirectX的优势：功能丰富的底层API、比OpenGL应用更广、比unity更底层，功能扩展更强。

Unity3d的优势：开源、成熟、容易入手

Unity游戏开发流程：策划（分析、设计）—>美工（素材收集）—>编程（组装）；

功能：通过五个视图scene、game、hierarchy（层次）、project、inspector处理素材和脚本；常用功能有：刚体、碰撞体、协程、GUI、shade；

用game object在hierarchy创建和使用资源

用asset在Project导入资源

用Component创建组件，和用inspector查看资源属性

用scene和game显示资源；

资源包括camera、light、物体；

组件有位置、刚体、碰撞器、材质、脚本。 

 

## 一、unity5.0介绍

2015年unity官方在GDC发布5.0；免费提供了4.0专业版所有的游戏引擎功能以及各个平台的发布权；增加了新的功能（unity3d.com/cn）

图形处理技术（图像处理引擎）：shade、全新的动态全局光照系统、反射探头

云构建（could build）：版本控制（远程的安装和测试）、产品分析

灵活编辑器：混音（audio mixer）

跨平台性：21个平台

（WebGL实现网页游戏）（IL2CPP提高C#性能）

 

## 二、界面

Scene场景：QWER控制选择平移旋转、缩放；右键+WSAD旋转视图；

Game游戏：播放暂停；显示长宽比；游戏全屏显示；

hierarchy层次：搜索菜单

project资源：视图、模型、脚本、shade

inspector属性

 

七个菜单

File：场景、项目、发布

Edit：界面设置preference

Asset资源：控制project的资源。如导入包、导出包

Game Object：给hierarchy添加物体。如光、摄像机

Component组件：给inspector添加组件。如mash物体模型和贴图、effect粒子特效、物理组件、导航组件、声音组件、渲染组件、脚本组件

Window：调整窗口。如animation窗口（微调动画）、animator窗口、光照窗口、寻路系统、报错窗口；

Help：管理证书、收看官网、欢迎菜单（有教程、资源）

 

场景漫游

QWER；物体轴心、权重轴心；2D；光照；声音；effect；搜索；广角视图和世界视图；

 

场景搭配（Game Object和hierarchy）

基本组件： camera（inspector的death控制深度）

灯光组件：平行光（阴影、光晕设置）、点光（范围）、聚光灯、区域光

物体组件：立方体（位置、渲染、碰撞体、脚本）、材质、、球体、圆柱体、胶囊体、平面、方框；

精灵sprite组件：模拟背景，实现2D动画效果

地形Terrible组件：在terrain添加贴图、山峰、平面、树木、草地、设置

 

项目资源类型（Asset和project）

十一种：文件夹、脚本、shader、prefab、材质、立方体贴图（天空盒）、镜头光晕、animator

Fbx模型

模型、骨骼、材质、贴图、动画

贴图材质与着色器

材质由贴图和shader组成；

Texture贴图：2D（界面UI、Mesh模型、粒子效果）、movie（视频资源）、render渲染（摄像机）

 

游戏组件Component和inspector

窗口操作：

检视面板用途：setting项目配置属性、game object游戏物体编辑、asset资源文件编辑

编辑：添加图标标注、是否静态、标注tag、控制可见layer；

设置和介绍：设置reset（默认）、复制、添加与删除组件

物理类型组件、效果类型组件、脚本：

Trail render设置效果

脚本：可拖拽可添加脚本组件、点击问号了解脚本；

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)物体与组件总结

 

## 三、脚本（知识准备和专题课程）

C#语言基础

基本语法：数据类型、逻辑语句、函数结构、引用类型、类型转换

面向对象：封装、继承、多态

设计模式：单例模式、监听者模式、状态机模式

脚本编程（依托物体展现）

基础部分：生命周期、事件对应、常用方法、图形用户界面

进阶：计算机几何、测试、优化

 

脚本

调试脚本：Console窗口查看报错、start（用Debug.LogError）、update

脚本生命周期：Awake（创建变量）、start（给变量赋值）、update（每一帧调用一次，用于非物体）（fixed update常用于物体碰撞）、rendering、GUI、on destroy；

Mono Behavior的响应事件函数massage：启动（awake、start）、刷新（update）、交互函数（物理、输入、渲染、对象、场景、程序、网络、动画、声音）

组件访问：创建物体rigid body、引用组件game object、add component；awake、enable、start

场景变换：transform、position、rotation、scale、hierarchy

位移：变量posltion = new Vector3；函数方法Translate()

旋转：变量rotation = new quaternion；函数方法Rotate()

缩放：变量localscale=new Vector3；

位置：变量root；函数方法find（）

Random随机数、mathf数学运算；

3D数学基础：向量、运算、三维空间的向量运算

脚本的输入与控制、object体系结构、destory物体的销毁、sendmessage消息的推送、coroutine协同执行程序

界面

 

## 四、着色器和其他

动画系统：内置动画状态机系统、人物动画重定向

模型创建（建模、骨骼、蒙皮）导入、配置

 

粒子系统（依托物体）

界面

初始化模块initial module：lifetime、color

发射模块emission module：发射速率、粒子爆发

 

渲染（输出）

模型<—材质<—贴图+shader：着色器实际上是一小段程序。它负责将输入的顶点数据以指定的方式和输入的贴图或颜色组合起来，然后输出。材质好比商品，shader好比加工，贴图好比原材料。

Shader：一种可编程图形管线的算法片段。用于告诉图形硬件如何计算和输出图形，过去由汇编语言来编写。主要分为Vertex（顶点）Shader和Fragment （片段）shader。

渲染管线：一种计算机从数据到最终图形成像的形象描述。

顶点处理（本地坐标系![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image003.png)-世界

坐标系）：计算颜色、坐标变换

 

面处理：面组装、截取、剔除

 

光栅化：将以向量为基本结构

的面转化为点阵式的像素

 

像素处理（片段着色器）

 

Shader language：主要有三种语言，基于OpenGL的GLSL，基于DirectX的HLSL，以及NVIDIA公司的Cg语言。

GPU（graphic processing unit）图形处理器简史：七十年代为初GPU、1998为中等GPU（2001年研发出顶点编辑能力，2003年研发出片段编辑能力可编辑像素级；

 

Unity shader 跟渲染流水线的 shader 有很大的不同。

Unity 的 shader 能够以以下三种方式编写：

作为 surface shader

作为 vertex and fragment shader

作为 fixed function shader

不管采用哪种方式写 shader, 都需要使用 ShaderLab 语言来组织 shader 结构。所以我们先要了解 ShaderLab.

 

Shaderlab基本结构：

Shader“name“{

[properties]//属性

Subshaders//列表

[fallback]//自定义编辑器声明

}

Physical based shader：基础图片albedo、反光specular、表面粗糙roughness、normal法线贴图、（fresnel折射）（环境光照ambient、漫反射diffuse）

三个常用shader：顶点着色器、漫反射、（含高光、漫反射和环境光的凹凸纹理映射）

