---
title: react入门03-定义组件
date: 2016-12-17 22:06:11
categories: 
  - 技术
  - React
tags: react
---

##### 创建一个组件类，用于输出Hello React

1.React中创建的组件类以大写字母开头，驼峰命名法;
2.在React中使用React.createClass方法创建一个组件类
3.核心代码：每个组件类必须实现自己的render方法。输出定义好的组件模板。返回值:null, false, 组件模板
<!--more-->  

```javascript
      var HelloMessage = React.createClass({
            render: function(){
            return <h1>定义组件</h1>
            }
      })

      ReactDOM.render(
            //在模板中插入<HelloMessage /> 会自动生成一个实例
            <HelloMessage />,
            document.getElementById('container')
      )
```

 