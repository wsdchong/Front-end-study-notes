# Docker使用体验

前言：今天看JavaGuide的文章，看到一篇文章名叫[一文搞懂 Docker 镜像的常用操作！](https://github.com/Snailclimb/JavaGuide/blob/master/docs/tools/Docker-Image.md)

凑巧最近我想了解docker的使用，于是就决定试一试。其实在此之前我就久仰docker的大名，甚至买了一本《Docker技术入门与实战（第3版）》的书。

理论部分我就不多赘述了，都在上面那本书里。下面讲我在使用Docker的过程 中遇到了那些坑。好期待。

[toc]

## Docker Desktop的使用

1注册docker hub账号。打开 Docker Hub 网址 https://hub.docker.com，开始注册。填写账号、密码和邮箱；邮箱确认；

2下载和安装Docker Desktop。安装包有390M，我花了十几分钟才下好。然后我安装的时候遇到一个坑——安装完毕显示restart，我以为是这个软件的重启，结果是电脑系统的重启，当时我这笔记恰好没保存。于是重启之后又重新写到这里。

3创建镜像仓库。在docker hub上创建，填写仓库名、描述信息、公共仓库；其中仓库名必须小写，并且不能有空格。

4克隆仓库。跟着docker desktop的新手教程来。

```
git clone https://github.com/docker/getting-started.git
```

然后docker desktop就把这个下载了。

5建立镜像。

```
docker build -t docker101tutorial .Next Step
```

然后docker desktop就建好镜像了。这个好舒服。

6运行容器

```
docker run -d -p 80:80 \  --name docker-tutorial docker101tutorialNext Step
```

7保存和分享镜像

```
docker tag docker101tutorial {userName}/docker101tutorialdocker push {userName}/docker101tutorialDone
```

