---
title: Flutter 环境搭建
tags: Flutter
categories: Flutter
abbrlink: 45550
date: 2019-07-02 13:31:01
---



安装 flutter



下载 zip 包 或者 直接去 flutter 的 github 项目中下载 or clone 你需要的版本。

安装的时候有四点最需要注意。



1、现在 flutter sdk 要求 有 powershell 5.0 + ，

win 7 如果没有的，可以去 [微软下载中心](https://docs.microsoft.com/zh-cn/powershell/scripting/install/installing-windows-powershell?view=powershell-6) 下载一个

下载中心里面也有查看版本的相关说明



2、如果是 zip 包，解压的时候可能会忽略隐藏的 .git 文件夹造成错误。

所以可以在解压目录下手动初始化一个 git 项目，就有 git 文件了，

或者去 clone 项目，可以直接带 .git 文件，还是建议直接 clone 项目，因为下载 zip 包的问题实在是太多了，后面执行 flutter doctor 的时候也会因为 git 的问题而自动退出，还是直接 clone 省事。



3、一定不要放在需要权限比较高的文件夹下解压/clone，否则会说此时不应有 bin/cache

可以直接解压在某盘的根目录，成功概率大。



4、环境变量配置和国内镜像配置，按要求配置就好。



配置完以上，可以在全局使用 flutter 命令了，第一次用flutter命令的时候会自动下载 dart sdk，

以及一些升级工作。

![img](E:/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/txb406@163.com/a2ce4643cc8841a292c48c300a49301c/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20190702145512.png)



然后 运行 flutter doctor 看看还缺啥没安，

![img](E:/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/txb406@163.com/c4ca378e6cd049ac83f8bb1d4b72b8cb/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20190702145558.png)

我因为之前研究 ionic 的时候配置过安卓开发的一些东西，当时也踩了好多坑才配置好，所以这次基本都有了，只有 sdk 需要升级，然后 Android Studio 要安一下插件这三个问题。



如果从来没有配置过 Android sdk 的童鞋，还得专门找详细的教程来配置，比较麻烦，需要耐心。



问题全部解决之后再  flutter doctor  可以看到已经没有 issues 了 

![img](E:/%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/txb406@163.com/64beea404c6341b697aff7eeebf42336/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20190702153140.png)

然后就可以愉快的开发了。