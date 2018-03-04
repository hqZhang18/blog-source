---
title: react入门02-JSX语法
date: 2016-12-17 22:06:11
categories: 
  - 技术
  - React
tags: [React, JSX]
---
 JSX入门
 JSX不是一门新的语言，是个语法（语法糖）

 1.JSX必须借助React环境运行

 2.JSX标签其实就是HTML标签，只不过我们在JavaScript中书写这些标签的时候，不用使用""括起来，可以向XML一样书写

 3.转换JSX语法能够让我们更直观的看到组件的DOM结构，不能直接在浏览器上运行最终会转化成JavsScript代码在浏览器上运行  

 4.在JSX中运行JavaScript代码。使用 {} 括起来 {表达式}

 5.例如：属性、设置样式、事件绑定等
<!--more--> 

```javascript
    ReactDOM.render(
      React.createElement('h1', null, 'Hello React'),
      document.getElementById('container')
    )
    
    var text = 'Hello React 表达式';
    ReactDOM.render(
      <h1>{text}</h1>,
      document.getElementById('container')
    )

```
 