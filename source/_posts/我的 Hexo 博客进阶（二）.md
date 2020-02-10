---
title: 我的 Hexo 博客进阶（二）
tags: 博客搭建
categories: 博客搭建
abbrlink: 25110
date: 2019-07-31 13:31:01
---



有了博客之后，当然是需要被更多人看到了，我们总不希望自己写博客是写给自己看，自说自话的吧，那就不叫博客，叫日记了。所以博客进阶，我们来讲讲如何让更多人看到我们的静态博客。

由于 GitHub 有防百度爬虫的措施，建议把我们的博客在 [Coding](https://coding.net/) 上也做一遍，这样国内用的比较多的百度搜索可以通过爬取 Coding 上的页面来找到我们的博客，国外搜索也不影响，双管齐下，提升我们博客被发现的效率。

Coding 是腾讯旗下的代码托管平台，和 GitHub 类似，所以 Coding 同步 GitHub 博客，流程其实也和 GitHub 开启 Pages 服务差不多，有过 GitHub 部署博客的经验，相信在 Coding copy 一份也不是什么难事。



#### 注册账号

万事第一步，注册。不多说，先自行注册一个 Coding 平台的账号。



#### Coding 建立仓库及准备

##### 新建项目

这里可以直接提交我们的静态博客到新建的空仓库，也可以参阅 [腾讯开发者平台中的说明](https://dev.tencent.com/help/git-import-tencentcloud) 将 Github 上的仓库导入到 Coding。

我这里采用的是导入的方法：

在 Coding 中新建一个名为 ` yourname.coding.me` 的项目，不勾选 `启用 README.md 文件初始化项目`，也不添加 `License` 和 `.gitignore` 文件。项目地址那里，会根据你的项目名称自动生成。由于 pages 服务对项目名有特殊要求，所以这里我们要尽量写成下面的形式，不然可能会造成页面无法正常打开，后面修改路径会很麻烦还容易出错。

![](http://image.tubbodetang.site/blog_adv_2_10.png)



##### 添加 SSH Key 

以前用 GitHub 的时候已经生成过密钥，密钥所在目录为(`C:\Users\yourUserName\.ssh\id_rsa`)，直接拷贝之后在个人设置中添加就好了

![](http://image.tubbodetang.site/blog_adv_2_9.png)

然后测试一下公钥：

```bash
ssh -T git@git.coding.net
```

成功之后就可以向 Coding 提交代码了。



#### 导入 GitHub 的博客仓库到 Coding

见 [腾讯开发者平台中的说明](https://dev.tencent.com/help/git-import-tencentcloud) 

大致步骤如下：（注意地址要和自己的仓库保持一致）

1. 将 Github 上想要导入的项目完整克隆到本地。

   本地执行

   ``` 
   git clone https://github.com/yourname/yourname.github.io.git --bare
   ```

2. 克隆完成后，将克隆好的仓库推送到 Coding 上。
   使用 Coding 仓库页面提供的 URL。推送所有的分支和对象

   ```
   cd yourname.github.io.git
   
   git push https://git.dev.tencent.com/yourname/yourname.coding.me.git --all
   ```

3. 完成后，再推送所有的标签。

   ``` 
   git push https://git.dev.tencent.com/yourname/yourname.coding.me.git --tags
   ```


这样，整个博客仓库就全部导入到 Coding 了。



#### 博客设置同步推送

修改博客根目录下的`_config.yml`文件，内容如下：

```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
      github: git@github.com:yourname/yourname.github.io.git
      coding: git@git.dev.tencent.com:yourname/yourname.coding.me.git
  branch: master
```

测试一下是否正确，需要重新生成部署

```bash
hexo g
hexo d
```

看到 Github 和 Coding 同步更新的记录，说明设置成功。



#### 打开 Coding 的 Pages 服务

直接在左侧栏找到 ``` 代码 - pages 服务``` 选项卡，一键开启即可。

![开启 Pages 服务](http://image.tubbodetang.site/blog_adv_2_12.png)

片刻，开启成功：

![](http://image.tubbodetang.site/blog_adv_2_13.png)

直接点击访问地址，就可以看到自己的静态博客了。

Coding 会帮我们自动做一些配置，因为我们的博客只有 master 分支，所以默认就建立在 master 分支上。我们也可以做一些其他的设置，比如绑定域名之类的，这个在 [博客进阶（一）]() 中我们已经讲过，有需要的可以参考设置一下。

![](http://image.tubbodetang.site/blog_adv_2_11.png)



至此，我们的 Coding 博客已经全部设置完成了。下一篇打算整理一下怎么把站点提交到各大搜索引擎，让他们的爬虫来发现我们的博客。





————————————

参考文章：

[Hexo博客之速度优化](http://fengdi.org/2017/08/07/Hexo%E5%8D%9A%E5%AE%A2%E4%B9%8B%E9%80%9F%E5%BA%A6%E4%BC%98%E5%8C%96.html)

