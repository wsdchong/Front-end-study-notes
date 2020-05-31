# springboot代码使用

前言：把《springboot+Vue全栈开发实战》跑一遍。记录跑一遍过程中遇到的问题。

[toc]

## 第一章 入门

共用三个项目。

chapter01应该是用maven工程来创建的。

chapter01-2应该是用spring initializr插件创建的。

通过file-open导入chapter01；然后就报错。我看了看IDEA的界面，看是不是maven在导入我之前没安装过的springboot。一看底部，果然，event log报了三个错。

```
Error Loading Project: Cannot load facet Spring (chapter01) Details...

Error Loading Project: Cannot load facet Web (chapter01) Details...

Features covered by IntelliJ IDEA Ultimate Spring Support, Java EE: EJB, JPA, Servlets are detected
			Try IntelliJ IDEA Ultimate
			Do not suggest Ultimate
```

前两个说我无法加载spring和web；后一个问我要不要尝试IDEA终极版（付钱版）；后一个我当然选择No，前两个我点了details，然后它问我忽略不，然后我也选择不忽略。应该和我没安装过springboot有关。

最后我等这个下载，等了十分钟，算了，我还是干干其他事。这个先等着。

