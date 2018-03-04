---
title: react入门01-创建React工程
date: 2016-12-17 22:06:11
categories: 
  - 技术
  - React
tags: react
---
 
创建一个React Dome<!--more-->   
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>react入门01-创建React工程</title>
    <!--react.js是React的核心库-->
    <script src="js/react.js"></script>
    <!--react-dom.js的作用是提供与DOM相关的功能-->
    <script src="js/react-dom.js"></script>
    <!--browser.min.js的作用是将JSX语法转换成javaScript语法-->
    <script src="js/browser.min.js"></script>
  </head>
  <body>
    <!--React渲染的模板内容会插入到这个DOM节点中，作为一个容器-->
    <div id="container"></div>
  </body>

  <!--在React开发中，使用JSX，跟JavaScript不兼容，在使用JSX的地方，
要设置type: text/babel-->
  <!--babel是一个转换编译器，在ES6转成可以在浏览器中运行代码-->
  <script type="text/babel">
    // 在此编写React代码
    // 需求： 渲染一行标题，显示'Hello React'
    /*
      ReactDOM.render()
      React的最基本方法，用于将模板转换成HTML语言，渲染DOM,并插入指定的DOM节点中

      3个参数
      第一个：模板的渲染内容(HTML形式)
      第二个：这段模板需要插入的DOM节点(本程序中，是id为container的div节点)
      第三个：渲染后的回调，一般不用

     */

    ReactDOM.render(
      <h1>Hello React</h1>,
      document.getElementById('container')
    )

  </script>
</html>
```
<!--more--> 

 