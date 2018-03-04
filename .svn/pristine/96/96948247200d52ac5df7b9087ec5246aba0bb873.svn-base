---
title: 浏览器兼容性问题汇总
date: 2016-12-21 22:59:16
categories: 
  - 技术
  - JavaScript
tags: [JS兼容性]
---


<code>trim</code>（不支持IE6~IE9） 去掉字符串中的空格。

```javascript
// 以下为兼容写法
String.prototype.trim = function () {
    return this.replace(/^\s\s*/, '').replace(/\s\s*$/, '');
}

```


<!--more-->

<code>requestAnimationFrame</code>（不支持IE6~IE9）它是由浏览器专门为动画提供的API，效果和setTimeout/setInterval类似。

```javascript
// 以下为兼容写法
var rAF = window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    window.msRequestAnimationFrame ||
    function (callback) { window.setTimeout(callback, 1000 / 60); };

```

<code>addEventListener</code> （不支持IE）  为元素绑定事件。
```javascript
// 以下写法可以兼容大部分情况
var addHandler = function(el, type, handler, args) {
    if (el.addEventListener) {
        el.addEventListener(type, handler, false);
    } else if (el.attachEvent) {
        el.attachEvent('on' + type, handler);
    } else {
        el['on' + type] = handler;
    }
};
var removeHandler = function(el, type, handler, args) {
    if (el.removeEventListener) {
        el.removeEventListener(type, handler, false);
    } else if (el.detachEvent) {
        el.detachEvent('on' + type, handler);
    } else {
        el['on' + type] = null;
    }
};
```

event.target （不支持IE6~IE9） 引发事件的DOM元素。

```javascript
// 以下为兼容写法
target = event.target || event.srcElement;
```

event.preventDefault （不支持IE6~IE9）如果事件对象的cancelable属性为true，则该方法可以取消事件的默认动作，但并不取消事件的冒泡行为。

```javascript
// 以下为兼容写法
event.preventDefault ? event.preventDefault() : (event.returnValue = false);

```
event.stopPropagation（不支持IE6~IE9）阻止事件的冒泡行为。

```javascript
// 以下为兼容写法
event.stopPropagation ? event.stopPropagation() : (event.cancelBubble = false);

```
event.touches.pageX（不支持IE6~IE9）鼠标在页面上的位置,从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化。

```javascript
// 以下为兼容写法
var touches = e.touches ? e.touches[0] : e;
var pageX = (touches.pageX) ? touches.pageX : e.clientX + (document.documentElement.scrollLeft ? document.documentElement.scrollLeft : document.body.scrollLeft);
var pageY = (touches.pageY) ? touches.pageY : e.clientY + (document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop);

```