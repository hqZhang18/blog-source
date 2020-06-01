---
title: JavaScript_设计模式系列 - 观察者模式
date: 2019-12-02 14:45:25
categories: 
  - 技术
  - JavaScript
tags: 观察者模式
---

#### 概要：
相信大家都用过鼠标悬停，按键等事件，其实他们就是观察者模式的例子。说重点，<strong>这种模式的实质就是你可以对程序中的某个对象的状态进行观察，并且在其发生改变时能够得到通知。</strong>

<!--more-->
#### 角色：
观察者模式中存在两种角色：观察者和被观察者，也可以叫做发布者和订阅者。

#### 作用：
例如，你在你每个阶段，进行到一定阶段的时候，就要做一些事情，就可以利用观察者模式做一些相应的处理，不过多解释了。

#### 详解：
观察者模式中，并不是一个对象调用另一个对象的方法，而是一个对象订阅另一个对象的特定活动并在状态改变后获得通知。当发生了一个重要的事件时，发布者将会通知所有订阅者并且可能经常以事件对象的形式传递消息。

#### 示例
为了加深理解，让我们来看一个具体的例子，有三个报纸出版社，报社一、报社二、报社三，有两个订报人，分别是:订阅者1，订阅者2。在这里出版社就是被观察者，订报人就是观察者

##### 被观察者
```javascript
  //观察者模式：对程序中某一个对象的进行实时的观察，当该对象状态发生改变的时候 进行通知
  //被观察者
  var Publish = function (name) {
    this.name = name;
    this.subscribers = []//数组中存着所有的订阅者(出版社名单)，数组的元素都是函数类型
  }
  //publish的实例对象去发布消息的方法
  Publish.prototype.deliver = function (news) {
    var publish = this;//this就代表报社
    this.subscribers.forEach(function (item) {
        //循环subscribers数组中所有的订报人，为他们发布内容。
        item(news,publish);//每个订阅者都收到了新闻（news），还有来自哪家报刊
    })
    return this;//为了方便，采用链式调用。
  }

``` 

##### 观察者
订阅功能

```javascript
  //订阅者的方法,每一个订阅者都是一个函数,在函数原型上扩展一个方法
  Function.prototype.subscribe = function (publish) {//出版社形参
    var sub = this;//取得当前订阅者这个人
    //不能同时订一家出版社同一份报纸,没意义
    //publish.subscribers//张三，李四，王五，名字可能重复
    //publish.subscribers数组里面有的人，不能再订阅
    //我们使用ecma5里面的some方法，循环遍历数组的每一个元素，执行一个函数，如果有相同的名字则返回true，不相同则返回false
    var alreadExists = publish.subscribers.some(function (item) {
        return item === sub;
    })
    //如果出版社名单没有这个人，则加入其中
    if(!alreadExists){
        publish.subscribers.push(sub);
    }
    return this;//为了方便，采用链式调用。
  }  

``` 

取消订阅
```javascript
  //具体的一个订阅者去取消订阅报纸的方法
  Function.prototype.unsubscribe = function(publish){
    var sub = this;//取得当前订阅者这个人
    // filter (过滤函数:循环便利数组的每一个元素，执行一个函数如果不匹配，则删除该元素)
    publish.subscribers = publish.subscribers.filter(function(item){
        return item !== sub ;
    });
    return this;//为了方便，采用链式调用。
  };
``` 

好了，上面就已经做好了基本的准备的，我们来做个小demo
```javascript
  //实例化发布者对象(报社对象)
  var pub1 = new Publish('报社一');
  var pub2 = new Publish('报社二');
  var pub3 = new Publish('报社三');

//观察者
  var sub1 = function (news,pub) {
    console.log(arguments);
    document.getElementById('sub1').innerHTML += pub.name + news + '\n'
  }
  var sub2 = function (news,pub) {
    document.getElementById('sub2').innerHTML += pub.name + news + '\n'
  }
  var p1 = document.getElementById('pub1')
  var p2 = document.getElementById('pub2')
  var p3 = document.getElementById('pub3')
  //执行订阅方法
  sub1.subscribe(pub1).subscribe(pub2).subscribe(pub3)
  sub2.subscribe(pub1).subscribe(pub2).subscribe(pub3)

  // 事件绑定
  p1.onclick = function () {
    pub1.deliver(document.getElementById('text1').value, pub1);
  }
  p2.onclick = function () {
    pub2.deliver(document.getElementById('text2').value, pub2);
  }
  p3.onclick = function () {
    pub3.deliver(document.getElementById('text3').value, pub3);
  }
  sub1.unsubscribe(pub1); //取消订阅 
```

我们来看看html代码段
```html
<div class="col-lg-8">
  <div class="input-group">
    <span id="pub1" class="input-group-addon">
      报社一
    </span>
      <input v-model="user.name" type="text" class="form-control"  id="text1">
  </div>
</div>
<div class="col-lg-8">
  <div class="input-group">
    <span id="pub2" class="input-group-addon">
      报社二
    </span>
      <input v-model="user.name" type="text" class="form-control"  id="text2">
  </div>
</div>
<div class="col-lg-8">
  <div class="input-group">
    <span id="pub3" class="input-group-addon">
      报社三
    </span>
      <input v-model="user.name" type="text" class="form-control"  id="text3">
  </div>
</div>

<div class="col-lg-8">
  订阅者一
  <textarea id="sub1" class="form-control" rows="5"></textarea>
  订阅者二:
  <textarea id="sub2"class="form-control" rows="5"></textarea>
</div>
```