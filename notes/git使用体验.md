# git使用体验

## 前言

- 出发点：看到JavaGuide的GitHub文档，看完后发现用GitHub写存文档十分好用。在此之前我都是用Word写笔记，然后在Windows10上用文件夹和文件命名来管理笔记。
- 本部分内容为：收集、记录使用git的过程中遇到的问题，以及解决问题的答案；
- 目前已知git是一个版本控制软件；官网是https://github.com/ ；有一个控制版本软件git；有一个图形化的控制版本软件GitHub desktop；

[toc]

## 1gitbash、gitcmd、gitgui是什么？

- gitcmd：命令行提示符。当你在Windows上安装git并且习惯使用命令行时，可以使用cmd来运行git命令；

- gitbash：命令行工具，一个shell。基于cmd，在cmd的基础上添加了一些新的命令与功能。与cmd相比，bash更加方便；

- gitgui：图形用户界面。提供一个图形用户界面来运行git命令。


## 2gitgui与GitHub for desktop的关系？常用的GUI git客户端有哪些？

gitgui有两种意思，一种是git自带的gitgui，一种是git的图形用户界面。

GitHub for desktop是git的一种专门开发的图形用户界面软件，功能完善，使用方便。与gitgui相比，更美观好用。

git GUI除了GitHub for desktop外，还有两种常用的独立客户端工具。如source tree（老牌git gui管理工具）、tortoisegit（小乌龟）。还有IDE集成的git客户端，如eclipse的Egit、vs的git integration和GitHub extension、vscode

其他的我没怎么使用，目前暂时以GitHub for desktop为主。

## 3github上的license-许可证是什么？

开源许可证可以保护贡献者和用户。正是有这开源许可证，才促使企业和开发人员开源。下面是阮一峰大神在2011年5月发表的一篇博客里的图，清晰明了地介绍了几种主流的许可证。

![alt text](notes\bg2011050101.png)

我在这还重点介绍两种

[MIT许可证](https://choosealicense.com/licenses/mit/#suggest-this-license)：简短而简单的许可证，只需要保留版权和许可声明就可以自由使用。

[GNU Affero许可证](https://choosealicense.com/licenses/agpl-3.0/)：要求较多的许可证。

也不是特别懂，反正我这GitHub上保留学习笔记只是为了方便可以换一台电脑任然可以翻阅。我选择先用MIT许可证试试。

## 4我创建和使用一个front-end study notes库的过程

1. 在GitHub上，点击 start a program，填写库名；
2. 经过比较选择MIT许可证，.gitignore选择none，然后点击创建存储库repository；
3. 进入到库中，看到有readme.md和license；随后我乱点点点，创建了一个文件和自动化；

## 5使用git的经验 

发现了两种学习使用git的方法。

- 一种是根据我无意间发现的[GitHub帮助](https://help.github.com/en/github)来学习，里面的文档真的是应有尽有。是git的全部说明书。有什么搞不懂的就可以在里面看。
- 一种是在git官网的页面中分析结构，把每一个都点一次，也差不多理解有什么内容。

目前我接触的应该是三大块。

- 用户设置：在用户设置里设置，有用户的信息
- git仓库的使用：code（主页、存储库、自述文件）、issues（问题）、pull requests（记录其他贡献者的贡献）、actions（设置工作流程）、projects（管理项目的设置）、wiki、security（安全）、insights（记录贡献者等）、settings（设置仓库的设置）
- git社区：pull requests、issues、marketplace、explore；

## 6使用GitHub for desktop的经验

1. 选择和进入我之前创建的存储库front-end study notes；

2. 在GitHub for desktop的主界面中，有常规的六个工具栏：file、edit、view、repository、branch、help；

3. 在工具栏中，有current repository、current branch、fetch origin；再下面，左边是changes和history，右边是有三个选项操作（open in vscode、show in explorer、view on github）

4. 我选择的是show in explore。在文件夹中我把之前写的文件放入其中，然后点击fetch origin，就实现了文档上传。优秀，舒服。不过有些延迟，得十分钟才能在GitHub上看到自己上传的东西。

## 7出现新的问题

在typora中自动生成目录的[toc]到GitHub上不显示目录，而是显示这个这个符号，愁。为什么呢，在Javaguide上为什么可以自动生成目录？

还有就是在本地用typora编辑markdown文档，使用的是本地，到了GitHub上就不显示了。

然后我就去看Javaguide，看完之后，我发现Javaguide上是直接写的目录，怪不得。借鉴这个Javaguide，我发现他的目录用[前言](#前言)来实现。图片直接把存储库当做根目录，之前我是用电脑桌面为根目录。

然后我试了试文档跳转，发现typora好像不能像图片引用那样使用存储库为根目录，但是Javaguide中却可以，看了看帮助文档，说是兼容性的问题。迷。

其他文档用[typora使用体验](/notes/typora使用体验.md)来实现

## 8最后摸索一下readme（参照Javaguide与Javainterview）

他们的大体结构是：前言-目录-正文-说明。共四部分。

前言：引用和log；

目录：本文中的链接

正文：链接到其他文档

说明：介绍、关于转载、投稿、联系方式、contributor、公众号