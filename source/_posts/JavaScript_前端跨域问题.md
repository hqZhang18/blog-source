---
title: 前端跨域问题
date: 2017-01-05 20:27:33
categories: 
  - 技术
  - JavaScript
tags: 跨域
---

#### 同源策略
域名相同、端口相同、协议相同
<!--more-->
满足这三个条件时满足同源策略

#### JSONP
JSON With Padding : 把一段 json 数据添加进来

jsonp 是使用 script 来进行交互的, 因为 script 标签不受同源策略影响, 而且 script 可以执行一段 javascript 代码, 利用这个机制来绕开同源策略。

##### 前端对 jsonp 的处理
```javascript
//声明全局函数，用来接收 jsonp 返回的数据
function jsonp_callback(data){
  console.log(data);
}

//动态创建一个 script 标签
var script = document.createElement("script");
//设置 src, 数据以 get 形势传递
//最重要的是要跟上一个 get 参数 callback (参数名随意, 参数的值必须是前面自己定义的全局函数名称)
script.src = "/test/jsonp?data=data&callback=jsonp_callback";

//获取一个 dom 节点
var body = document.getElementsByTagName("body")[0];
//把创建好的 script 添加到页面中
body.appendChild(script);
```
##### 后台对 jsonp 的处理

以 node.js 为例
```javascript
var express = require ('express');
var app = express();

app.route('/test/jsonp')
  //声明一个 get 请求
  .get(function(req, res, next) {
      var param = req.query;
      //这个 key 值需要与前端沟通好
      //关系到返回的数据是否能正常执行
      var callbackNmae = param['callback']; 
      var data = {
        "success" : true,
        "data" : [
          "这里返回正确的数据，与正常的 ajax 交互一样"  
        ]
      };
      //以为返回的就是一个数据对象, jsonp 需要返回一段 javascript 代码, 且是立即执行的函数
      //函数的参数为 json 数据
      res.send(`${callbackNmae}("${JSON.stringify(data)}");`);
  }
);


var server  = require('http').createServer(app);
server.listen(5000, "127.0.0.1", function() {
  console.log('http://127.0.0.1:5000');
});
```

#### 代理模式 <code>server language</code>

回到开头，我们的需求是当网站前台需要访问其它站点的接口时因为受到同源策略限制, 发起的 ajax 会失败, 后面介绍了实用 jsonp 来绕过同源策略, 假如其它站点不支持 jsonp 该怎么办呢？
浏览器有同源策略限制，但是 后台没有限制，我们是否可以在后台这样做呢？

前端发起一个请求给后台，后台接收到请求后去请求其它站点的数据，拿到数据后返回给前端。

前端发起正常的 ajax

```javascript
var xhr;
if (window.XMLHttpRequest){
  //支持 XMLHttpRequest 的浏览器
    xhr=new XMLHttpRequest();
}else{
  //不支持 XMLHttpRequest 的浏览器使用 ActiveXObject
    xhr=new ActiveXObject("Microsoft.xhr");
}

xhr.onreadystatechange=function(){
    if (xhr.readyState == 4){
    console.log(xhr.responseText);
    }
}
var url = "/test/jsonp?data=data&url=http://website/api/path";
xhr.open("GET", url, true);
xhr.send();
```

后台处理 ajax
```javascript
var express = require ('express');
//导入 request 模块
var request = require('request');
var app = express();

app.route('/test/jsonp')
  //声明一个 get 请求
  .get(function(req, res, next) {
      var param = req.query;
      var url = param.url; //获取目标服务器地址
      delete param.url; 
      //发起 http 请求
      request.get({
      url : url,
      formData : param
    }, function (error, response, body) {
      if (!error && response.statusCode == 200) {
        //返回接收到的数据
        res.send(body);
      }
    });
  }
);


var server  = require('http').createServer(app);
server.listen(5000, "127.0.0.1", function() {
  console.log('http://127.0.0.1:5000');
});
```

#### 代理配置 Nginx

反代理与上面的逻辑一样, 都是利用后台服务进行绕开同源策略, 上面两种方式都是需要修改后台代码的, 这种方式是在服务器层进行配置, 相对简单很多。

不会安装 nginx 的请移步, 先看安装与配置文档

将路由开头为 cors/api 的所有请求全部转发到另一个站点, 达到跨域请求效果

nginx 配置
```javascript
server {
    server_name localhost;
    listen 8080;

    root /PATH/TO/WEBROOT/;
    index index.html index.htm;

    # 配置开头路由，只有路由中是以 cors/api 开头的都会默认为跨域请求
    location ^~ /cors/api/ {
        proxy_pass http://origin.website/;
    }
}
```
前端处理
```javascript
var xhr;
if (window.XMLHttpRequest){
  //支持 XMLHttpRequest 的浏览器
    xhr=new XMLHttpRequest();
}else{
  //不支持 XMLHttpRequest 的浏览器使用 ActiveXObject
    xhr=new ActiveXObject("Microsoft.xhr");
}

xhr.onreadystatechange=function(){
    if (xhr.readyState == 4){
    console.log(xhr.responseText);
    }
}
var url = "/cors/api/test/getdata?data=data";
xhr.open("GET",url,true);
xhr.send();

// 请求地址为 /cors/api/test/getdata?data=data
// 真实请求地址为 : http://origin.website/test/getdata?data=data
```

#### Access-Control-Allow-Origin

浏览器每一个请求不管是否跨域都会向服务器发送一个请求，询问是否可以访问，如果服务器告诉浏览器该接口你有全新访问，那么浏览器就会接收服务器返回的数据，否则会抛出异常

以 node.js 为例，修改 response 信息

```javascript
var express = require ('express');
var app = express();

//设置请求的接口地址，允许 get / post
app.all('/api/test', function(req, res) {
  // 设置允许来置所有域下的的请求，达到跨域
  res.set({
    // * 为允许任何域访问
    // 如果只允许某个域名 请设置单独的域名
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "POST,GET",
    "Access-Control-Allow-Credentials": "true",
    "Content-Type": "text/html; charset=utf-8"
  });

  res.send({
    "success" : true,
    "data" : [ /* 返回的数据 */ ]
  });
});


var server  = require('http').createServer(app);
server.listen(5000, "127.0.0.1", function() {
  console.log('http://127.0.0.1:5000');
});
```