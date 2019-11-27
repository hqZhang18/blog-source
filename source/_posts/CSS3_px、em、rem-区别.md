---
title: px、em、rem 区别
date: 2016-12-24 22:13:16
categories: 
  - 技术
  - CSS
tags: 单位
---

#### PX
px 像素单位。px 是相对于显示器屏幕分辨率而设置大小的。
px 是一个真实的物理尺寸, 是一个绝对单位。<!--more-->
#### EM
em 是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸(也可以理解为相对于父元素尺寸)。

```html
<div style="font-size: 12px;">
	<strong style="font-size: 1em;">hello world</strong>
</div>
```
strong 元素中的 1em 就是想对与父元素中来设置的, 这里的 1em 等于 12px	
#### REM
rem 是 CSS3 的一个相对单位（root em，根em, 这个单位与 em 有什么区别呢？区别在于使用 rem 为元素设定字体大小时, 仍然是相对大小，但相对的只是 HTML 根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。
```html
<!DOCTYPE html>
<html lang="en" style="font-size: 12px;">
<head>
	<meta charset="UTF-8">
	<title>Rem</title>
</head>
<body>
	<div style="font-size: 20px;">
		<strong style="font-size: 1rem;">hello world</strong>
	</div>
</body>
</html>
```
strong 元素中的 1rem 就是想对与跟元素(html)中来设置的, 这里的 1rem 等于 12px, 与父元素没有关系