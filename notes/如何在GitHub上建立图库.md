# 如何在GitHub上建立图库

文章持续更新，最新版本请在我的GitHub上看：https://github.com/wsdchong/Front-end-study-notes
本来以为简简单单，用不着专门写一篇博客的，结果发现还有需要写一下的。
借鉴了两个教程，一个是在CSDN上的[教程](https://blog.csdn.net/int1282951082/article/details/95236240)，一个是GitHub上的用户[手册](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site).不过仅仅看这些还是不够的。

先说说他们的教程的步骤吧，

[toc]

## 借鉴的教程

1进入repositorys后新建一个存储库，命名为<user>.github.io；

2进入存储库的settings的GitHub pages设置项，把source项设置为master branch；

## 结果

第一个出问题的是在创建存储库的时候我没注意命名（要命名为用户名.github.io），这个好解决。

第二个问题的在settings里，给GitHub pages-source设置发布源。结果我没用过GitHub pages。然后节外生枝，补充[GitHub pages的学习](https://lab.github.com/githubtraining/github-pages)。

## github pages 的学习

1生成GitHub Pages 网站：设置发布源；

2自定义主页：修改index.html；

3合并拉取请求：合并（遇到问题，找不到合并的地方）

4自定义网站详细信息：（编辑配置文件已显示自己的信息）

5发一篇博客文章：创建新文件。

6添加博客文章的元数据：将yaml前件添加到博客文章以显示标题和日期

7合并第一篇文章：合并拉取请求。

弄完之后的感受就是，比起正常的git操作，就是创建存储库的时候改下命名；连设置发布源都用不着。可能我没学到家。

## 遇到的问题

我创建的存储库就是没有发布源，僵硬。

还有合并的时候不熟练，不过其实问题不大。其实挺想用GitHub for desktop来管理git的，但是延迟10分钟是真的问题大；还是得重新学学git，命令行就是比图形界面高效。——改变一下，突然发现是因为我只点了fetch origin（获取来源），没有点commint to master然后push origin的原因，才在GitHub上没刷新处理。（嘿嘿，又学到了，GitHub for desktop真香，git就不学了，懒得记）

## 收获

虽然图库依然没有成功，但是把合并操作弄熟练了，GitHub的用户手册也翻得更熟练了，GitHub Pages也有了了解。

## 转机

我之后接着搜如何用GitHub创建图床，又被我找到了一篇[教程](https://www.cnblogs.com/ly-2019/p/11828790.html)，看了看里面的内容，发现，靠谱。于是开始第二次尝试。

第一步创建GitHub图床，我都没问题

但是第二步配置picgo，我就遇到迷惑行为，我下载了picgo的GitHub，但是不是exe文件，之后看其中的readme文档，才找到[下载exe的地方](https://github.com/Molunerfinn/PicGo/releases)

b2a32042ccf657f863cce2f40cc6ed695ee9dc17

结论：还是没用，我就是建不了图床。扎心。在settings-source就是显示

> **Source**
>
> Your GitHub Pages site is currently being built from the `master` branch. [Learn more](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/).
>
> User pages must be built from the `master` branch.
>

期待以后能解决。图片的事，我就先不纠结了

https://lab.github.com/githubtraining/github-pages

