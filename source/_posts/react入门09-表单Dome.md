---
title: react入门09-表单Dome
date: 2016-12-21 13:29:35
categories: 
     - 技术
     - React
tags: react
---

在输入框输入的内容进行实时显示
分析： 组件与用户交互过程中，存在状态的变化，即输入框的值
<!--more--> 



```javascript
var Input = React.createClass({
     	getInitialState: function() {
     		return {
     			value: '请输入'
     		}
     	},
     	
     	handleChange: function(event) {
     		//通过event.target.value读取用户输入的值
     		this.setState({
     			value: event.target.value
     		})
     	},
     	render: function() {
     		let value = this.state.value
     		return (
     			<div>
     				<input type='text' value={value} onChange={this.handleChange} />
     				<p>{value}</p>
     			</div>
     		)
     	}
     })
     
     ReactDOM.render(
     	<Input />,
     	document.getElementById('container')
     )
```



