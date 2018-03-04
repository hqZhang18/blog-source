---
title: D3-理解 Update、Enter、Exit
date: 2017-01-09 14:11:32
categories: 
  - 技术
  - D3.js
tags: D3
---

<code>Update</code>、 <code>Enter</code> 、<code>Exit</code> 是 D3 中三个非常重要的概念，它处理的是当选择集和数据的数量关系不确定的情况。<!--more-->
根据数组长度和元素数量的关系，分别把各种情况归纳如下：
* <code>updata</code>: 数组长度 = 元素数量
* <code>enter</code>: 数组长度 > 元素
* <code>exit</code> 数组长度 < 元素数量

##### Update 和 Enter 的使用
当对应的元素不足时 （ 绑定数据数量 > 对应元素 ），需要添加元素（append）。

现在 <code>body</code> 中有三个 p 元素，要绑定一个长度大于 3 的数组到 p 的选择集上，然后分别处理 <code>update</code> 和 <code>enter</code> 两部分。
```JavaScript
var dataset = [ 3 , 6 , 9 , 12 , 15 ];

//选择body中的p元素
var p = d3.select("body").selectAll("p");

//获取update部分
var update = p.data(dataset);

//获取enter部分
var enter = update.enter();

//update部分的处理：更新属性值
update.text(function(d){
    return "update " + d;
});

//enter部分的处理：添加元素后赋予属性值
enter.append("p")
    .text(function(d){
        return "enter " + d;
    });
```
结果如下图，<code>update</code> 部分和 <code>enter</code> 部分被绑定的数据很清晰地表示了出来。
![](/css/images/enterexit-3.png)
请大家记住：
* update 部分的处理办法一般是：更新属性值
* enter 部分的处理办法一般是：添加元素后，赋予属性值

#### Update 和 Exit 的使用

当对应的元素过多时 （ 绑定数据数量 < 对应元素 ），需要删掉多余的元素。

现在 <code>body</code> 中有三个 p 元素，要绑定一个长度小于 3 的数组到 p 的选择集上，然后分别处理 <code>update</code> 和 <code>exit</code> 两部分。

```JavaScript
var dataset = [ 3 ];

//选择body中的p元素
var p = d3.select("body").selectAll("p");

//获取update部分
var update = p.data(dataset);

//获取exit部分
var exit = update.exit();

//update部分的处理：更新属性值
update.text(function(d){
    return "update " + d;
});

//exit部分的处理：修改p元素的属性
exit.text(function(d){
        return "exit";
    });

//exit部分的处理通常是删除元素
// exit.remove();
```
结果如下，请大家区分好 <code>update</code> 部分和 <code>exit</code> 部分。这里为了表明哪一部分是 exit，并没有删除掉多余的元素，但实际上 exit 部分的绝大部分操作是删除。
![](/css/images/enterexit-4.png)
请大家记住：
* <code>exit</code> 部分的处理办法一般是：删除元素（remove）


