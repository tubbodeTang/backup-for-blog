---
title: 我的 Hexo 博客进阶（一）
tags: 博客搭建
categories: 博客搭建
abbrlink: 62063
date: 2019-07-12 13:31:01
---

[Hexo 博客搭建](www.tubbodetang.site/2017/09/02/Hexo 博客搭建/) 这篇文章已经讲了如何借助 Hexo 搭建一个静态博客，目前我们的博客已经有了属于我们的内容和样式风格，也可以借助 GitHub 的 Pages 功能在互联网上访问到了，那么如何才能让我们的博客写起来效率更高，更高大上呢？



#### 图床

用 Markdown 写博客，有一个最不好处理的地方就是，插入图片的时候，图片的地址链接不好做。

图床就是为了储存我们的图片，并且生成可以在互联网上任意访问的服务器地址的，有了服务器地址，我们储存在图床的每一个图片，就都有自己专属的地址链接了。

##### 图床的选择

图床其实也有很多的解决方案，甚至有很多免费的图床，但是免费总有一定的风险：

- 指不定哪天就停止维护了（对于个人维护的图床站尤其如此）
- 有可能突然加了防外链，让我们的图片无法访问（比如简书、微博图床以前可用，现在都不能用了）

所以我们这里还是建议使用付费的大品牌存储来建立私人图床，可以相对稳定一些，不用担心未来的迁移成本。

付费图床比如：

- 腾讯 COS 储存
- 阿里云 OSS 储存（目前收费是这几个里最贵的）
- 七牛云（提供的测试地址只能使用 30 天，后续用得绑定已备案域名，有些麻烦）
- 又拍云

我这里由于一些其他问题，暂时注册了图床空间但还没有开始使用，所以对具体的图床建立方式就不介绍了。

##### 图床工具

有了专属的图床空间之后，我们还需要一个便捷的上传、生成链接的工具来配合我们日常使用，否则手动一张一张传照片再一张一张复制地址，就很让人心累了。

图床工具也有很多，甚至让人眼花缭乱，而且根据不同数据储存服务商提供的 API 我们自己也能写一些小工具，不过这样就很费事了，喜欢折腾的同学可以多试试，我这里只分享两个使用的人比较多，我个人也比较喜欢的：

- [PicGo](https://github.com/Molunerfinn/PicGo)（Windows）
- [iPic](https://toolinbox.net/iPic/)（MacOS）。

可以点击链接看看官方文档配置使用，配置都比较简单，不难上手。因为是个人开发，觉得做得好的朋友可以给他们点赞支持，这样我们才能一直有好用的软件用，省的自己造轮子。

##### 我的图床搭建

我因为一直在用 Windows 环境工作，所以自然选择 PicGo 作为我的图床工具。PicGo 中还贴心的提供了 GitHub 图床的上传方式，由于我目前还无法使用付费的图床空间，所以刚好配合 PicGo 用 GitHub 仓库建立了一个图床。

[GitHub 图床搭建，配合 PicGo 使用的方法](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github图床)

这个方式也是免费的，相对也稳定，但最可怕的就是，GitHub 国内访问有时很慢，还有一定的 404 风险，所以后期我也会尽快更换付费图床的。到时候再对图床的搭建这一部分进行更新。



#### 域名的购买以及关联

使用 GitHub Pages 功能搭建博客之后，默认的地址都是 github.io 这样的形式，虽然说不是不能用，但是就是看起来有点低级，不太像属于个人的博客，倒像是属于 GitHub 的博客。

所以有条件的朋友，可以挑选一个属于自己的域名，然后关联到 GitHub 博客，这样的话，其他人看到我们的博客就更具有我们个人的品牌色彩了。

暂时没有打算关联域名的朋友，就不用看这一部分的内容了。

##### 域名的购买

我是在阿里云买的，也可以去腾讯云等等其他出售域名的网站购买。

购买前先挑一个自己中意的，然后搜索一下是否可用，就可以加入购物车付费购买了，和淘宝一个流程。不同的域名价格也不同，有的还有连续购买多年的优惠活动，还有一些网站会举办新用户赠送一年免费域名这种活动，都可以了解一下，然后做个对比，选择一个最适合自己的就可以了。

![阿里云域名购买](http://image.tubbodetang.site/blog_adv_1.png)

##### 域名的关联

有了域名之后，我们还要对域名进行实名认证，没有认证的域名状态会显示未认证，无法正常使用，这一步也很简单，只要上传一下身份证信息，几分钟之后就可以认证成功了。

![域名认证](http://image.tubbodetang.site/blog_adv_2.png)

然后我们对域名添加解析，解析到自己 GitHub Pages 博客的 IP 地址。

![添加解析](http://image.tubbodetang.site/blog_adv_3.png)

过几分钟之后在 GitHub 的配置中，可以看到已经关联到了我们的域名。

![](http://image.tubbodetang.site/blog_adv_4.png)

此时再访问我们的域名，就可以看到博客已经可以直接通过域名打开了。



*关于备案的小知识*

购买域名的很多搜索结果里都会说到备案这件事。那么我们的域名没有经过备案可以用吗？会不会因为没有备案就产生什么问题呢？

其实备案主要是针对网站备案，域名只是网站的“代号”而已，所以其实域名是不存在备案一说的，对域名的备案只是对网站备案的简称罢了。

GitHub 博客是放在 GitHub 的国外服务器的，所以不用备案，博客也可以正常使用。

如果你还想把博客建立在自己购买的服务器上，不用 GitHub 的 Pages 服务，就要对自己购买的服务器进行备案建站，然后关联域名，这个时候，你的域名也相当于已经备过案了。

但是，环境特殊，我们还是注意不要写不该写的内容。否则有一天被 404 了，就真的需要自己买服务器建站写博客了，随之而来也有很高的迁移成本。

