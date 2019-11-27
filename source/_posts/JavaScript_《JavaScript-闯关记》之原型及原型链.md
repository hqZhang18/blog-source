---
title: 《JavaScript 闯关记》之原型及原型链
date: 2016-12-21 22:29:28
categories: 
  - 技术
  - JavaScript
tags: [JavaScript, 原型链]
toc: true
---


原型链是一种机制，指的是 JavaScript 每个对象都有一个内置的 <code>__proto__</code> 属性指向创建它的构造函数的 prototype（原型）属性。原型链的作用是为了实现对象的继承，要理解原型链，需要先从函数对象、constructor、new、prototype、__proto__ 这五个概念入手。
<!--more-->
### 函数对象

前面讲过，在 JavaScript 里，函数即对象，程序可以随意操控它们。比如，可以把函数赋值给变量，或者作为参数传递给其他函数，也可以给它们设置属性，甚至调用它们的方法。下面示例代码对「普通对象」和「函数对象」进行了区分。

普通对象：
```javascript
var o1 = {};
var o2 = new Object();
```
### 函数对象：
```javascript
function f1(){};
var f2 = function(){};
var f3 = new Function('str','console.log(str)');
```
简单的说，凡是使用 function 关键字或 Function 构造函数创建的对象都是函数对象。而且，只有函数对象才拥有 prototype （原型）属性。

constructor 构造函数

函数还有一种用法，就是把它作为构造函数使用。像 Object 和 Array 这样的原生构造函数，在运行时会自动出现在执行环境中。此外，也可以创建自定义的构造函数，从而自定义对象类型的属性和方法。如下代码所示：
```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
        console.log(this.name);
    };
}

var person1 = new Person("Stone", 28, "Software Engineer");
var person2 = new Person("Sophie", 29, "English Teacher");
```
在这个例子中，我们创建了一个自定义构造函数 Person()，并通过该构造函数创建了两个普通对象 person1 和 person2，这两个普通对象均包含3个属性和1个方法。

你应该注意到函数名 Person 使用的是大写字母 P。按照惯例，构造函数始终都应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头。这个做法借鉴自其他面向对象语言，主要是为了区别于 JavaScript 中的其他函数；因为构造函数本身也是函数，只不过可以用来创建对象而已。

