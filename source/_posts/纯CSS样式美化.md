---
title: 纯CSS样式美化(滚动条/checkbox)
date: 2016-06-28 10:16:18
categories: 
  - 技术
  - CSS
tags: [CSS]
---
#### 兼容IE和Chrome浏览器滚动条CSS样式
<!-- more -->
IE CSS
```css
html,body {
scrollbar-face-color:#FB4446; /*滚动条3D表面（ThreedFace）的颜色*/ 
scrollbar-highlight-color:#fff; /*滚动条3D界面的亮边（ThreedHighlight）颜色*/ 
scrollbar-shadow-color:#eeeeee; /*滚动条3D界面的暗边（ThreedShadow）颜色*/ 
scrollbar-3dlight-color:#eeeeee; /*滚动条亮边框颜色*/ 
scrollbar-arrow-color:#000; /*滚动条方向箭头的颜色 */ 
scrollbar-track-color:#fff; /*滚动条的拖动区域(TrackBar)颜色*/
scrollbar-darkshadow-color:#fff; /*滚动条暗边框（ThreedDarkShadow）颜色*/ }
```
Chrome CSS
```css
/*---滚动条默认显示样式--*/  
::-webkit-scrollbar-thumb{  
   background-color:#FB4446;  
   height:50px;  
   outline-offset:-2px;  
   outline:2px solid #fff;  
   -webkit-border-radius:4px;  
   border: 2px solid #fff;  
}  
/*---鼠标点击滚动条显示样式--*/  
::-webkit-scrollbar-thumb:hover{  
   background-color:#F01360;  
   height:50px;  
   -webkit-border-radius:4px;  
}  
/*---滚动条大小--*/  
::-webkit-scrollbar{  
   width:8px;  
   height:8px;  
}  
/*---滚动框背景样式--*/  
::-webkit-scrollbar-track-piece{  
   background-color:#fff;  
   -webkit-border-radius:0;  
}
```
#### 纯CSS美化checkbox(方案1)

```css
.selectBetting{ 
   display: none; 
} 
.selectBetting + label { 
 background:$bgf8efce;
 border-radius:50%;
 border:1px solid $borb9aa77;
 width:$v25;
 height:$v25;
 display: inline-block; 
 position: relative; 
}  
 .selectBetting:checked + label { 
   background-color: $fontRed; 
   border:2px solid $fontRed;
} 
.selectBetting:checked + label::after { 
   font-family: "customfont";
   content: '\e616'; //勾选符号 
   position: absolute; 
   top: 50px;
   left: 0px; 
   color: white; 
   width: 100%; 
   text-align: center; 
   font-size: 1.4em; 
   padding: 1px 0 0 0; 
   vertical-align: text-top; 
} 
```
html
```html
<input type="checkbox" id="checkbox_sel" class="selectBetting" />
<label for="checkbox_sel" class=""></label>
```


#### 纯CSS美化checkbox(方案2)

```css

input[type="checkbox"]{
  -webkit-appearance: none;
  vertical-align:middle;
  margin-top:0;
  background:#fff;
  border: 1px solid #D9D9D9;
  border-radius: 2px;
  min-height: 15px;
  min-width: 15px;
  outline: none !important;
  position: relative;
}
input[type="checkbox"]:checked {
  background: #1890FF;
  border: 1px solid #1890FF;
}
input[type=checkbox]:checked::after{
  content: '';
  top: 2px;
  left: 2px;
  position: absolute;
  background: transparent;
  border: 2px solid #fff;
  border-top: none;
  border-right: none;
  height: 6px;
  width: 10px;
  -moz-transform: rotate(-45deg);
  -ms-transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

```

html
```html
<input type="checkbox" value="0" />
```

#### 纯CSS美化radio

##### 样式1

```css

label{
  line-height: 20px;
  display: inline-block;
  color: #777;
  outline: none;
}
.radio_type{
  width:17px;
  height: 17px;
  appearance:none;
  -moz-appearance:none;
  -webkit-appearance:none;
  outline: none !important;
  position: relative;
}
.radio_type:before{
  content: '';
  width: 17px;
  height: 17px;
  display: inline-block;
  border-radius: 50%;
  vertical-align: middle;
  border: 1px solid #D9D9D9;
}
.radio_type:checked:before{
  content: '';
  width: 17px;
  height: 17px;
  border: 1px solid #1890FF;
  display: inline-block;
  border-radius: 50%;
  vertical-align: middle;
}

.radio_type:checked:after{
  content: '';
  width: 9px;
  height: 9px;
  text-align: center;
  background: #1890FF;
  border-radius: 50%;
  display: block;
  position: absolute;
  top: 4px;
  left: 4px;
}

.radio_type:checked+label{*/
  color: #1890FF; 
}

```
##### 样式2

```css
label{
    line-height: 20px;
    display: inline-block;
    margin-left: 5px;
    margin-right:15px;
    color: #777;
}
.radio_type{
    width: 20px;
    height: 20px;
    appearance: none;
    position: relative;
}
.radio_type:before{
    content: '';
    width: 20px;
    height: 20px;
    border: 1px solid #7d7d7d;
    display: inline-block;
    border-radius: 50%;
    vertical-align: middle;
}
.radio_type:checked:before{
    content: '';
    width: 20px;
    height: 20px;
    border: 1px solid #c59c5a;
    background:#c59c5a;
    display: inline-block;
    border-radius: 50%;
    vertical-align: middle;
}
.radio_type:checked:after{
    content: '';
    width: 10px;
    height:5px;
    border: 2px solid white;
    border-top: transparent;
    border-right: transparent;
    text-align: center;
    display: block;
    position: absolute;
    top: 6px;
    left:5px;
    vertical-align: middle;
    transform: rotate(-45deg);
}
.radio_type:checked+label{
    color: #c59c5a;
}

```


```html

<input class="radio_type" type="radio" name="type" id="radio1" checked="checked"/> 
<label for="radio1">radio1</label>
<input class="radio_type" type="radio" name="type" id="radio2" /> 
<label for="radio2">radio2</label>

```

####  CheckBox 半选中状态

<input type='checkbox' />可以半选中，这个特性，很多浏览器都支持，包括Firefox，Chrome和IE

用 input.indeterminate 这个属性来获取或者设置半选中状态。

input.indeterminate = true; //设置成半选中

if(input.indeterminate) //用这个属性来判断是否半选中

选中和半选中input.checked都是true



#### select箭头美化

```css
select {
  /*Chrome和Firefox里面的边框是不一样的，所以复写了一下*/
  border: solid 1px #000;

  /*很关键：将默认的select选择框样式清除*/
  appearance:none;
  -moz-appearance:none;
  -webkit-appearance:none;

  /*在选择框的最右侧中间显示小箭头图片*/
  background: url("../img/report_arrow.png") no-repeat scroll right center transparent !important;

  /*为下拉小箭头留出一点位置，避免被文字覆盖*/
  padding-right: 14px;
}
```