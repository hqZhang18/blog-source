---
title: React Router 4 简易入门
date: 2019-06-28 09:46:28
categories: 
  - 技术
  - React
tags: [react-router]
---

##### 安装
React Router被拆分成三个包：react-router,react-router-dom和react-router-native。react-router提供核心的路由组件与函数。其余两个则提供运行环境（即浏览器与react-native）所需的特定组件。
<!--more-->
进行网站（将会运行在浏览器环境中）构建，我们应当安装react-router-dom。react-router-dom暴露出react-router中暴露的对象与方法，因此你只需要安装并引用react-router-dom即可。

```javascript
npm install --save react-router-dom
```

#### 路由器(Router)
 在你开始项目前，你需要决定你使用的路由器的类型。对于网页项目，存在<BrowserRouter>与<HashRouter>两种组件。当存在服务区来管理动态请求时，需要使用<BrowserRouter>组件，而<HashRouter>被用于静态网站。

通常，我们更倾向选择<BrowserRouter>，但如果你的网站仅用来呈现静态文件，那么<HashRouter>将会是一个好选择。

对于我们的项目，将设将会有服务器的动态支持，因此我们选择<BrowserRouter>作为路由器组件。

#### 路径(Path)

<Route>接受一个数为string类型的path，该值路由匹配的路径名的类型。例如：<Route path='/roster'/>会匹配以/roster[注2]开头的路径名。在当前path参数与当前location的路径相匹配时，路由就会开始渲染React元素。若不匹配，路由不会进行任何操作[注3]。

```javascript
<Route path='/roster'/>
// 当路径名为'/'时, path不匹配
// 当路径名为'/roster'或'/roster/2'时, path匹配
// 当你只想匹配'/roster'时，你需要使用"exact"参数
// 则路由仅匹配'/roster'而不会匹配'/roster/2'
<Route exact path='/roster'/>

```




