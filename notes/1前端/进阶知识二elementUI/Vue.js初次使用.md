# Vue.js初次使用

教程：https://cn.vuejs.org/v2/guide/

时间：2020/5/2

内容：安装、介绍、实例、模块语法、计算属性和监听器、class与style绑定、条件渲染、列表渲染、事件处理

我认为学习一个UI框架，应该把它当成HTML文档使用，用其实现文本、图片、表格、表单、超链接；学以致用，不然跟着这个步骤了有些晕头转向，找不到方向。看这个前，最好把JavaScript掌握好。

前置知识：JavaScript最基础的关键字和语法结构、事件机制、DOM编程、闭包、对象引用、内置对象的常用方法；

正确的教程应该是用其做demo，边做demo边说内容。学以致用。

[toc]

## 一、安装

下载并用script标签引入，把Vue注册为一个全局变量 ；CDN、NPM

命令行工具、

 

## 二、介绍

Vue是一套用于构建用户界面的渐进式框架。从低向上逐层应用。Vue.js的核心库只关注图层，不但易于上手，还便于与第三方库或既有项目整合。

 

## 三、实例

每个Vue应用都是通过Vue函数创建一个新的Vue实例开始的。

Var VM = new Vue（{//选项 el :’#app’, data : data,}）

每个Vue实例在被创建时都要经过一系列的初始化过程（设置数据监听、编译模板、将实例挂载到dom并在数据变化时更新DOM等），在这个过程会运行一些叫生命周期钩子的函数，让用户在不同阶段添加自己的代码。

Created : function(){console.log(“a is:’+this.a)})  mounted  updated destroyed

生命周期：创建一个Vue实例-初始化（事件&生命周期）-初始化（注入&检验）-是否指定（el）-是否指定（template）-是的话将template编译到render函数中，否的话将el外部的HTML作为template编译-创建vm.$el并用其替换‘el’-挂载完毕（虚拟DOM渲染）-vm.$destroy()函数时-解除绑定，销毁子组件以及事件监听器-销毁完毕。

Beforecreate-created-beforeMount-mounted(update)-beforedestroy-destroyed

 

## 四、模板语法

Vue使用基于HTML的模板语法，允许开发者声明式地将DOM绑定到底层Vue实例的数据。所有vue.js的模板都是合法的HTML。

底层的实现上，Vue将模板编译成虚拟DOM渲染函数，结合响应系统，可以最少需要重新渲染组件，将DOM操作次数减到最少。

如果足够的熟悉DOM并且偏爱JavaScript的原始力量，可以不用模板，直接写渲染（render）函数，使用可选jsx语法。

插值：

文本（<span v-once>这个将不会改变: {{ msg }}</span>）

原始HTML（<p>Using mustaches: {{ rawHtml }}</p>）

Attribute（<div v-bind:id="dynamicId"></div>）

指令（<p v-if="seen">现在你看到我了</p>）

 

## 五、计算属性和侦听器

模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。

对于任何负载逻辑，应当使用计算属性。

Vue提供了一种更通用的方式来观察和响应Vue实例上的数据变动：监听属性。

虽然计算属性在大多数情况更合适，但有时也需要一个自定义的侦听器。这就是为什么Vue通过watch选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

 

## 六、class与style绑定

操作元素的class列表和内联样式是数据绑定的一个常见需求。因为它们都是attribute，所以我们可以用v-bind处理它们。

绑定HTML class：

对象语法（<div v-bind:class="{ active: isActive }"></div>）

数组语法（<div v-bind:class="[activeClass, errorClass]"></div>）

用在组件上（<my-component class="baz boo"></my-component>）

绑定内联样式

对象语法（<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>）

数组语法：<div v-bind:style="[baseStyles, overridingStyles]"></div>

 

## 七、条件渲染

v-if：<div v-if="Math.random() > 0.5"> Now you see me</div>

v-else：<div v-else> Now you don't</div>

v-show：<h1 v-show="ok">Hello!</h1>

 

## 八、列表渲染

v-for：<div v-for="(value, name) in object"> {{ name }}: {{ value }}</div>

 

## 九、事件处理

可以用v-on指令监听DOM事件，并在触发时运行一些JavaScript代码。

在HTML中监听事件，违背了关注点分离的优良传统。但由于所有vue.js事件处理方法和表达式都严格绑定在当前视图的VM上，它不会导致任何维护上的困难。使用v-on有以下几个好处：1看HTML模板可以轻松定位JavaScript代码的对应方法；2无须再JavaScript里手动绑定事件，和DOM完全解耦，更易于测试；3销毁VM时，所有事件处理器自动删除。

 

## 十、表单输入绑定

使用v-model指令在表单input、select元素上创建双向数据绑定。他会根据控件类型自动选取正确的方法更新元素。V-model本质上是语法糖，负责监听用户的输入事件和更新数据。

 

 

## 十一、组件基础

组件的可复用的Vue实例，且带有一个名字。

一个组件的Data选项必须是一个函数。

 

## 十二、组件注册

组件名：vue.component

全局注册、局部注册、模块系统

 

## 十三、prop的大小写

HTML中的attribute名是大小写不敏感。所以浏览器会把所有大写字符解释成小写字符。这意味着使用DOM中的模板是，camelCase的prop名需要使用等价的kebab-case命名。

 

## 十四、自定义事件

事件名this.$emit('myEvent')

自定义组件：<base-checkbox v-model="lovingVue"></base-checkbox>

将原生事件绑定到组件<base-input v-on:focus.native="onFocus"></base-input>

 

## 十五、处理边界情况

访问元素&组件：

程序化的事件侦听器

循环引用、控制更新

 

## 十六、进入/离开&列表过渡

Vue在插入、更新或者移除DOM时，提供多种不同方式的应用过渡效果。包括以下工具：1在CSS过渡和动画中自动应用class；2配合使用第三方CSS动画库；3在过渡钩子函数中使用JavaScript直接操作DOM；4可以配合第三方JavaScript动画库。

 

## 十七、状态过渡

Vue的过渡系统提供了非常多简单的方法设置进入、离开和列表的动效，如数字和运算、颜色显示、svg节点的位置、元素的大小和其他的property；这些数据要么本身以数字形式存在，要么可以转换为数值。有了这些数值，可以结合Vue的响应式和组件系统，使用第三方库来实现切换约束的过渡状态；

状态动画与侦听器、动态状态过渡、把过渡放到组件里、赋予设计以生命

 

 

## 十八、混入mixin

混入提供一种非常灵活的方式，来分发组件中的可复用功能。

选项合并、全局混入、自定义选项合并策略

 

## 十九、自定义指令

除了核心功能默认内置的指令v-model和v-show，Vue允许注册自定义指令。

钩子函数参数：el\binding\name\value\oldValue\expression\arg\modifiers\vnode

动态指令参数：argument

函数简写、对象字面量、

 

## 二十、渲染函数&JSX

Vue推荐在绝大多数情况下使用模板创建你的HTML。然而在一些场景中，需要JavaScript的完全编辑能力。这时需要用渲染函数，它比模板更接近编辑器。

节点、树以及虚拟DOM

渲染函数render: function (createElement) { return createElement('h1', this.blogTitle)}

虚拟DOM：Vue通过建立一个虚拟DOM来追踪自己要如何改变真实DOM

return createElement('h1', this.blogTitle)

render函数显得比较复杂，使用JSX语法，可以写出更接近于模板的语法上。

new Vue({ el: '#demo', render: function (h) {

  return (   <AnchoredHeading level={1}>

​    <span>Hello</span> world!   </AnchoredHeading>  ) }})

 

## 二十一、插件

通过全局方法vue.use()使用插件、