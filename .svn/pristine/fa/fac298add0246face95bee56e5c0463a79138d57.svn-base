---
title: react入门06-属性设置(props)
date: 2016-12-17 22:06:00
categories: 
  - 技术
  - React
tags: [react, props] 
---

props是组件自身的属性，一般用于嵌套的内外层组件中，负责传递信息（通常
是由父层组件向子层组件传递）
注意：props对象中的属性与组件的属性一一对应，不要直接去修改prpos中属性的值

定义一个组件WebShow。功能：输出网站的名字和网址，网址是一个可以点击的链接
分析：定义一个组件WebName负责输出网站名字，定义组件WebLink显示网站的网址，并且可以点击

思路：
1.给WebShow设置两个属性，wname,wlink
2.WebShow的props对象增加了两个属性值
3.WebName从WebShow的props对象中获取wname的值，即网站的名字，<!--more-->  
```javascript
//定义WebName组件
 var WebName = React.createClass({
   render: function(){
     return <h1>{this.props.webname}</h1>
   }
 })

 //定义WebLink组件
 var WebLink = React.createClass({
   render: function(){
     return <a href={this.props.weblink}>{this.props.weblink}</a>
   }
 })

 //定义WebShow组件
 var WebShow = React.createClass({
   render: function(){
     return (
       <div>
         <WebName webname = {this.props.wname} />
         <WebLink weblink = {this.props.wlink} />
       </div>
     )
   }
 })

//渲染
ReactDOM.render(
	<WebShow wname = '百度' wlink = 'http://www.baidu.com' />,
	document.getElementById('container')
)
```
...this.props
props提供的语法糖，可以将父组件中的全部 属性都复制给子组件
需求：定义一个组件Link,Link组件中只包含一个< a >, 我们不给< a >设置任何属性所有属性全部从父组件复制得到
 ```javascript
var Link = React.createClass({
	render: function(){
		return <a {...this.props}>{this.props.name}</a>
	}
})

//渲染
ReactDOM.render(
	<Link name='百度' href='http://www.baidu.com' />,
	document.getElementById('container')
)
```

