# Git bash的尝试

## 前言

其实在大二暑假学《第一行代码Android（第2版）》的时候，在第五章和第十四章学过git bash。不过之后没怎么使用。最近用git的时候不太想用git bash，还要记忆指令，于是学了GitHub for DeskTop（git的图形化界面），这个图形化界面操作简便，而且满足需求。

不过闲着也是闲着，还是了解一下git bash；下面就记录一下我这次用git bash的过程。

参考书：《第一行代码Android（第2版）》的第五章和第十四章、《Vue.js从入门到项目实战》的附录A、[git的官方帮助文档](https://help.github.com/cn/github/using-git)

[toc]

## GitHub for desktop用到的内容

之前使用过GitHub for desktop。用过的功能有

1设置本地地址。在GitHub上创建git仓库，用GitHub for desktop在本地设置本地仓库；

2提交。commit to master后push就提交了。仓库修改，在changes中会自己显示（这个功能超好用）。

写这部分是为了参照，确定一个方向，使自己使用git bash的时候能有个具体要实现的功能。

## git常用命令

《Vue.js从入门到项目实战》的附录A。有删减，像什么回退项目版本，我目前没用到过就没去滥竽充数，等以后需要的时候再去补充。git的使用满足刚需即可。结合官网的[使用常用git命令](https://help.github.com/cn/github/using-git/using-common-git-commands)，我还做了补充。

```
# 克隆远程仓库。
git clone
#从远程仓库获取更改
git fetch
#合并更改到本地分支
git merge
#从远程仓库拉取合并，是fetch与merge的结合。
git pull
#推送提交到远程仓库
git push
```

感受：《Vue.js从入门到项目实战》的附录A的确有些宽泛。具体使用还得依据官网来了解细节（不过官网细节太多了，有些找不到北）。像上面创建文件、初始化仓库我就不写了，那些不是直接在本地仓库进行操作吗，到时候push的时候就有了。

由于我现在用git是一个人使用，所以有许多协调工作的部分，我都没使用，或者说没必要用。如：

1从远程仓库获取更改。（用到的命令有git clone、git merge和git fetch）。但是远程仓库就我一个人修改，也就是说远程仓库有的我本地都有，我本地有的（还没有上传的）远程仓库没有。故我去看有没有更新完全没必要，除非多人修改，远程仓库里才有我本地没有的。

2推送提交到远程仓库。（用到的命令用git push origin master）。一样，远程仓库就我一个人提交，所以我就以master的身份提交。不想多人协作那样，每个人有每个人的分支，提交上去后，master再拉取合并。

3回退版本。我更新版本都是最新版本，不用回退。哈哈哈哈哈哈。



## git bash实现的内容

《第一行代码Android（第2版）》的第五章和第十四章。这本书写的特别好。媲美官网，但比官网精简。

创建（或clone）代码仓库&提交本地代码

> #第一步 配置身份
>
> git config --global user.name "用户名"
>
> git config --global user.email "用户邮箱" 
>
> #第二步 找到本地仓库
>
> cd c:
>
> cd Users/Administrator/Documents/GitHub/test001
>
> #第三步 新建仓库用git init；克隆仓库用 git clone 地址
>
> git init
>
> #第四步查看本地项目中进行的所有git操作（项目根目录下.git文件夹中记录的）
>
> ls -al
>
> #第五步 提交本地代码
>
> git commit -a
>
> #第六步 更新远程仓库
>
> git push origin master

有趣的是我进行提交本地代码的时候，显示unable，说SSL连接被重置为443

我突然想起我在官网帮助文档中看到[为什么 Git 总是询问我的密码？](https://help.github.com/cn/github/using-git/why-is-git-always-asking-for-my-password)

我觉得可能和这个有关。

## 结论

还是用GitHub for Desktop香。git bash了解即可。

以后如果工作中要用到git bash，我就看[git的官方帮助文档](https://help.github.com/cn/github/using-git)进行知识补充。

不过现在用GitHub for Desktop已经能满足我的需求了。



我之前写过的[git使用体验——wsdchong](https://blog.csdn.net/weixin_42875245/article/details/106460605)，有我使用GitHub for desktop的学习经验。大家可以参考一下。



本人才疏学浅，许多内容请辩证理解。后期会不断更新。

更新地址：[Vue的基础知识](https://github.com/wsdchong/Front-end-study-notes/blob/master/road/Vue/Vue的基本知识.md)

更多内容请关注：[CSDN](https://blog.csdn.net/weixin_42875245)、[GitHub](https://github.com/wsdchong/Front-end-study-notes)