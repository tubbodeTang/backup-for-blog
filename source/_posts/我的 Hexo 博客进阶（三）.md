---
title: 我的 Hexo 博客进阶（三）
tags: 博客搭建
categories: 博客搭建
abbrlink: 28268
date: 2019-08-09 13:31:01
---



上回提到GitHub 有防百度爬虫的措施，所以我们在 Coding Pages 服务上也部署了一遍博客，这还只是折腾之路的第一步。

其实由于 Github 和 Coding 都做了防爬虫处理，搜索引擎是无法直接发现我们博客的，这样别人在搜索问题的时候，搜出来的答案也不会包含我们博客中的内容，相当于我们一直都是在自说自话，所以我们必须要给搜索引擎提交我们的博客站点，才能让搜索引擎知道站点的存在，这样搜索的结果才会有我们的内容。

我们写个人博客虽然不需要什么竞价排名买搜索前列这种操作，但是也不能让搜索结果里完全不存在啊，话不多说，就是干。



### 让各大搜索引擎收录博客

#### 博客的准备工作

为了让搜索引擎知道我们都有什么页面需要被收录，我们先要准备一个文件，里面包含我们博客所有文章的地址，即站点地图（sitemap）。



怎么生成这样一个站点地图呢，已经有好心人开发了现成的工具了，npm 安装一下就可以：

```undefined
百度：npm install hexo-generator-baidu-sitemap --save
谷歌：npm install hexo-generator-sitemap --save
```

插件使用如果有问题可以去 [hexo-generator-sitemap](https://www.npmjs.com/package/hexo-generator-sitemap) 和 [hexo-generator-baidu-sitemap](https://www.npmjs.com/package/hexo-generator-baidu-sitemap) 查看说明



然后修改博客根目录下的配置文件 `_config.yml`，添加以下内容：

```yml
# 自动生成sitemap
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```
如果绑定了域名，想收录域名下的地址，注意要把这项配置改为自己的域名，否则收录的网址可能会不准确。

```yml
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://www.tubbodetang.site
```



最后执行我们已经熟悉的博客生成和部署命令：

```undefined
hexo g
hexo d
```

在 `public` 目录下，就可以看到生成的 `sitemap.xml` 和 `baidusitemap.xml` 两个文件，打开也可以看到生成的 `baidusitemap.xml`  和 [百度平台工具使用帮助](https://ziyuan.baidu.com/college/articleinfo?id=267&page=2) 中要求的 sitemap 格式是一致的，这就是我们准备好的站点地图了。



#### 将站点地图提交到搜索引擎

首先我们要搜索引擎的站长管理工具去注册站长帐号，注册过程就不废话了。

- [百度](http://zhanzhang.baidu.com/)
- [谷歌](https://www.google.com/webmasters/)（自己想办法访问）
- [必应](https://www.bing.com/toolbox/webmaster)（由于前两个一个不好访问，一个搜索结果不尽人意，必应也是一个好的选择）



提交过程其实都差不多，都是：添加网址-验证权限-上传站点地图-等待，这么一个流程。

##### 先说说百度：

登录后在用户中心-站点管理中，添加站点，按照步骤操作

![添加站点](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_1.png?raw=true)



![百度验证](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_2.png?raw=true)

下载验证文件，然后放在博客的 `themes` 主题文件夹的 `source` 目录下，这样博客生成发布之后，这个文件才会在站点的根目录。

然后还是这两步，生成发布博客：

```
hexo g
hexo d
```

此时我们的 `public` 文件夹里就有了验证文件。

按照步骤验证，最后验证成功。

![验证成功](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_3.png?raw=true)

到这里我们已经把站点添加到了平台中。

最后进入站点管理，点击我们刚刚添加的站点，在导航栏找到：数据引入-链接提交，就可以上传我们准备好的 sitemap 了。

地址按照要求填写即可：`yoursite/baidusitemap.xml`

![提交百度站点地图](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_5.png?raw=true)

这里可以看到提交站点其实有很多种方法，甚至可以手动一个一个粘贴提交，自动提交也可以用代码主动推送，我这里只选择了最方便的 sitemap 解决方案，如果想要更快速的提交自己的站点，也可以查一查主动推送的实现方法。

提交之后，可以看到自己的站点正在等待被抓取，这个等待时间不一定，新站可能会更慢，百度的脾气，大家是知道的，如果等不及，建议还是上主动推送。

![提交结果](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_6.png?raw=true)



##### 再说说谷歌：

谷歌和百度除了站长平台的界面长得不一样以外，其他流程都是一样的。就不啰嗦了，还是添加一个站点，然后按步骤验证：

![谷歌验证](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_4.png?raw=true)

下载文件之后放在博客的 `themes` 主题文件夹的 `source` 目录下，生成发布博客：

```
hexo g
hexo d
```

就可验证成功了。

然后在站点地图的地方添加站点地图 `sitemap.xml` 即可

![谷歌站点添加](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_7.png?raw=true)

提交之后一样看到爬取结果。谷歌的比百度快一些，基本一天之后就有状态了。



##### 最后是 Bing 必应：

除了上面的方法，必应比较贴心的准备了和 Google 站长的关联选项，所以我这里就不再重复操作了，直接关联上 Google 站长的信息就可以了。

![Bing](https://github.com/tubbodeTang/PicBed/blob/master/blog_adv_2_8.png?raw=true)

不过必应的收录要求也挺高的，据说他喜欢收录图片站和文章比较长的，收录前还会观察你的站点是否是频繁更新的。收录的时间周期也比较长。



所以除了提交我们的站点到各大搜索引擎以外，最重要的还是好好写文，努力积累！



————————————

参考文章：

[必应收录之如何让bing快速收录你的网站](https://www.i5seo.com/must-be-included-in-how-to-allow-bing-to-quickly-collect-your-website.html)

[Hexo博客收录百度和谷歌-基于Next主题](https://www.jianshu.com/p/8c0707ce5da4)

[Hexo博客提交百度和Google收录](https://www.jianshu.com/p/f8ec422ebd52)

