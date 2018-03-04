---
title: react入门04-组件样式
date: 2016-12-17 22:06:11
categories: 
  - 技术
  - React
tags: react 
---


设置组件的样式，讲解三种：
1.内联样式
2.对象样式
3.选择器样式
<!--more-->  注意：在React和HTML中设置样式时的书写格式是有区别的
* 1.HTML以；结尾
*   React以,结尾
* 2.HTML中key、value都不加引号
*   React中属于JavaScript对象，key的名字不能出现'-'，需要使用驼峰命名法.如果value为
* 	  字符串，需要加引号
* 3.HTML中，value如果是数字，需要带单位
*   React中不需要带单位

##### 定义一个组件类，同时使用三种设置组件样式的方式
* 需求：定义一个组件，分为上下两行显示内容
* < div>  内联样式：设置背景颜色，边框大小，边框颜色
* < h1>  < /h1> 对象样式：设置背景颜色，字体颜色
* < p>< /p> 选择器样式： 设置字休大小
* 注意：在React中使用选择器样式设置组件样式时，属性名不能使用class使用className替换
* 类似的：使用htmlfFor替换for

```css
.pStyle {
  font-size: 24px;
}
```
```javascript
var hStyle = {
  backgroundColor: '#efe',
  color: 'red'
}

var ShowMessage = React.createClass({
  render: function(){
  return (
      <div style = {{backgroundColor:'yellow', borderWidth:5, borderColor: '#ccc', borderStyle: 'solid'}}>
        <h1 style = {hStyle}>{this.props.firstRow}</h1>
        <p className = 'pStyle'>{this.props.secondRow}</p>
      </div>
    )
  }	
})

ReactDOM.render(
  <ShowMessage firstRow = 'Hello' secondRow = 'React' />,
  document.getElementById('container')
)

```
 