---
title: Hexo 博客搭建
tags: 博客搭建
categories: 博客搭建
abbrlink: 10470
date: 2017-09-02 13:31:01
---

我的博客是通过 Hexo + GitHub Pages 搭建的，如果你也想搭建自己的专属博客，也有其他的选择，比如 WordPress 等，下面来讲讲我的博客搭建的过程。

#### 材料准备

- GitHub 帐号一个
- node、npm、git 环境
- 可能需要梯子（或配置 npm 镜像）
- [Hexo中文文档](https://hexo.io/zh-cn/docs/index.html)



#### 安装 Hexo

通过 npm 来全局安装 Hexo

```bash
npm install -g hexo
```

如果总是出错，就用梯子试试，因为有些依赖包可能在墙外。

安装好之后就可以全局使用 Hexo 命令了。



#### 用 Hexo 生成博客模版

在自己需要的地方新建一个文件夹，比如 MyBlog。

然后进入 MyBlog 文件夹，在该路径下启动命令行工具，执行：

```bash
hexo init
```

Hexo 会帮助你建立一个初始的博客模版，并且自动下载依赖包。

同上，如果依赖包总是出错安不上，建议爬梯试试。

图为正在初始化和安装依赖包

![](http://image.tubbodetang.site/blog_build_1.png)

片刻后依赖包安装完成

![](http://image.tubbodetang.site/blog_build_2.png)

至此，最初始的低级博客配置已经 OK 了，我们甚至可以在当前目录运行：

```bash
hexo server
```

然后打开浏览器，访问 `localhost:4000` 就可以看到我们的初始页面了。

![](http://image.tubbodetang.site/blog_build_3.png)

这就是 Hexo 初始化博客的样子，如果你不嫌弃，其实也可以直接用这个作为博客的样子哦。

嗯……不过多少还是有点丑，后面可以再慢慢优化……



#### 熟悉 Hexo 命令

上面我们用到了 `hexo init` `hexo server` ，这些其实都是 Hexo 的命令，熟悉这些命令是用好 Hexo 的必备条件，可以去 Hexo 的官网查看各个命令的用法，我这里只说几个比较常用的：

```bash
  hexo clean     清除静态文件生成后的缓存，更新博客样式之后如果看不到效果就是有缓存，用这个命令来清理。
  hexo generate  生成博客要发布的静态文件
  hexo deploy    发布博客
  
  hexo help      查看 Hexo 命令的使用帮助，会列出所有的 Hexo 命令及用法
  hexo init      这个我们之前用过，就是初始化一个 Hexo 文件夹
  hexo new       新建一个文章，（用的不多，我都直接文件夹里新建，或者复制粘贴）
  hexo publish   把草稿从草稿文件夹移到待发布的文件夹中（用的不多，我都直接手动拖过去）
  hexo server    这个刚刚也用过，开启本地服务器，可以作为发布前的调试和查看确认

```

也可以用简写，比如最常用的两个 generate 和 deploy 可以写成：

```bash
hexo g
hexo d
```



#### 同步推送到 GitHub 并利用 Github Pages 发布博客

之前我们只是在本地建好了我们的博客，也可以在本地服务器上看到我们的博客，那么接下来我们就要利用 GitHub 的 Pages 功能来让我们的博客人人能访问了。

1. 在 GitHub 上创建名为 yourname.github.io 的项目。（以个人账户为名的 Pages 服务只能建立一个）

2. 安装 Hexo 的 git 工具

   ```bash
   npm install hexo-deployer-git --save
   ```

3. 配置博客的 deploy 设置：

   在博客根目录下的 `_config.yml` 文件中，修改 deploy 配置如下：

   ```yaml
   # Deployment
   ## Docs: https://hexo.io/docs/deployment.html
   deploy:
     type: git
     repo: 
         github: git@github.com:yourname/yourname.github.io.git
     branch: master
   ```

4. 生成、发布

   ```bash
   hexo g
   hexo d
   ```

5. 开启 Github Pages 服务发布博客

   在项目的 Settings 中找到下面的设置，然后选择 master 分支即可开启 Pages 服务

   ![](http://image.tubbodetang.site/blog_build_5.png)

6. 接下来浏览器访问 yourname.github.io ,就可以看到发布在互联网上的博客了。

   

到此，以后我们每一次修改博客，发布文章，都只需要执行

```bash
hexo g
hexo d
```

即可看到 GitHub 博客同步更新。



#### 添加样式主题

但是现在我们的博客样式还有点太丑，所以我们还要美化一下它。

好在，Hexo 提供了开源样式库，都是大家制作分享的，我们自己也可以制作，但暂时没有那个时间，所以目前可以去 [样式中心](https://hexo.io/themes/) 选择一个自己喜欢的样式，直接套用就可以了。

套用的方法是：

1. 先把别人的主题文件去 GitHub 上克隆或者下载到 `themes` 文件夹里

2. 配置博客根目录下的 `_config.yml` 文件如下：

   ```yaml
   # Extensions
   ## Plugins: https://hexo.io/plugins/
   ## Themes: https://hexo.io/themes/
   theme: your-theme-name
   ```

   这里的 `your-theme-name` 和 `themes` 文件夹中的主题文件名字保持一致即可。

3. 修改主题配置在主题文件中的 `_config.yml` 文件修改



不过别人的样式终究有的地方不能符合自己的要求，多少需要自己修改下，但是这个比较需要代码知识，所以有空再单开文章一个写写我折腾的过程吧。

刚搭建的博客，先挑一个自己喜欢的、差不多的样式用上，赶紧开始写文章才是正道。



#### 发布第一篇文章

发布文章很简单，你可以用上面提到的命令来创建并发布，也可以直接在 `source/_post` 文件夹下新建一个 Markdown 文件，在里面按照格式写好文章。

然后 `hexo g` `hexo d` 生成发布就可以了。





本文完。

————————————

接下来就是漫漫的写博客和折腾博客之路了，一起见证。





