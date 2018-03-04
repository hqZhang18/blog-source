---
title: react入门05-复合组件
date: 2016-12-17 22:06:00
categories: 
  - 技术
  - React
tags: react 
---


复合组件也被称为组合组件，创建多个组件合成一个组件
定义一个组件WebShow。功能：输出网站的名字和网址，网址是一个可以点击的链接
分析：定义一个组件WebName负责输出网站名字，定义组件WebLink显示网站的网址，并且可以点击<!--more--> 
```javascript
//定义WebName组件
var WebName = React.createClass({
	render: function(){
	return <h1>百度</h1>
}
})

//定义WebLink组件
var WebLink = React.createClass({
	render: function(){
		return <a href='http://www.baidu.com'>http://www.baidu.com</a>
	}
})

//定义WebShow组件
var WebShow = React.createClass({
render: function(){
return (
  <div>
  	<WebName />
  	<WebLink />
  </div>
)
}
})
ReactDOM.render(
	<WebShow />,
	document.getElementById('container')
)
```

 