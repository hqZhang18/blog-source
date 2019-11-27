---
title: IE中的CSS3不完全兼容解决方案
date: 2016-12-22 09:17:05
tags: CSS3
categories: 
  - 技术
  - CSS
tag: CSS3
---

1.Opacity透明度
元素的透明度在IE中可以很方便的用滤镜来实现。
<!--more-->
```css
background-color:green;
opacity: .4;
filter:progid:DXImageTransform.Microsoft.alpha(opacity=40);
```
2.border-radius圆角/Box Shadow盒阴影/Text Shadow文字阴影
在IE中可以利用Vector Markup Language (VML)和javascript来实现这些效果，参见IE-CSS3，在引用了一个HTC文件后，在IE浏览器中就可以使用这三种CSS3属性了。
```css
-moz-border-radius: 15px; 
-webkit-border-radius: 15px; 
border-radius: 15px; 
-moz-box-shadow: 5px 5px 5px #000; 
-webkit-box-shadow: 5px 5px 5px #000; 
box-shadow: 5px 5px 50px #000; 
behavior: url(ie-css3.htc); 
```
单独设置，确实有效，不知道为什么在项目中这么设置文件一多，就老报错。

在IE中有滤镜来实现阴影(shadow)和投影(drop-shadow)效果的
```css
filter: progid:DXImageTransform.Microsoft.Shadow(color='#000000', Direction=145, Strength=10);
filter:progid:DXImageTransform.Microsoft.DropShadow(Color="#6699CC",OffX="5",OffY="5",Positive="1");
```
IE中的渐变滤镜
```css
background: linear-gradient(top, #444444, #999999); 
background: -moz-linear-gradient(top, #444444, #999999); 
background: -webkit-gradient(linear,left top,left bottom,color-stop(0, #444444),color-stop(1, #999999)); 
filter:progid:DXImageTransform.Microsoft.gradient(startColorStr='#444444', EndColorStr='#999999'); 
```
渐变滤镜支持RGBA的颜色，startColorStr和EndColorStr的前两位是Alpha通道值。使用带alpha通道来模拟RGBA颜色背景的同时，应该去掉其back
ground-color属性。
```css
background-color: rgba(0, 255, 0, 0.6); 
filter:progid:DXImageTransform.Microsoft.gradient(startColorStr='#9900FF00',EndColorStr='#9900FF00'); 
```
支持CSS3多重背景图片的浏览器中可以用下面的语句来实现背景多重图片：
```css
background: url(bg-image-1.gif) center center no-repeat, url(bg-image-2.gif) top left;
```
要在IE中实现多背景图片，在需要在单独的IE hack样式表中加入下面的代码：
```css
background: transparent url(bg-image-1.gif) top left repeat;
filter:progid:DXImageTransform.Microsoft.AlphaImageLoader (src='bg-image-2.gif', sizingMethod='crop');
```

Tranformations/rotate旋转元素
IE中有两个滤镜可以实现元素的旋转，BasicImage和Matrix，前者简单方便但是只能做90*n(n∈{1,2,3,4})度的旋转；Matrix滤镜功能强大，但是参数复杂。

```css
-moz-transform: rotate(180deg); 
-o-transform: rotate(180deg); 
-webkit-transform: rotate(180deg); 
filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2); filter:progid:DXImageTransform.Microsoft.Matrix(sizingMethod='auto expand',M11=-1, M12=-1.2246063538223772e-16, M21=1.2246063538223772e-16, M22=-1);
```