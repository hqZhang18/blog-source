---
title: apply call bind使用详解
date: 2016-06-28 21:58:16
categories: 
  - 技术
  - JavaScript
tags: 循环遍历
---


```javascript
vvar obj = {
  "loca" : "中国",
  "tel" : "小米",
  "money" : "100万"
};

<!-- more -->

function User(name,age){
  this.name = name;
  this.age = age;
  return this;
}

var user = new User("张三","20");
console.log(user);

function User2(name,age,sex){
  //User.apply(this,[name,age]);
  //this === obj
  User.call(this,name,age);
  this.sex = sex;
  return this;
};

var user2 = new User2("李四","30","男");
console.log(user2);

// bind 会改变函数体中的 this 对象
//变为你传递进去的对象
var user3 = User2.bind(obj)("王五","40","男");

console.log(user3);

```
