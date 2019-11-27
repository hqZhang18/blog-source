---
title: 前端经验总结(CSS)
date: 2018-03-04 16:52:40
categories: 
  - 技术
tags: javascript
---


将一些很小的但又很常用的知识点汇总到一起，方便以后查阅
<!-- more -->

##### 1.如何修改input的placeholder？

```css
::-webkit-input-placeholder { /* WebKit, Blink, Edge */
    color:    #909;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
   color:    #909;
   opacity:  1;
}
:-moz-placeholder { /* Mozilla Firefox 19+ */
   color:    #909;
   opacity:  1;
}
:-ms-input-placeholder { /* Internet Explorer 10-11 */
   color:    #909;
}
::-ms-input-placeholder { /* Microsoft Edge */
   color:    #909;
}
```

##### 2 如何修改滚动条默认样式
```ccc
//滚动条整体样式
.container::-webkit-scrollbar {
    width: 3px;
    height: 6px;
}

//滚动条轨道样式
.container::-webkit-scrollbar-track: {
    background-color: #fff;
}

//滚动条滑块的样式
.container::-webkit-scrollbar-thumb {
    background-color: rgba(0, 0, 0, 0.6);
    border-radius: 20%;
}

//滚动条上下按钮的样式
.container::-webkit-scrollbar-button {
    background-color: #888;
    display: none;
}

//两个滚动条交叉处的样式
.container::-webkit-scrollbar-corner {
    background-color: black;
}
```

##### 3.修改checkbox默认样式
```css
  .selectBetting{ 
    display: none; 
  } 
  .selectBetting + label { 
    background: url(../images/checkbox.png) no-repeat;
    width: 64px;
    height: 64px;
    display: inline-block; 
    float: left;
    cursor: pointer;
  }  
  .selectBetting:checked + label { 
    background: url(../images/checkbox.png) no-repeat;
  } 
  .selectBetting:checked + label::after { 
    content: '√';  
    float: left;
    font-family: "customfont";
    color: #6be9ff; 
    width: 100%; 
    text-align: center; 
    font-size: 32px;
    padding: 10px 0 0 0px;
    vertical-align: text-top; 
  }
```

```html
<input type="checkbox" id="checkbox_sel" class="selectBetting" />
<label for="checkbox_sel" class=""></label>
```

#### 4.使用CSS3动画导致页面抖动
###### 问题描述
使用digitroll插件导致页面抖动 ,该插件是一个数字滚动效果

###### 问题原因
效果使用css3动画制作，但是动画会导致页面抖动闪屏

###### 解决方案
使用到动画的样式设置如下样式，可解决
```css
-webkit-backface-visibility: hidden;（设置进行转换的元素的背面在面对用户时是否可见：隐藏）
// 如果有3d加上下面句 ，没有可省略
-webkit-transform-style: preserve-3d; （设置内嵌的元素在 3D 空间如何呈现：保留 3D ）
```

eg:
```css
.num {
  -webkit-backface-visibility: hidden
}
```

##### 使用 digitroll数字滚动插件,给数字加逗号(3位数分隔)


##### 3.D3图表中如何让文字竖着显示

```javascript
var svg = d3.select('body')
        .append('svg')
        .attr('width', 100)
        .attr('height', 100)
        .style('padding', '20px')

svg.append('text')
  .text('文字竖着显示')
  .style('writing-mode','tb-rl')
  .attr('textLength', 90) //文字间距
```
#### 盒子垂直水平居中
- 1、定位 盒子宽高已知， position: absolute; left: 50%; top: 50%; margin-left:-自身一半宽度; margin-top: -自身一半高度;
- 2、table-cell布局 父级 display: table-cell; vertical-align: middle; 子级 margin: 0 auto;
- 3、定位 + transform ; 适用于 子盒子 宽高不定时； （这里是本人常用方法）

```css
div {
  position: relative / absolute;
  /*top和left偏移各为50%*/
  top: 50%;
  left: 50%;
  /*translate(-50%,-50%) 偏移自身的宽和高的-50%*/
  transform: translate(-50%, -50%); 注意这里启动了3D硬件加速哦 会增加耗电量的 （至于何是3D加速 请看浏览器进程与线程篇）
}
```

- 4、flex 布局

```css
父级： 
div{
  /*flex 布局*/
  display: flex;
  /*实现垂直居中*/
  align-items: center;
  /*实现水平居中*/
  justify-content: center;
}
```
