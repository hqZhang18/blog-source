---
title: react入门08-state
date: 2016-12-21 13:29:35
categories: 
  - 技术
  - React

tags: react
---

  事件处理
  react中的事件名称首字母小写，驼峰命名法
  案例：定义一个组件，组件中包含一个button，给button绑定onClick事件
<!--more--> 



```javascript
var MyButton = React.createClass({
handleClcik: function(){
	console.log('tst')
},

render: function(){
	return (
		<button onClick={this.handleClcik}>{this.props.buttonTitle}</button>
	)
}
})	
//渲染
ReactDOM.render(
<MyButton buttonTitle='按钮' />,
document.getElementById('container')
)

```

  state 状态
  props 组件自身的属性
  this.state
  需求：创建一个CheckButton组件，包含一个checkbox类型< input >
  复选框在选中和未选中的两种状态下会显示不同的文字，退根据状态渲染


```javascript
var CheckButton = React.createClass({
getInitialState: function() {
  return {
  	//在这个对象中设置的属性将会存储在state中
		//默认状态，未选中
  	isCheck: false
  }
},

//定义事件绑定的方法
handleClick: function(event) {
  this.setState({
  	//修改状态值，通过this.state读取设置的状态值
  	isCheck: !this.state.isCheck
  })
},
render: function() {
	//根据状态值，设置显示的文字
 	//在JSX语法中，不能直接使用if,使用三目短运算符
  var text = this.state.isCheck ? '已选中' : '未选中';
  return (
  <div>
   <input type="checkbox" onChange={this.handleClick} />
   {text}
   </div>
  );
}
});

//渲染
ReactDOM.render(
<CheckButton />,
document.getElementById('container')
);

```



