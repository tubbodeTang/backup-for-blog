---
title: Hexo 博客阿里云同步部署更新
tags: 博客搭建
categories: 博客搭建
abbrlink: 31145
date: 2020-01-10 13:31:01
---



之前的博客一直是同时挂在 GitHub Pages 服务和 Coding 的 Pages 服务上的。但是网站备案通过后我一直没时间管，有一天忽然通知我需要指向阿里云国内节点服务器才行，否则就按空壳网站取消备案，所以没办法，决定先把博客放上阿里云再说吧……



由于购买的是 Ubuntu 操作系统的，所以上来先是安装 nginx。

#### nginx 的安装

切换到 root 用户

用 `apt-get install nginx` 命令来安装 nginx

![](http://image.tubbodetang.site/hexo_aliyun_2.png)

如果出现以上错误，就按照指示 `apt-get update` 一下，然后重新执行安装命令即可。

安装成功之后我们可以 `$sudo /etc/init.d/nginx start` 启动一下 nginx 服务，看看安装效果，访问我们阿里云服务器的公网 ip ，可以看到如下页面

![](http://image.tubbodetang.site/hexo_aliyun_3.png)

说明 nginx 服务已经运行起来了，接下来就是进一步的配置了。



#### git 安装

通过  `apt-get install git` 在 Ubuntu 上安装 Git。

安装成功后，同样通过 `git --version` 命令测试一下安装情况。出现版本号说明成功。

![](http://image.tubbodetang.site/image-20200110141547355.png)

接下来做好用户名和邮箱的全局配置。

```
git config --global user.name "your name"
git config --global user.email "your email"
```



#### 博客的初步挂载

进入 `/var/www/html` 目录中，这是 nginx 的默认目录。把之前放在 GitHub 的 Hexo 博客项目 clone 到 nginx 的默认目录下。然后修改一下 nginx 在 `/etc/nginx/sites-available/default` 文件中的默认配置，使路径指向我们的 clone 的博客项目。我的项目就叫 `tubbodeTang.github.io`，如下图：

![](http://image.tubbodetang.site/image-20200110155617578.png)

这个时候再访问我们的公网 ip ，就不是 nginx 默认的欢迎页了，已经可以看到我们的静态博客了



#### GitHub 与阿里云同步更新设置

刚刚我们只是把静态博客展示了出来，博客的来源是从 GitHub 上 clone 下来的。这还不够，因为我们总不能每次更新了博客都上阿里云 clone 或者 pull 一下来让其保持与 GitHub 上存储的内容一致，那就太让人抓狂了。

我们需要的是每次 hexo d 发布博客的时候，阿里云上的内容都自动更新。



##### 阿里云 git 服务搭建

在阿里云服务器添加一个 git 用户用来专门进行 git 操作。

```
adduser git
```

然后在 `home/git/` 目录下创建一个裸仓。

![](http://image.tubbodetang.site/hexo_aliyun_4.png)

因为后续的操作都是通过 git 用户，所以把这个裸仓的权限给到 git 用户。可以用 `chown` 命令的 `-v` 参数看到过程。裸仓下所有的文件权限都递归的给到了 git 用户。

![](http://image.tubbodetang.site/image-20200110161942657.png)



在**本地机器**执行  `cat ~/.ssh/id_rsa.pub`  获取到本机的 SSH 公钥

![](http://image.tubbodetang.site/image-20200110175830814.png)

然后进入阿里云服务器 git 用户的  ~/.ssh 目录，打开 authorize_keys 文件进行编辑。把本地机器的 SSH 公钥粘贴写入。

```
$ cd /home/git/
$ mkdir .ssh
$ cd .ssh
$ vi authorized_keys
```

注意我这里因为是裸机，服务器上面 `/home/git` 目录下应该没有 `.ssh` 目录，所以得自己创建（打开即自动创建）authorized_keys 之后，把刚才复制下来的公钥粘贴进去，就可以了，保存退出。



我们可以先测试一下本地对阿里云 git 服务的连接情况，试一下 clone 操作，这时可以把阿里云服务添加到known_host 中。成功克隆裸仓说明服务可以连接。

![](http://image.tubbodetang.site/image-20200112142551399.png)



##### 使用 hooks 同步更新

为了能实现自动同步，我们需要用到 Git 的 hook 功能。让我们的裸仓接到本地的 push 之后，触发动作。

在 `/home/git/hexo/hooks/` 路径下新建一个 `post-receive` 文件

```
vim post-receive
```

并写入以下内容：

```
#!/bin/sh
git --work-tree=/var/www/html/tubbodeTang.github.io --git-dir=/home/git/hexo.git checkout -f
```

这里的文件夹名字以自己的名字为准。就是之前我们在 nginx 默认路径下 clone 的那个。以上操作就是在接到 push 之后，把内容写入到 nginx 默认路径下。

最后的效果可以看到 hooks 路径下新生成了 post-receive 文件

![](http://image.tubbodetang.site/image-20200110180338874.png)

之前赋予权限的时候还没创建这个文件，重新更改一下权限。

![](http://image.tubbodetang.site/hexo_aliyun_1.png)



##### 为本地 Hexo 项目添加推送配置

最后的最后更新一下本地 hexo 的配置文件，添加：

```
hexo: git@你的公网ip:/home/git/hexo.git,master
```

如图：

![](http://image.tubbodetang.site/hexo_aliyun_5.png)

这样 `hexo d` 的时候，就能同时推送到阿里云服务器，然后触发我们写好的 `post-receive` 钩子，去更新我们放在 nginx 默认路径下的静态博客站。



以上全部没问题之后， `hexo d` 更新发布一篇文章看看，刷新我们的公网页面，可以看到，已经同步发布了。



————————————

本文完。



#### 参考文章

[Hexo 从 GitHub 到阿里云](http://iamwr.com/2018/12/20/hexo-from-github-2-aliyun/)

[阿里云搭建Git服务，实现Hexo自动部署](https://imys.net/20160303/hexo-nginx-auto-deploy.html)

[在阿里云上搭建自己的git服务器](https://www.cnblogs.com/herd/p/7063091.html)