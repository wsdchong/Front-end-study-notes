# 前言

HTML真的是网页的基础，CSS，JavaScript都是为了丰富它的功能。而HTML的内容也十分明确，就像写笔记一样。基本内容有标题、段落、文本格式化、链接、图像、表格、列表（无序列表、有序列表、定义列表）、表单。剩下就是修饰内容，有布局（样式/区块）、框架、颜色。

# 速查列表

菜鸟教程的链接：https://www.runoob.com/html/html-quicklist.html

# 学以致用

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>HTML使用</title>
	</head>
	<body>
		<h1>HTML使用</h1>
		<h3>前言</h3>
		<p>看看就使用HTML可以达到什么效果，在这其中尽量多的应用各个元素。</p>
		<h3>元素使用和速查</h3>
		<p>标题h1、段落p、换行br、水平线hr、链接、两种列表ul+li、表格table和表单form、文本格式化</p>
		<p>其中标题、段落、换行就不多赘述了。</p>
		
		<h3>一、文本格式化</h3>
		<p>最常用的有</p>
		<b>粗体b、</b><i>斜体i、</i><ins>下划线ins</ins>
		<del>删除del、</del><sup>上标sup</sup><sub>下标sub.</sub>
		
		<h3>二、两种列表</h3>
		<ul>
			<li>无序列表ul+li</li>
		</ul>
		<ol>
			<li>有序列表ol+li</li>
		</ol>
		<p>列表还可以通过CSS的修饰成为导航栏</p>
		
		<h3>三、表格</h3>
		<table border="1" cellspacing="" cellpadding="">
			<tr><th>Header</th><th>表格table+tr+th</th></tr>
			<tr><td>Data</td><td>表格table+tr+td</td></tr>
		</table>
		
		<h3>四、表单</h3>
		<form>
			<input type="color" value="颜色" />
			<input type="date" value="年月日数据" />
			<input type="datetime-local" value="时分数据" /><br>
			<input type="email" value="email" />
			<input type="file"value="选择文件file" />
			<input type="search"value="搜索search" /><br />
			<input type="text"value="文本框text" />
			<input type="password"value="密码password" />
			<input type="submit" value="发送submit"/><br>
			<select>
				<option>固定选项</option>
				<option selected="selected">固定选项select+option</option>
			</select>
			<input type="checkbox" value="勾选checkbox"/>
			<input type="radio"value="复选框" />
			<input type="button" value="按钮button"/>
		</form>
		<p>常用于注册和登录页面</p>
		
		<h3>五、链接</h3>
		<a href="https://mp.csdn.net/"><img src="img/csdn.png"width="40px"height="40px"></a>
		<a href="https://mp.csdn.net/">文字链接</a>
		
	</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 最终效果

![img](https://img-blog.csdnimg.cn/20200311092223803.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg3NTI0NQ==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)