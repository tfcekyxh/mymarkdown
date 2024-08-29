# 最快时间上手element-ui

> 基于vue2的element-ui2
>
> 这里图快，所以不会使用npm脚手架安装，全用外链安装各种东西
>
> 只需要拷贝官网的入门文档，然后进行自己的修改就可以实现快速使用element-ui的所有组件了。



**引入Vue**

首先要引入Vue，`直接使用<scrpit>引入`-`CDN`中选择前两个都行

我选择这个下面的语句。

```xml
#CDN
#对于制作原型或学习，你可以这样使用最新版本：

<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
```

这里是[Vue官网文档-安装教程页面](https://v2.cn.vuejs.org/v2/guide/installation.html)

<iframe src="https://v2.cn.vuejs.org/v2/guide/installation.html" height="500"/>





**引入element-ui**

有了vue的引入后，然后，我们才能进入[element ui 中文文档](https://element.eleme.cn/#/zh-CN/component/installation)，找到`安装`-`CDN`，使用CDN方式安装，就只需无脑拷贝就可以。

这里我们拷贝这个

```xml
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

<iframe src="https://element.eleme.cn/#/zh-CN/component/installation" height="500"/>





### 使用vue需要注意的点

有些时候发现很多事件，比如绑定的事件没有反应，在后面加上`.native`就可以了

比如`keyup.enter`换成`keyup.enter.native`



# Vue工程的方式使用element-ui

> 这个其实我觉得和`web-component`技术差不多的
>
> 这里我选择element-plus、使用vue3

