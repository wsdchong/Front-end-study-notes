# vue项目之启动项目

## 前言：

[vue的基本知识](https://blog.csdn.net/weixin_42875245/article/details/106558173) 重点讲述《vue.js从入门到项目实战》的第一章到第四章

[vue项目化](https://blog.csdn.net/weixin_42875245/article/details/106698109) 重点讲述《vue.js从入门到项目实战》的第六章

接下来就是对第八章的启动了。

[toc]

## 一、理论内容

打造一个线上商城。首页、详情页、购物车、订单四个页面。购物车和订单页面的动态就没展示了。

### 页面设计

首页设计：顶部banner有搜索框、购物车和订单的跳转链接等，是各个页面所共有的；中部banner有导航；底部有几件商品的超链接；

详情页设计：左侧banner是商品的详情图、右侧banner是商品的购物；

购物车设计：表格设置商品；

订单设计：和购物车设计类似，表格设置订单；

### 目录结构设计

#### 初始目录

build：开发和生产版本的构建脚本；

config：开发和生产版本的部分构建配置；

dist：由npm run build生成；项目的生产版本，只有HTML、CSS、JavaScript和静态资源；

src：项目开发的关键资源目录和主要工作空间；

.gitignore：应该被git版本控制工具忽略的文件；

index.html：应该被webpack注入资源的模板HTML文件；

#### src目录结构

asset：存放样式表和图片；

components：存放vue的单文件模板。目录下的index.vue、Goods.vue、Cart.vue、Order.vue分别对应首页、购物页、购物车、订单；

config：存放配置项，如商品信息及商品细分类目的导航；

router：路由；

widgets：存放自定义组件，自定义了复选框和跑马灯；

App.vue：项目的根目录

main.js：webpack的入口文件，在这里引入全局资源，如CSS、js等和声明全局变量。

### webpack介绍

webpack是一个模块打包器，可以将项目中所有资源打包整合注入到指定位置。在这个项目中是通过main.js引入，然后打包到dist文件夹中。在vue CIL构建的项目中，build目录下存放着webpack的配置文件。

### Font Awesome介绍

一套不错的图标库，提供几百个图标并且用法简单，满足日常开发需求。

方法一：CDN

```
<link rel="stylesheet" href="https://cdn.staticfile.org/font-awesome/4.7.0/css/font-awesome.css">
```

方法二：cnpm

```
cnpm install font-awesome --save-dev
```

之后再main.js中全局引入依赖。

### 动态资源配置

在src/config/config.js中模拟商品信息；

在src/components/index.vue组件中引入并渲染出来；

把这些信息在config.js中配置的好处是这些信息不仅能在index.vue中使用，也可以在Goods.vue中使用。并且修改的时候只需修改一处。

### 动态资源构建

用npm run build来构建项目的生产版本。之后再项目根目录中会出现一个dist文件目录。

vue CLI无法检索路径的字符串，这时可以把静态资源放在src同级的static目录下。当vue CLI构建生产版本时，该目录下的东西就会被注入dist/static中。

### 动态资源存储

使用window.localStorage来存储数据。

window.localStorag来接收对象类型的数据值，所以在读取和写入时，我们需要用到浏览器内置对象JSON。

### 自定义组件

封装两个组件：首页幻灯片、购物车页面的复选框；

## 二、启动线上商城

一个人从头敲代码到项目建成，会学得很全面。不过我暂时只做初步了解，能理解原理以及会修改即可。

首先用cmd进入项目的文件夹；然后安装项目依赖cnpm install；接着启动项目npm start；最后在浏览器中打开http://localhost:8080

果然成功了。

## 三、启动企业网站

发现启动这么方便，于是干脆把剩下几个也一一尝试。

### 理论

#### 响应式设计：

Ethan marcotte在2010年5月提出的概念，指的是网页在不同尺寸和设备上可响应式地显示，达到once write，run everywhere的效果。最初的响应式设计用于CSS3中，通过媒体查询media query判断设备类型，进而对不同设备设置相应的样式表。在实际开发过程中，也会使用js对设备类型进行补充判断。

#### 页面开发-页面切换与滑动：

企业官网大都采用一种布局方式——“顶部导航栏+内容栏”。用户可以通过顶部导航栏轻松切换页面；

许多网站也习惯把多个内容区从上到下组合成一个长页面，通过滑动滚动条来切换浏览器视窗的位置。还有就是用swiper的组件将页面设置为单屏，并以幻灯片翻页的方式来切换视图。本项目就是采用这种。

swiper的代码可以在GitHub上下载好，然后通过静态脚本方式引用和使用它们。

```
<link rel="stylesheet" href="path/to/swiper.min.css"
```

也可以利用npm来安装swiper。然后在相关组件引入和使用它。

```
cnpm install swiper --save-dev
```

#### 划分内容区

顶层header有logo和中英文切换，是固定不变的。共有四个内容区（首页、三个展示内容页）

首页一般设计一个具有冲击力的特效。展示内容页看页面需要什么。

#### 中英文语种切换

把幻灯片内的信息提取出来，vue的插值绑定可以设置占位符，选择不同语言，网站就要不同的语言展示。首先是把所有信息都纳入配置，然后将配置导入组件并绑定到视图模板上。

### 启动

指令如下：

```
C:\Users\Administrator>cd c:/

c:\>cd C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\RentCar

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\RentCar>cnpm install

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\RentCar>npm start
```

然后成功启动。

## 四、启动掌上新闻

资讯类应用

### 理论

应用首屏：新增GIF图作为启动动画，使首屏有一个炫酷的动画。

应用首页：搜索栏、tab选项卡和新闻列表三部分。新闻类别用v-for指令获取数据生成；

新闻详情：新闻的DOM结构都是定制的，但只需要v-html指令将新闻的DOM结构数据表现出来就可以了。

搜索页面：历史记录、猜你想搜的。用window.localStorage来保存用户曾输入过的关键字。

搜索结果：和首页类似，但未加入Tab选项卡。

### 项目构建

这个项目模拟了完整的前后台交互流程，新增了data、store、ajax目录。

data目录充当数据库的角色，里面存储着应用所有动态数据。category.json保存着新闻的分类数据；List.json保存着新闻的简介数据；News.json保存着新闻的DOM数据结构；

ajax目录负责完成与后台接口的对接，并将数据导流到Vuex全局状态管理器。

store目录存储项目的全局状态管理器。

### 启动

和前面一样，成功启动了。但是Chrome浏览器却显示“请在手机端上访问”

方法一：F12，然后点击左上角，显示手机浏览。

结果：不行。

然后刷新一下，可行。

刚刚我差点就想用手机模拟器试一试了，还好谷歌可以模拟。

[vue开发手机端，如何在手机端进行项目的预览和测试](https://blog.csdn.net/weixin_44491927/article/details/99621826) 

差一点就去试一试了。这个掌上新闻还挺好的。比前两个更有参考价值。

## 五、启动SVG画图板

工具类网站

### 理论

SVG是可伸缩矢量图形，一种基于XML的图片格式，尺寸放大或缩小图片质量不损失，并且可以将SVG元素作为DOM元素处理。

#### 基本图形的使用

用<rect><circle><ellipse><line><path>

#### SVG中的渐变

用Linear Gradient和Radial Gradient。

### 页面设计

顶部放logo；左侧为工具类；右侧为菜单栏；中间是画板；

### 启动

按之前的操作启动。

成功启动

## 六、总结

熟悉vue项目的启动后，其他vue项目也终于会引用了。

在第一个项目中：线上商城学习到了webpack和font awesome；

在第二个项目中：企业网站学习到了响应式、swiper.js、双语切换；

在第三个项目中：掌上新闻学习到了前后台交互流程；这一部分很有意思，可以扩展学习后端。第一个项目虽然也有后端，但是没模拟。

在第四个项目中：SVG画板学习到了SVG的概念。

总的来说，通过三部分的学习，最终初步会用vue了。

第一部分[vue的基本知识](https://blog.csdn.net/weixin_42875245/article/details/106558173) 重点讲述网站的发展和vue实例与模板语法

第二部分[vue项目化](https://blog.csdn.net/weixin_42875245/article/details/106698109) 重点讲述用vue CIL进行项目化。（前端路由和状态管理的笔记写在书上）

第三部分，用四个项目讲解vue的项目开发。



之后，尝试一下github上其他vue项目，然后使用elementUI进行前端网站开发；可能会用到不少组件。到时候一个一个试。

再之后，尝试一下学习node.js，然后用express做做后端。

剩下就熟能生巧，根据这些工具然后去理解其底层知识，看HTML、CSS、JavaScript、DOM、网络知识，还有响应式、兼容性、安全、SEO、CSR、SSR、异步编程，还有组件化、less、命名规范、性能优化、内存管理、工程化思想。

最后不断实践，不断理解。

