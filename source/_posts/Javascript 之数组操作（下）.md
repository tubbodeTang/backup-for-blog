---
title: Javascript 之数组操作（下）
date: 2018-03-15 14:04:01
tags: Javascript
categories: Javascript
---


>嗯，接着上次的写，这次写的几个方法，使用频率相对来说少一些，最后几个混个眼熟吧，可能不经常用还是会忘记（捂脸
  



## 数组的常用操作


#### 数组的常用方法 


##### copyWithin()

用于复制调用数组中的一部分，到调用数组的指定位置。会覆盖原有的元素。

用法：
```
// copyWithin(复制目标位置，?复制源起始位置，复制源结束位置。默认是到数组的末尾)
// 注意，源起始位置和结束位置的大小如果不对，这个方法将毫无作用。

var Array1=[a,b,c,d,e,f];

Array1.copyWithin(2,0);
// 结果是Array1=[a,b,a,b,c,d]

Array1.copyWithin(2,0,3);
// 结果则是Array1=[a,b,a,b,c,f]

```


##### fill()

用于把某个对象或值填充到数组，此操作会改变原数组的元素

用法：
```
// array.fill(要填充的对象 , ?开始填充的位置。默认是0 , ?停止填充的位置。默认array.length)

var Array1 = ["a", "b", "c", "d"];
var f = ["hh", "jj"];
Array1.fill(f, 1, 3);

// Array1 输出结果：[Array(2), Array(2), Array(2), Array(2)]
```


##### join() VS toString()

join() 用于把数组中的所有元素转换一个字符串。
这些元素是通过指定的分隔符进行分隔的，如果没有指定，默认是用逗号分隔。
而 toString() 把数组中的所有元素转换一个字符串并用逗号分隔，不能指定分隔符。
用法：
```
// array.join(?分隔符。默认是",")
// array.toString()

var f = ["hh", "jj"];
var Array1 = ["a", "b", "c", "d", "e", f];
console.log(Array1.join("#")); // 控制台输出 a#b#c#d#e#hh,jj
console.log(Array1.toString()); // 控制台输出 a,b,c,d,e,hh,jj

```

##### reduce() VS reduceRight()

这两个方法也类似，只不过 reduceRight() 从右往左操作，reduce() 从左往右操作。

以 reduceRight() 为例介绍用法：
```
//array.reduceRight(function(初始值, 或者计算结束后的返回值, 当前元素, ?当前元素的索引, ?当前元素所属的数组对象), ?计算的初始值。默认是尾元素，这时计算将从倒数第二个元素开始。如果指定了初始值，计算将从第一个元素开始)

var numbers = [2, 45, 30, 100];
function getSum(total, num) {
    return total - num;
}
console.log(
  numbers.reduceRight(getSum,200);
)
// 控制台输出23

console.log(
  numbers.reduceRight(getSum);
)
// 控制台输出23

```
这两个操作还能衍生出一些神奇的功能，请移步[这里](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)参考



##### splice()

用于向源数组中删除，添加元素，参数比较多，直接看例子比较清楚。

用法：
```
//array.splice(start, ?deleteCount, ?item1, ?item2, ?...)
//除开始操作的位置必须外，其他都是可选项
//也有以下三种情况，注意区间的位置，都是闭区间
//1. 从start位置开始删除[start，end]的元素。
//array.splice(start)
//2. 从start位置开始删除[start，Count]的元素。
//array.splice(start, deleteCount)    
//3. 从start位置开始添加item1, item2, ...元素。
//array.splice(start, 0, item1, item2, ...)   

var myFish = ["parrot", "anemone", "blue", "trumpet", "sturgeon"];
var removed = myFish.splice(myFish.length - 3, 2,"red");
// 运算后的myFish： ["parrot", "anemone", "red", "sturgeon"] 
// 被删除元素数组：["blue", "trumpet"]
```


##### valueOf()

valueOf() 方法返回 Array 对象的原始值。即 Array1.valueOf()与 Array1 返回值一样。
valueOf() 方法通常由 JavaScript 在后台自动调用，不需要在代码中出现，了解一下即可。