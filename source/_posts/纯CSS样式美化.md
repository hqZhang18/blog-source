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
#### 纯CSS美化checkbox

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