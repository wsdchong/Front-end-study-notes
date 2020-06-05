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

感受：《Vue.js从入门到项目实战》的附录A的确有些宽泛。具体使用还得依据官网来了解细节（不过官网细节太多了，有些找不到北）。上面的



## git bash实现的内容



