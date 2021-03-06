---
title: 程序员的 Tricks - 02
tags: Tools
categories: Tools
abbrlink: 50016
date: 2019-01-08 17:51:01
---



### 程序员的 Tricks - 02



嗯，这个栏目好久没更啦，主要是懒，但其次，很久没遇到过需要特殊处理的数据，其实也是一种幸福……

好，直接进入正题，介绍一下情景：
需求方提供了一堆格式类似的文件（视频、图片、文档等），这些文件的文件名已经按照要求命名好，放在层层嵌套的分类文件夹里，而在前端因为要批量展示这些文件，所以得拿到所有文件的文件名列表

这次的情景还不是特别让人抓狂，但平时遇到的频率应该挺高，所以是非常值得记录的（插一句…我的操作系统是 Windows）。

比如在下面这个图里，我要拿到当前路径下所有的歌名，不只有当前文件夹下一些分散的歌，还有按照歌手和歌手下面按专辑分类文件夹里面的歌。

![](http://image.tubbodetang.site/trick_2_1.png)

没有相关经验的人，此时第一个想到的可能就是一个一个文件去复制文件名整理到文档中，当然，这作为最笨的办法，是可行的。缺点就是非常耗时间，而且如果文件很多（几百个），文件夹又分的比较细致，可能刚操作十来个就崩溃打算放弃了。

这个时候人都会主动寻求一些偷懒的办法，去网上一查，或者问对计算机知识比较了解的人，最后都会指向同一个答案——写个批处理脚本。

其实批处理脚本的概念并不是那么明确，有些软件也支持写脚本来批量处理软件中要用到的文件的，而我们这篇文主要针对 Windows 来说的。并且我也不打算把批处理文件中用到的各种命令语法在这里啰嗦的说一大堆，日常用的不多的话，学了也会很快忘记。

对于不同的需求，基本上利用搜索工具都能找到对应的批处理方案，如果不是有特殊需求或者追求酷炫，我认为没必要专门去学写批处理的命令语法。

最主要的是记住重复的工作计算机总有办法帮我们偷懒批量处理这一条就够了。

以后再遇到这种情况，只要第一时间想的不是一个一个用最笨的方法去处理，而是赶紧搜一下对应的批处理偷懒方法，我写这篇文章的目的就达到了。

最后简单介绍一下流程吧，已经熟练的童鞋可以直接关掉页面啦。

1. 新建一个 .txt 文件，在里面贴上你搜到的对应批处理命令，比如对于我上面举的例子，就是下面这一段（当前文件夹多层级文档列表）：

``` bash
@echo off
for /f "delims=" %%i in ('cd') do set "cl=%%~ni"
tree %cd% /f>文件夹详情.txt
echo 目录已经存入 %cd% 文件夹详情.txt 中！
pause
```
2. 保存 .txt 并关闭，然后修改 .txt 后缀为 .bat ，这时这个文件就已经变为一个批处理文件了 ![](https://github.com/tubbodeTang/PicBed/blob/master/trick_2_2.png?raw=true)

3. 双击执行 .bat，你可以看到命令行黑框（有的只会一闪而过，和批处理命令怎么写有关），说明我们的命令已经执行了

![](http://image.tubbodetang.site/trick_2_3.png)

4. 我得到的结果如下（歌名按层级全部提取出来）

![](http://image.tubbodetang.site/trick_2_4.png)


从上面的简单步骤不难看出，批处理真的是偷懒利器，溜了溜了



