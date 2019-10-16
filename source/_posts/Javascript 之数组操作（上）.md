---
title: Javascript 之数组操作（上）
tags: Javascript
categories: Javascript
abbrlink: 52385
date: 2018-02-06 13:31:01
---

>从今天开始，将系统总结一系列 Javascript （Js）的原生操作。因为平时很多时候都是在使用现成的 Js 框架进行开发，（如 Jquery、AngularJs 等），对 Js 本身反倒没有太多关注。但万变不离其宗，相信对 Js 更深入、更全面的掌握，才是更好理解、运用上层框架的基础。
  

平时开发中遇到最多的数据处理，肯定不外乎就是处理大量的数组数据。

不管是遍历还是数组整体操作，只有更熟练才能更高效的从海量数据中得到我们所需要的信息。

## Js中的数组
众所周知，Js 中所有的变量都是对象，所以数组也是一种对象。

#### 数组的创建 
简单介绍一下数组的创建，有三种形式：
1. 第一种（最笨最普通的方法，平时都不会这么写）
```
var myArray=new Array();
myArray[0]=1;
myArray[1]=2;
myArray[2]=3;
```
2. 第二种（平时也不会用到）
```
var myArray=new Array(1,2,3);
```
3. 第三种（本人最常用到）
```
var myArray=[1,2,3];
//或者直接创建空数组

var myArray=[];
//然后再进行一系列赋值操作
```
*注意*

Js 的同一个数组中可以有不同类型的元素，虽然平时处理数据可能很少有这种情况出现，但是知道也没坏处


#### 数组的访问
Js 中的数组也遵循循秩访问，访问的时候直接通过下标就可以访问到对应元素，上面的例子其实已经提到，就不再啰嗦了


## 数组的常用操作

#### 数组的常用属性

##### length  
用来返回数组元素的个数，循环的时候可用作边界条件

#### 数组的常用方法 
这个部分比较长，所以打算按方法的使用频率降序分两次写完。  
  
    
      
      

##### concat()

  
用于连接2或2+个数组，concat这个词语也是编程的专业术语，基本只会在讨论编程的时候才会出现。

用法：
```
var Array1=[a,b,c];
var Array2=[d,e];
var Array3=[f];
var result=Array1.concat(Array2,Array3);
// result=[a,b,c,d,e,f]，是Array1的一个副本，一个新数组。
// 这里的a，甚至可以是数组（在浏览器中可以解析）。

// 也可以像下面这样

var result=Array1.concat(Array2,Array3,"c");
// result=[a,b,c,d,e,f,"c"]
```
  
 
  
##### forEach()

用于让数组中每个元素都执行一次回调函数。
这个方法可以说是平时用的最多的了，不过，有些时候是属于滥用，我自己就因为对其他更方便的方法不了解，滥用 forEach() 去帮我处理数组。
简单介绍一下用法：
```
// array.forEach(function(currentValue, ?index, ?arr), ?thisValue)

var Array1 = [4, 9, 16, 25];
Array1.forEach(function(item,index){
  console.log("["+index+"]:"+item);
})
// 控制台输出
// [0]:4
// [1]:9
// [2]:16
// [3]:25
```
*注意*  
这个方法的返回值是 undefined，所以它不能进行链式操作之类的操作。而且这个方法在循环的过程中是无法终止的，如果想中途终止，不如用普通的循环操作。如果循环的目的是通过判断数组里的元素是否满足条件进而返回布尔值，不如改用 some() 或 every() 方法。


##### map()

用于让数组中每个元素都执行一次回调函数并返回新的数组。
这个方法平时用也挺多，和 forEach() 稍稍有点像，不同的就在于它会返回所有回调函数要求返回的对象。
简单介绍一下用法：
```
// array.map(function(currentValue,?index,?arr), ?thisValue)

var Array1 = [4, 9, 16, 25];
var Array1_doubled = Array1.map(function(item){
   return num * 2;
})
// Array1_doubled 数组的值为： [8, 18, 32, 50]
// Array1 数组未被修改： [4, 9, 16, 25]

```
map() 可以应用的操作也很多，可以做[扩展了解](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)，在平时的开发中多用，才能熟练。


##### every() VS some() includes()

上面这三个都是比对查找操作，有些类似，所以放在一起讲了。

不同的是，includes() 只能直接查找值，而 every() 和 some() 可以对数组中的元素进行更详尽的比对查找，可以用函数设置查找条件。

every() 和 some() 有点像 && 和 || 的关系

every() 有点像 &&，用于检测数组**所有元素**是否都符合指定条件（通过函数提供）。
- 如果数组中检测到有一个元素**不满足**，则整个表达式返回 false ，且剩余的元素不会再进行检测。
- 如果所有元素都满足条件，则返回 true。

而 some() 有点像 ||，用于检测数组中是否有满足指定条件的元素（通过函数提供）。
- 如果**有一个元素满足条件**，则表达式返回 true , 剩余的元素不会再执行检测。
- 如果没有满足条件的元素，则返回 false。

用法：
```
// arr.includes(要查找的值, ?从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。)
var site = ['runoob', 'google', 'taobao'];
site.includes('runoob'); // true 
site.includes('baidu'); // false


// every() 和 some() 这里只以some()举例

// array.some(function(当前元素的值,?当期元素的索引值,?当期元素属于的数组对象),?thisValue)

// 检测数组中是否有元素大于 18，只要有就返回 true

var ages = [3, 10, 18, 20];
console.log(ages.some(function (age) {
    return age >= 18;
}))

// 控制台输出 true

```

##### pop() push() VS shift() unshift()

这一组也放在一起讲。

pop() 和 push() 是在数组的末尾进行添加、删除元素的操作。

而shift() 和 unshift() 是在数组的头部进行添加、删除元素的操作。

其余的细节两组都一样，所以只以 pop() 和 push() 为例讲一讲。

pop() 方法用于删除数组的最后一个元素并返回删除的元素。会改变数组的长度

push() 方法用于在数组的末尾添加一个元素或多个元素，并返回数组的新长度。会改变数组的长度
用法：
```
// array.push(item1, item2, ..., itemX)

var Array1 = ["aa", "bb", "cc", "dd"];
Array1.push("ee","ff","gg");
console.log(Array1);

// 控制台输出["aa", "bb", "cc", "dd","ee","ff","gg"]

//array.pop()

var Array2 = ["aa", "bb", "cc", "dd"];
var a = Array2.pop();
console.log(a);  // 控制台输出 "dd"
console.log(Array2);  // 控制台输出["aa", "bb", "cc"]

```



##### filter()

顾名思义，filter() 算是一个过滤的方法，可以把源数组中符合条件的数据都放到一个新的数组中返回。
对于空数组不会执行，这个方法也不会改变源数组。
用法：
```
// 标准形式如下，各个参数的意义如上面 every() 和 some() 方法
// array.filter(function(currentValue,index,arr), thisValue)

var Array1 = [32, 33, 16, 40];
console.log(Array1.filter(function(ele){
   return ele >= 30;
}));

// 输出结果为: [32,33,40]

```

##### sort() VS reverse()

这两个方法都是对数组进行排序的方法，所以也放在一组讲。

reverse() 比较简单，是将原来的数组逆序，就不多说了。

而 sort() 可以按照多种方式排序，又稍微有点复杂，直接贴一个 [MDN关于这个方法的文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 吧，讲的更清楚一些




##### find() VS findIndex()

这两个都是查找元素操作。

find()返回的是满足条件（函数提供）的第一个元素，没有符合的返回 undefined。

而findIndex()返回的是满足条件（函数提供）的第一个元素的位置，没有符合的返回 -1。
对于空数组，它们都不会执行，这两个方法也不会改变数组的原始值。

用法：
```
// 标准形式如下，各个参数的意义如上面 every() 和 some() 方法
// array.find(function(currentValue, index, arr),thisValue)
// array.findIndex(function(currentValue, index, arr), thisValue)

var Array1 = [3, 19, 18, 20]; 
function condition(ele) {
    return ele >= 18;
}
console.log(Array1.find(condition));
// 控制台输出19

console.log(Array1.findIndex(condition));
// 控制台输出1

```


##### indexOf() VS lastIndexOf()

这两个方法也类似，一个是查找某元素第一次出现在数组中的位置，另一个是查找某元素最后一次出现在数组中的位置。这个不同也意味着 indexOf() 查找的时候是从数组头开始查找，而 lastIndexOf() 查找的时候是从数组尾开始查找。
如果没有符合的元素存在，则两者都返回 -1。

用法：
```
// array.indexOf(查找的元素,?开始查找的位置。默认是数组起始位置)

// array.lastIndexOf(查找的元素,?开始查找的位置。默认是数组的终止位置，一旦指定了这个值，相当于把数组截断从中间向前寻找元素最后一个出现的位置了)

var Array1 = ["Banana", "Orange", "Apple", "Mango", "Banana", "Orange", "Orange", "Apple"];
console.log(Array1.lastIndexOf("Apple", 4));

// 以最难的一个情况为例，控制台输出的是2，即从 Array1[4]向前查找，"Apple"最后出现的位置

```


##### slice()

slice用于从数组中截取需要的部分，并以新的对象返回，不会改变源数组。一般是对字符串处理的比较多。

用法：
```
// array.slice(?start, ?end)
// start 或 end 如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。
// 注意选取区间的变化，有以下三种情况

arr.slice();
// [0, end]

arr.slice(begin);
// [begin, end]

arr.slice(begin, end);
// [begin, end)

var Array1 = ["aa", "bb", "cc", "dd", "ee"];
var Array2 = Array1.slice(-3,-1);

// Array2 = ["cc", "dd"]
```
 

嗯，写的有点多，怕影响阅读体验。
其他还有一些平时用的频率没那么高的方法，下篇再写。
