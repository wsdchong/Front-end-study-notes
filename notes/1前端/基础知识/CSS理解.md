# 本质

全称为层叠样式表（cascading style sheets）。属于修饰HTML文件的语言。如果把HTML比作成word文档的基本内容，CSS就是修饰word的设计和布局部分，使基本的文档样式更多，布局更好。

# 核心

CSS的使用方式（三种）：外部样式表（在head标签中用<link rel="stylesheet" type="text/css" href="mystyle.css">)、内部样式表（在head标签中用style标签）、内联样式（在标签里用style属性）。外部样式表的优越性是可以在多个HTML文件中使用样式，内部样式表的优越性是可以在特定HTML文件中使用样式，内联样式可以在特定HTML标签中使用样式。

选择器概念：选择器（HTML中的标签，id，class）{属性：值；属性：值；}。其中标签选择器可以指定HTML一组元素的样式；id选择器可以指定一组HTML元素中标记id的元素的样式；class选择器可以描述一组元素的样式，可以在多个元素中使用。

盒子模型的概念：CSS盒模型包装HTML元素，它包括：margin（外边框，没颜色）、outline（轮廓，在边框边缘，有颜色）border（边框）、padding（填充）、content（实际内容）

定位的概念：position属性（static默认、relative相对、fixed固定、absolute绝对定位、sticky粘性）

处理溢出内容的概念：overflow属性（visible默认、hidden其他内容不可见、scroll滑动可见、auto、inherit）

# 基本内容

对应HTML基本内容，也有五种。

处理文字：字体fonts、文本text、背景background；

处理列表：list-style-type属性（circle、square、url、none）可以丰富列表前的标签。

处理表格：用盒子模型（border、padding）、color、text-align等。

处理表单：同处理文字、处理表格类似，用盒子模型、文本处理。

处理链接：link（未访问）、visited（已访问）、hover（移动到链接上）、active（点击）