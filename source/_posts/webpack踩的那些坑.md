---
title: webpack踩的那些坑
date: 2018-08-08 08:47:56
categories: 
  - 技术
  - Webpack
tags: Webpack
---

Webpack升级到4.x踩的那些坑
##### 安装
```
npm install --save-dev webpack
```
你使用 webpack 4+ 版本，你还需要安装 CLI。
```
npm install --save-dev webpack-cli
```
更多初始配置详见 https://www.webpackjs.com/guides/installation/
<!--more-->
```
"start": "webpack-dev-server --open",
+     "start": "webpack-dev-server --open --config webpack.dev.js",
-     "build": "webpack"
+     "build": "webpack --config webpack.prod.js"
```

https://www.webpackjs.com/guides/production/#%E9%85%8D%E7%BD%AE

##### 常用操作命令
webpack -p    //压缩混淆脚本，这个非常非常重要！
webpack -d    //生成map映射文件，告知哪些模块被最终打包到哪里了
webpack -w 或 --watch   //监听变动并自动打包
webpack --config XXX.js   //使用另一份配置文件（比如webpack.config2.js）来打包
webpack --display-error-details 查看查找过程，方便出错时能查阅更详尽的信息
webpack --colors 输出结果带彩色，比如：会用红色显示耗时较长的步骤
webpack --profile 输出性能数据，可以看到每一步的耗时
webpack --display-modules 默认情况下node_modules下的模块会被隐藏，加上这个参数可以显示这些被隐藏的模块