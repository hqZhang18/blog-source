---
title: 获取地址栏参数
date: 2016-06-11 14:11:32
categories: 
  - 技术
tags: javascript

---


```javascript
获取地址栏参数(谷歌49以上版本才支持)
url: https://www.baidu.com/?name=xiqoao&age=23
var search = location.search
"?name=xiqoao&age=23"
search = search.slice(1)
"name=xiqoao&age=23"
parms = new URLSearchParams(search)
parms.get('name')
"xiqoao"
parms.get('age')
"23"
```

