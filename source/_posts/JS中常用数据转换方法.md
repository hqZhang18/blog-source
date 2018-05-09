---
title: JS中常用数据转换方法
date: 2018-04-09 07:07:33
categories: 
  - 技术
tags: JavaScript
---

将数组转换为对象，并循环遍历对象

```javascript
// 现有如下数组
let array = [
  {
    id: '001',
    name: 'AA1'
  },{
    id: '002',
    name: 'AA2'
  }
]
<!-- more -->
let object = {}
array.map(d => object[d.id] = d.name)

// 有已知的id，通过id查找名字
let menuId = '001'
let name = ''
for(let id in object) {
  if(id === menuId) {
    name = object[id]
  }
}

```
