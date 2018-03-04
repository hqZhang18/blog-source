---
title: JS循环遍历
date: 2017-02-10 21:58:16
categories: 
  - 技术
  - JavaScript
tags: 循环遍历
---

通过Ajax请求后端接口，获得json数据后前端进行解析遍历再渲染页面，这是前端人员经常要做的工作，今天就来说说在循环遍历json数据的时候，几种常用的方法。
<!-- more -->

先设定一个功能场景如下:
html
```html
<ul class="target">
  <li></li>
  <li></li>
  <li></li>
</ul>
<button class="btn">click me</button>
```

点击按钮后，给三个li元素添加内容；

js如下：

```javascript
var data = [{
      name: 'aaa',
      sex: 'boy'
    },{
      name: 'bbb',
      sex: 'girl'
    },{
      name: 'ccc',
      sex: 'boy'
    }]
$(function() {
  $(".btn").click(function(){

    //一、传统for循环
    // for(var i = 0;i < data.length;i++){
    //   $(".target li:eq(" + i + ")").html(data[i].name + data[i].sex);
    // }

    //二、for-in循环
    // for(var i in data){
    //   $(".target li:eq(" + i + ")").html(data[i].name + data[i].sex);
    // }

    //三、$.each()
    // $.each(data,function(key,val){
    //   $(".target li:eq(" + key + ")").html(data[key].name + data[key].sex );
    // }) 

    //$.each()的ES6写法
    //$.each(data,(key,val) =>$(".target li:eq(" + key + ")").html(data[key].name + data[key].sex ))
   
    //四、使用map()
    // data.map(function(val, index){
    //   $(".target li:eq(" + index + ")").html(val.name + val.sex );
    // })

    //map()的ES6写法
    data.map((val,index) =>$(".target li:eq(" + index + ")").html(val.name + val.sex ))

  })
})

```

将一个字符循环 N 遍
```javascript
function repeat(value,n){
  new Array(n+1)).join(value)) 
}

```
设计思路，利用数组的 join 连接方法，达到循环 n 遍的逻辑 为什么是 N + 1 ？ new Array(10) 会创建一个数组长度为 10 的数组 但是元素与元素之间的链接只有 9 个, 所以上面是 N + 1