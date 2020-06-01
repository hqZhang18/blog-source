---
title: JavaScript_MV* 模式
date: 2019-12-03 16:44:47
categories: 
  - 技术
  - JavaScript
tags: MV* 模式
---


MVC (Model(模型)-View(视图)-Controller(控制器)), MVP (Model(模型)-View(视图)-Presenter(中介者)) 以及 MVVM (Model(模型)-View(视图)-ViewModel(视图模型))。过去，这些模式已经被大量用于构建桌面和服务器端的应用程序，但它只是在最近几年才被应用到JavaScript。

由于目前大多数JavaScript开发人员选择使用Backbone.js一类的库实现的MVC/MV* 架构来实现这些模式，我们将来比较一下它们和传统的实现对于MVC的不同解释。
<!--more-->

#### MVC
MVC是一个架构设计模式，它通过分离关注点的方式来支持改进应用组织方式。它促成了业务数据(Models)从用户界面(Views)中分离出来，还有第三个组成部分(Controllers)负责管理传统意义上的业务逻辑和用户输入。该模式最初是由Trygve Reenskaug在研发Smalltalk-80 (1979)期间设计的，当时它起初被称作Model-View-Controller-Editor。在1995年的“设计模式: 面向对象软件中的可复用元素” (著名的"GoF"的书)中，MVC被进一步深入的描述，该书对MVC的流行使用起到了关键作用。