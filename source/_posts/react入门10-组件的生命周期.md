---
title: react入门10-组件的生命周期
date: 2016-12-21 15:35:04
categories: 
  - 技术
  - React
tags: [react, 生命周期]
---



生命周期介绍
1.组件的生命周期可分为三个状态：

<code>Mounting</code>: 组件挂载，已插入真实 DOM

<code>Updataing</code>: 组件更新，正在被重新渲染
<code>Unmounting</code>: 组件移出，已经移出真实 DOM<!--more-->


2.组件的生命周期可分为四个阶段:
创建、实例化、更新、销毁


3.网易新闻列表页面

1.Mounting/组件挂载相关：

(1) <code>componentWillMount</code>

组件将要挂载。在render之前执行，但仅执行一次，即使多次重复渲染该组件，或者改变了组件的<code>state</code>
(2) <code>componentDidMount</code>
组件已经挂载。在render之后执行，同一个组件重复渲染只执行一次

<p></p>
2.<code>Updataing</code>/组件更新相关

(1) <code>componentWillReceiveProps</code>(object nextProps)

已加载组件收到新的props之前调用，注意组件初始化渲染时则不会执行

(2) <code>shouldComponentUpdate</code> (object nextProps, object nextState)

组件判断是滞重新渲染时调用。该接口实际是在组件接收到了新的 props 或者新的<code>state</code>的时候 会立即调用，
然后通过返回

(3) <code>componentWillUpdata</code>(object nextProps, object nextState)
组件将要更新

(4) <code>componentDidUpdata</code>(object prevProps, object prevState)
组件已经更新


3.<code>Unmounting</code>/组件移除相关	

(1) <code>componentWillUnmout</code>

在组件要被移除之前的时间点触发，可以利用该方法执行一些必要的清理组件将要移除


4.生命周期中与<code>props</code>和<code>state</code>相关

(1) <code>getDefaultProps</code> 设置props属性默认值

(2) <code>getInitialState</code> 升值state属性初始值


```javascript
//生命周期各阶段介绍
var Demo = React.createClass({
  /*
   一、创建阶段
   流程：只调用getDefaultProps方法
 */

  getDefaultProps: function() {
    //创建类的时候被调用，设置this.prpos的默认值
    console.log('getDefaultProps')
    return {}
  },

  /*
	二、实例化阶段
     流程：
     getInitalState
     componentWillMount
     render
     componentDidMount
  */

  getInitialState: function() {
    //设置this.state的默认值
    console.log('getInitalState')
    return null
  },
  componentWillMount: function() {
    //在render之前调用
    console.log('componentWillMount')
  },
  render: function() {
    //渲染并返回一个虚拟DOM
    console.log('render')
    return <div>Hello React</div>
  },

  componentDidMount: function() {
    //在render之后调用
    //在该方法中，React会使用render方法返回的虚拟DOM对象创建真实的DOM结构
    console.log('componentDidMount')
  },

  /*
	三、更新阶段
     流程：
     componentWillReceiveProps
     shouldComponentUpdate  如果返回值是false 后三个不执行
     componentWillUpdate
     render
     componentDidUpata
  */
  componentWillReceiveProps: function() {
    console.log('componentWillReceiveProps')
  },
  shouldComponentUpdate: function() {
    //是否需要更新
    console.log('shouldComponentUpdate')
    return true
  },
  componentWillUpdate: function() {
    console.log('componentWillUpdate')
  },
  componentDidUpata: function() {
    console.log('componentDidUpata')
  },

  /*
 四、销毁阶段
 流程： 
 componentWillUnmount
 */
  componentWillUnmount: function() {
    console.log('componentWillUnmount')
  }
})
//第一次创建并加载组件
ReactDOM.render(
  <Demo />,
  document.getElementById('container')
)
//更新渲染组件
ReactDOM.render(
  <Demo />,
  document.getElementById('container')
)
//移出组件
ReactDOM.unmountComponentAtNode(document.getElementById('container'))
```

