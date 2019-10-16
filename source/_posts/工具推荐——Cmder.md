---
title: 工具推荐——Cmder
tags: Tools
categories: Tools
abbrlink: 65333
date: 2018-07-22 22:39:06
---

做开发久了，每次在论坛上查找问题的时候总是看到用 Mac 或者其他非 Windows 环境开发者的终端截图，又漂亮又明晰，看着才有点像电影里演的 Hacker 那样高大上。然而大多数是用 Windows 自带终端的我们，看起来总是不那么酷炫，并且使用中确实有些必要的、能提升开发效率的功能是缺失的。

鉴于此，我在查找了一番之后，发现了 Cmder 这个 Windows 环境下的终端神器，体验确实很不错，所以推荐给大家。

Cmder 的优点：

- 是免安装压缩包，解压直接可用

- 支持 Git 等命令

- 支持多标签页

- 支持自定义终端

- 内置多种主题，支持自定义主题

![官网](https://github.com/tubbodeTang/PicBed/blob/master/cmder_main.png?raw=true)

上面这个图是我从 Cmder 的[官网](http://gallery.echartsjs.com/editor.html?c=xHJaWqD-1Q)找的。

不过本文到此还没有结束。

平时开终端的时候都是直接用『Win+R』命令，然后运行 cmd 的，为了使用 Cmder 也能这样方便，不用每次都开启 .exe 文件，我们当然还要为 Cmder 配置环境变量啦。

环境变量配置如下：

先给系统变量中添加一个变量，值是解压后 Cmder.exe 所在的路径，然后将这个新添加的变量添加到系统 Path 中：

![环境变量](https://github.com/tubbodeTang/PicBed/blob/master/cmder_3.jpg?raw=true)

如果有需要，还要向用户变量的 Path 中添加解压后的 bin 路径，才能使配置生效。

![Path](https://github.com/tubbodeTang/PicBed/blob/master/cmder_2.jpg?raw=true)

做好配置之后，可以直接使用『Win+R』命令，然后运行 cmder 就可以直接启动 Cmder 了。

** 还有一个很重要的懒人配置 ** 就是平时开发的时候一般不会用命令行直接去找执行路径，而是在路径下『Shift+右击』快速打开该路径下的终端。

Cmder 也可以这样配置，我们只需要以管理员方式打开 Cmd 或者 PowerShell ，输入 『Cmder.exe /REGISTER ALL 』然后执行就可以了。之后我们就能在任意菜单下右击，点击『Cmder Here』 即可。

最后效果就是这样的：

![last](https://github.com/tubbodeTang/PicBed/blob/master/cmder_1.png?raw=true)


其他的个性化设置，比如主题更换等我就不多啰嗦了，在Settings里大家都可以快速找到

![settings](https://github.com/tubbodeTang/PicBed/blob/master/cmder_0.jpg?raw=true)


毕竟自己配置的才是最酷最好用最适合自己开发习惯的。

