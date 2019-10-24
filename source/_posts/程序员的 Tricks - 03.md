---
title: 程序员的 Tricks - 03
tags: Tools
categories: Tools
abbrlink: 929
date: 2019-07-01 18:13:01
---



### 程序员的 Tricks - 03



这个系列好久没继续了，说明好久没遇到奇葩的需求，虽然没遇到奇葩需求很开心，但是系列文章没得可写了也是挺纠结的呢。

今天来聊聊之前遇到的一个奇葩事。

咨询人员给了我们一个 Excel 文档，里面只有一个根据数据生成的散点图，源数据的表格并不在这个文档里，而他的要求是……让我们用图里的数据拟合出曲线公式来，然后用拟合出来的公式计算数据。

![](https://github.com/tubbodeTang/PicBed/blob/master/tricks_3_0.png?raw=true)

当时我和我的小伙伴内心又是万马奔腾，可以看到图中数据点很密，点都已经连成线了，根本不是靠带几个值就能反算或者是根据图表上的几个数据点就能编出计算结果来的……

面面相觑之后还是得靠百度，看看有没有合适的解决方案，毕竟程序员也不是万能的。没有的话，就只能取几个临近点估值了，但那样就无法得到用于自动化计算的公式了。

在搜索引擎里找答案，靠的真的是一种问问题的能力，换了几种问法之后，我终于搜到了解决这个问题的关键钥匙：Excel 里的宏。

宏是一个计算机术语，说得是批量处理的事儿。不过在 Excel 中，宏则指 Excel 自动集成的 VBA 高级程序语言编制出的程序。借助这样的程序，我们就可以批量处理需求了。

说到这里又说了一个新词：VBA（Visual Basic Application）

它是微软为了扩展 Windows 应用程序功能而开发出来的一种通用编程语言，是 VB（Visual Basic）语言的一个子集，这种语言写出的程序，可以且只能在 Windows 桌面应用中执行。（也有不法分子利用这点编制目的不良的宏病毒利用文件来传播）

有哪些 Windows 桌面应用程序有执行 VBA 的能力呢？

其实最有名的几大 Office 办公软件：Word、PowerPoint，当然也包括我们今天要说的 Excel，都是能执行 VBA 的应用程序。

学会了 VBA，使用这些软件解决问题和办公的效率将大大提升，所以其实 VBA 完全可以作为一个单独的技能去学习。不过这不是我们今天的重点，我们的重点，只是了解一下这个功能，并看看它有多么强大，以便以后有需求的时候能速速想起并运用。

我找到的是一段可以解决我问题的 VBA 代码，现在就来应用它试一试。

首先打开 Excel（我的是 2013），然后在表名上右击打开代码编辑器。

![](https://github.com/tubbodeTang/PicBed/blob/master/tricks_3_1.png?raw=true)

代码编辑器长这样：

![](https://github.com/tubbodeTang/PicBed/blob/master/tricks_3_2.png?raw=true)

在 ChartData 表（表名也要和程序中的对应才能找到对象）填入如下代码。

```vbscript
Sub GetChartValues()
   Dim nRows As Integer
   Dim X As Object
   Counter = 2

   nRows = UBound(ActiveChart.SeriesCollection(1).Values)
    '数据的数量 nRows 
   Worksheets("ChartData").Cells(1, 1) = "X Values"  
    'ChartData 表的（1，1）格写 “X Values”

   With Worksheets("ChartData")
      .Range(.Cells(2, 1), .Cells(nRows + 1, 1)) = Application.Transpose(ActiveChart.SeriesCollection(1).XValues)
   End With
   '_从第(2,1)格开始，到第(nRows + 1,1)格，填入选中图表的所有 X 值_

   For Each X In ActiveChart.SeriesCollection 
   '如果图表有多个系列值，依次循环输出到 2、3、4 ... n 列
      Worksheets("ChartData").Cells(1, Counter) = X.Name
      '在第一行写入系列名
      With Worksheets("ChartData")
         .Range(.Cells(2, Counter), .Cells(nRows + 1, Counter)) = Application.Transpose(X.Values)
      End With
      ' _从第(2,n)格开始，到第(nRows + 1,n)格，，填入选中图表第 n 系列的所有 X 值对应的 Y 值_
        Counter = Counter + 1   '_下一系列值_
   Next

End Sub
```

大概写了一下注释说明，我也不太会写 VBA，不过看个大概意思还是没问题的。

好了，接下来保存代码，保存的时候会提示普通的 .xlsx 格式不支持宏运行，所以保存为 .xlsm 的格式，这样就可以支持宏运行了。

最后选中我们的图表（一定要选中才有目标对象），运行宏。

![](https://github.com/tubbodeTang/PicBed/blob/master/tricks_3_3.png?raw=true)

然后就看到，酷炫的结果出现了。那张散点图里的 2000 多条数据，全部被提取出来了，这样就可以根据数据去重新拟合一个曲线了。

![](https://github.com/tubbodeTang/PicBed/blob/master/tricks_3_4.png?raw=true)

是不是还挺强大的，能做到一些基础功能做不到或者想都不敢想的事。

更牛逼的是，一旦写好一段程序之后，其他的文件也都可以通用，这样的话，处理百八十个相同需求的文档，就都不在话下了。

好了，今天的程序员偷懒技能就分享到这里。不知道下次还会遇到什么奇葩需求，也不知道下次还要过多久，遇到的时候，我们再见咯。


