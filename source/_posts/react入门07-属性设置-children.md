---
title: react入门07-属性设置-children
date: 2016-12-17 22:06:00
categories: 
  - 技术
  - React
tag: react
---
this.props.children
children是一个例外，不是跟组件的属性对应的
表示组件的所有子节点
HTML中有一种标签：列表 < ul > < ol > < li >
定义一个列表组件，列表项中显示的内容，以及列表项的数量都由外部决定<!--more-->  
 
```javascript
var ListComponent = React.createClass({
  render: function(){
    return (
      <ul>
        {
          /*
            列表项的数量以及内容不确定，在创建模板时才能确定
            利用this.props.children从父组件获取需要展示的列表项内容
            
            获取到列表项内容后，需要遍历children，逐项进行设置
            使用React.Children.map方法
            返回值：数组对象，这里数据组中的元素是<li>
          */
        
          React.Children.map(this.props.children, function(child){
            //child是遍历得到父组件的子节点
            return <li>{child}</li>
          })
        } 
      </ul>
    )
  }
})

//渲染
ReactDOM.render(
  (
    <ListComponent>
      <h1>百度</h1>
      <a href="www.baidu.com">www.baidu.com</a>
    </ListComponent>  
  ),
  document.getElementById('container')
)
```
<!--more-->  
