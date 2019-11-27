---
title: Node.js express 模板的简单使用、如何设置修改代码后自动重启服务（解决 “频繁修改代码手动重启服务器” 问题）
date: 2019-09-03 17:47:28
categories: 
  - 技术
  - Node
tags: [node]
toc: true
---


解决 “频繁修改代码手动重启服务器” 问题，安装第三方命令行工具： nodemon
<!--more-->
 
#### 通过 全局命令 安装的 包 可以在任意目录执行
```javascript
npm install --global nodemon
```

#### 安装完成后使用方法
```javascript
//  安装之前
node <fileName>
//  安装之后
nodemon <fileName>
```

只要是通过 nodemon 命令启动的服务，它会监视文件的变化，一旦文件发生变化（文件保存后）就会重启服务。