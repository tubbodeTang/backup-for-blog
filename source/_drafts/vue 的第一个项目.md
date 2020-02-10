---
abbrlink: 7
---
以前用 angular 比较多，虽然也多少看过 vue 的东西，但是迟迟没有开始使用过，也挺遗憾的，错过了 vue 快速发展的时期。

什么时候开始都不迟，今天就来尝试第一个 vue 项目了，做个记录，以后可以参考。

先是脚手架的搭建，angular 也有脚手架。现在大的框架都很贴心帮开发者准备了这么多。

vue-cli，和 angular 也是一样，需要 npm 全局安装



安装好之后，可以用脚手架命令，直接自动化创建项目框架，管理、生成、发布项目，很方便

具体使用可以看官方文档：[vue cli](https://cli.vuejs.org/zh/guide/)



我们按照文档中的说明，在自己选好的文件夹下用命令行创建一个项目

```bash
vue create projectname
```

有默认设置和手动设置两个选项，如果选择手动设置项目需要的结构和配置的话，还需要做进一步设置，

![](http://image.tubbodetang.site/vue_first_1.png)

我这里选择了手动设置项目所以后续还要选择一些设置。

![](http://image.tubbodetang.site/vue_first_6.png)

设置好之后，等待自动创建和下载依赖包

![](http://image.tubbodetang.site/vue_first_4.png)

创建成功，就可以看到脚手架创建的整个项目了：

![](http://image.tubbodetang.site/vue_first_5.png)

差不多是这么一个结构，根据配置的不同，也会有细微差别。

接下来按照脚手架提示在项目根目录下 `npm run serve` 启动项目看看：

![](http://image.tubbodetang.site/vue_first_3.png)

一个基本的项目就建立出来了。

接下来我们为他填充一点血肉，用比较流行的 element-ui。

element-ui 是饿了么开源的 VUE UI 库，由于 vue-cli 采用了插件的方式来帮助建立应用，所以 element-ui 也提供了一个可以配合 vue-cli 的插件。直接用这个插件，就可以引入 element-ui 到项目中了。

用 vue add element 来引入这个 element 插件

![](http://image.tubbodetang.site/vue_first_2.png)

从提示可以看到更改了一部分文件。这个时候启动应用，就可以在主页看到自动添加的一个element-ui 风格的按钮，说明添加成功了。

接下来，可以开始尝试搭建我们的 ui 界面了。

首先是路由和菜单，有了这两个，我们才能有多个页面并在里面跳转

element 布局和布局容器

vue 的路由

