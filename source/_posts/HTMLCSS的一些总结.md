---
title: HTMLCSS的一些总结
date: 2016-06-25 21:58:16
categories: 
  - 技术
  - CSS
tags: 
---

#### 1、什么是盒子模型？
在网页中，一个元素占有空间的大小由四个部分构成

其中包括元素的内容（content），元素的内边距（padding）元素的边框（border），元素的外边距（margin）四部分。
<!-- more -->
这四个部分占有的空间中，有的部分可以显示相应的内容，

而有的部分只用来分隔相邻的区域或区域。4个部分一起构成了css中元素的盒模型。


#### 2、行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

行内元素：a、b、span、img、input、strong、select、label、em、button、textarea 

块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote 

空元素：即系没有内容的HTML元素，例如：br、meta、hr、link、input、img
#### 3、CSS实现垂直水平居中
HTML结构：
```html
<div class="wrapper">
  <div class="content"></div>
</div>
```
CSS：
```css
.wrapper{
  position:relative;
} 
.content{ 
  background-color:#6699FF; 
  width:200px; 
  height:200px;
  position: absolute; //父元素需要相对定位
  top: 50%; left: 50%; 
  margin-top:-100px ; //二分之一的
  height，width margin-left: -100px; 
}
```

#### 4、src与href的区别
href 是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。

src是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；

在请求src资源时会将其指向的资源下载并应用到文档内，

例如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，

直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。

这也是为什么将js脚本放在底部而不是头部。

#### 5、什么是CSS Hack?
一般来说是针对不同的浏览器写不同的CSS,就是 CSS Hack。

IE浏览器Hack一般又分为三种，条件Hack、属性级Hack、选择符Hack（详细参考CSS文档：css文档）。
例如：
// 1、条件Hack
<!-- <!--[if IE]>
<style>
.test{color:red;}
</style>
<![enfif]> -->

// 2、属性Hack 
```css
.test{ color:#090\9; / For IE8+ / 
color:#f00; / For IE7 and earlier / 
_color:#ff0; / For IE6 and earlier */
```
// 3、选择符Hack 
```css
html .test{ color:#090; } / For IE6 and earlier / 
html .test{ color:#ff0; } / For IE7 
```
#### 6.同步和异步的区别
同步是阻塞模式，异步是非阻塞模式。

同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，
直到收到返回信息才继续执行下去；

异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进
行处理，这样可以提高执行的效率。

#### 7、px和em的区别
px和em都是长度单位，区别是，px的值是固定的，指定是多少就是多少，计算比较容易。

em得值不是固定的，并且em会继承父级元素的字体大小。

浏览器的默认字体高都是16px。所以未经调整的浏览器都符合: 1em=16px。那么12px=0.75em, 10px=0.625em

#### 8、什么叫优雅降级和渐进增强？
##### 渐进增强 progressive enhancement：
```css
.transition{
   transition: all .5s;          /* 标准写法 */
  -moz-transition: all .5s;     /* firefox 内核 */
  -webkit-transition: all .5s;  /* webkit 内核 */
}
```
针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到
更好的用户体验。

##### 优雅降级 graceful degradation：
```css
.transition{
    -webkit-transition: all .5s;  /* webkit 内核 */
    -moz-transition: all .5s;     /* firefox 内核 */
    transition: all .5s;          /* 标准写法 */
}
```
一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

区别：

a. 优雅降级是从复杂的现状开始，并试图减少用户体验的供给

b. 渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要

c. 降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带

##### 9、浏览器的内核分别有哪些?
IE: trident内核 Firefox：
gecko内核 Safari：
webkit内核 Opera：以前是presto内核，Opera现已改用Google Chrome的Blink内核 
Chrome：Blink(基于webkit，Google与Opera Software共同开发)

##### 10、-moz、-ms、-webkit浏览器私有前缀详解

- -moz 代表firefox浏览器私有属性
- -ms 代表IE浏览器私有属性
- -webkit 代表chrome、safari私有属性

##### 11、如何理解CSS的display属性

在布局中，display属性是最重要的CSS属性之一。
其最常见的属性值有block,inline,none,table以及inline-block
最近的新宠为flex

display: none;
将元素与其子元素从普通文档流中移除。这时文档的渲染就像元素从来没有存在过一样，
也就是说它所占据的空间被折叠了。元素的内容也会被屏幕阅读所忽略。

display: inline;
该元素生成一个或多个行内框。就如名字般，行内级元素所占具的空间就是他的标签所定义的大小。
可以被视为对块级元素的补充。

display: block;
该元素生成块级框。除特殊声明外，所有的块级元素开始于新的一行，延展到其容器的宽度。

display: list-item;
元素被渲染为列表项呈现的方式，确切说就像是一个块级元素，但是会生成一个可以被list-style属性进行样式修饰的标记框。
只有
元素可以具有list-style的默认值。通常将
元素重置为默认行为。

display: inline-block;
该元素生成一个块级别框，但是整个框的行为就像是一个内联元素。尝试在Codepen书写此示例，改变窗口的大小，这样会更有意义。

display: flex;
引入flexbox布局模块或CSS弹性框，标志着我们第一次有了专门为浏览器内容进行布局的规范。
自从HTML被引入之后，网页内容布局已经演变了很多。
当设计者想要创建一些富有创意的设计时，使用的第一种方法就是嵌套的HTML表格，或者我们所说的基于表格的布局。