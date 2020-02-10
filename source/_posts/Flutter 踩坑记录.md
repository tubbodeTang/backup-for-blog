---
title: Flutter 踩坑记录
tags: Flutter
categories: Flutter
abbrlink: 40166
date: 2019-07-02 13:31:01
---



决定踩一下 Flutter 的坑了，做个记录。

教程的话，起步我觉得看这个就够：[Flutter 中文网](https://flutterchina.club/)



### Flutter 踩坑记录

整个过程可能会用到梯子。



#### 下载

可以去官网下载 zip 包（要梯子）或者 直接去 Flutter 的 GitHub 项目中 download or clone 你需要的版本。

[GitHub地址](https://github.com/flutter/flutter)



#### 安装

然后就是按照教程里的步骤解压配置即可，但是配置的时候有 4 点最需要注意：



**1、现在 Flutter SDK 要求 有 Powershell 5.0 + **

win 7 如果没有的，可以去 [微软下载中心](https://docs.microsoft.com/zh-cn/powershell/scripting/install/installing-windows-powershell?view=powershell-6) 下载一个，下载中心里面也有查看版本的相关说明



**2、如果是 zip 包，解压的时候可能会忽略隐藏的 .git 文件夹造成错误。**

有两个解决办法：

1. 在解压目录下手动初始化一个 git 项目，就有 .git 文件夹了

2. 以 clone 方式下载项目，可以直接带 .git 文件

但是经过我的尝试，还是建议直接 clone 项目，因为下载 zip 包的问题实在是太多了，后面执行 `flutter doctor` 命令的时候也会因为 .git 的问题而自动退出，还是直接 clone 省事。



**3、一定不要放在需要权限比较高的文件夹下解压或 clone，否则会说此时不应有 bin/cache**

可以直接解压在某盘的根目录，成功概率大。



**4、环境变量配置和国内镜像配置，按要求配置就好。**



配置完以上，可以在全局使用 flutter 命令了，第一次用 flutter 命令的时候会自动下载 dart sdk，

以及一些升级工作。

![](http://image.tubbodetang.site/flutter_1_1.png)



然后 运行 `flutter doctor` 看看还缺啥没安，

![](http://image.tubbodetang.site/flutter_1_2.png)

我因为之前研究 ionic 的时候配置过安卓开发的一些东西，当时也踩了好多坑才配置好，所以这次基本都有了，只有 Android  SDK 需要升级，然后 Android Studio 要安一下插件这两个问题。doctor 命令很贴心，解决方案也写在上面了，按照要求处理就好了。

如果从来没有配置过 Android SDK 的童鞋，还得专门找详细的教程来配置，比较麻烦，需要耐心。也可以参考我之前写的 [ionic 开发踩坑]() 里面的部分内容来助你踩坑。



问题全部解决之后再  `flutter doctor`  可以看到已经没有 issues 了 

![](http://image.tubbodetang.site/flutter_1_3.png)

然后就可以愉快的开发了。



#### 开发环境

最后提一嘴开发环境。

官方推荐是 Android Studio 来开发，我虽然也安装了，但是还是觉得它过于复杂，所以我暂时还在用 VS Code 在开发。

在 VS Code 里装一下 Dart 和 Flutter 插件，然后就可以愉快的在 VS Code 中使用 Flutter 命令和 Dart 语法提示了，也可以调试和热重载。现阶段还是够用的，后面如果有高级需求了再上 Android Studio 吧。