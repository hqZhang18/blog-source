---
title: 网页中常用Jquery效果
date: 2016-06-11 23:03:57
categories: 
  - 技术
  - Jquery
tags: 
---
#### 下拉菜单
```javascript
$(function(){
  $(".s-weather").hover(function(){ 
      $(".s-wShow").show(); 
      },function(){ 
      $(".s-wShow").hide();   
  })
<!-- more -->
  $(".s-wShow").hover(function(){
      $(".s-wShow").show(); 
      },function(){ 
   $(".s-wShow").hide(); 
  })
})
```
#### 导航菜单切换1
```javascript
 $(function(){
    $(".tabs-nav a:first").addClass("current")
        $(".tabs-nav a").on("click",function(){
        var index=$(this).index();
        $(this).addClass("current");
        $(this).siblings().removeClass("current");
        $(".wrap").find(".tabs-box").hide().eq(index).show();
    })
})  
```
#### 导航菜单切换2
```javascript
 $(function(){
       $(".sel-tabs-nemu li").on("click",function(){
        var i=$(this).index();
        $(".sel-tabs-nemu li").children().removeClass("cur");
        $(this).children().addClass("cur");
        $(".con_center").find(".sel-tabs-content").hide().eq(i).show();
    });
})
```
 

#### a标签点击跳转页面后怎么给当前点击的a标签用jquery添加一个样式。
```javascript
    $('.tag_sort a').each(function () {
        if ($($(this))[0].href == String(window.location))
        $(this).addClass('cur').attr('href', 'javascript:void(0);');
    });
    A 标签target属性必须是_parent 在父框架集中打开被链接文档
```
#### 点击按钮回到顶部

```css
.gotop{ 
  position:fixed; 
  right:10px; 
  bottom:20px; 
  display:block; 
  background:#ccc;
  font-size:24px; 
  color:#222; width:40px; 
  height:40px; 
  line-height:40px; 
  text-align:center; 
  cursor:pointer; 
  display:none;
 }
```
```javascript
$(function(){
  $(window).scroll(function(){
    var wh=$(window).scrollTop();
    if(wh>0)
    {
      $("#gotop").fadeIn()
    }else{
      $("#gotop").fadeOut();
    }
  });
  $("#gotop").click(function(){
    $("body,html").animate({scrollTop:0},300);
  })
})
```
```html
<div style="height:; background:#eee;"></div>
<div class="gotop" id="gotop">^</div> 
```
#### 禁止右键点击
```javascript
$(document).ready(function(){ 
  $(document).bind("contextmenu",function(e){ 
   return false
 }); 
});
```
#### 隐藏搜索文本框文字

```javascript
$(document).ready(function() { 
   $("input.text1").val("Enter your search text here"); 
    textFill($('input.text1'))
}); 
function textFill(input){ //input focus text function 
  var originalvalue = input.val(); 
  input.focus( function(){ if( $.trim(input.val()) == originalvalue )
  { input.val(''); } }); 
  input.blur( function(){ if( $.trim(input.val()) == '' )
  { input.val(originalvalue); } 
}); 
}
```
#### 在新窗口中打开链接

```javascript
$(document).ready(function() { 
//Example 1: Every link will open in a new window 
         $('a[href^="http://"]').attr("target", "_blank");
//Example 2: Links with the rel="external" attribute will only open in a new window  
           $('a[@rel$='external']').click(function(){ 
               this.target = "_blank"; }); 
}); 
````
#### 让两个 DIV 高度相同
```javascript
var $columns = $('.column'); 
var height = 0; $columns.each(function () { 
    if ($(this).height() > height) { 
    height = $(this).height(); } });
    $columns.height(height);
```
#### Jquery判断当前屏幕分辨率并加载不同的css样式

```javascript
$(function () {
    if ((screen.width == 1024) && (screen.height == 768)) {
    $("#xx").height(500);//此分辨率下你需要的操作
    } else if ((screen.width == 1360) && (screen.height == 900)) {
    $("#xx").height(700);//这个分辨率下你的操作
    } else {
    $("#xx").height(500);//默认操作
    }
});
```
#### jQ判断IE版本
```javascript
if ($.browser.msie && ($.browser.version == "7.0" 
    || $.browser.version == "8.0") && !$.support.style) {
  $(document).ready(function () { 
    $("#chartContainer").css("width", 435); 
    $(".highcharts-container").css({ "position": "absolute", "left": -420, "top": 5 ;
  })
}
```