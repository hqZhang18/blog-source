---
title: npm常用命令及npm-install-报的那些错
date: 2017-02-20 23:49:46
categories: 
  - 技术
  - npm
tags: npm
---

这两天的执行npm install 这个命令后每次心都伤得巴凉巴凉的，要么一整天都没个反应，要么全是ERR
真是要崩溃了，搞得我都想放弃react了，还好功夫不负有心人，今晚总算是把react-router的实例跑起来了，
<!-- more -->
当然从20:00至23点多，各种报错，准备睡了，不如再试试吧！不然睡不着呀！
不知道怎么搞的，这次报了个: ERR！Windows_NT 6.1.7601

解决办法：先设置代理为空 npm config set proxy null， 然后再npm install cnpm -g --registry=https://registry.npm.taobao.org！

哇噻！再来安装react需要依赖的一些包全都成功了

### 再补充个实用的 rimraf
每次npm install 后 想删掉node_modules这个文件夹又麻烦了
文件及文件夹太深总是删不掉
不如试试这个 npm install rimraf -g
安装成功后 rimraf node_modules

#### 常用命令
npm是什么
npm install 安装模块
npm uninstall 卸载模块
npm update 更新模块
npm outdated 检查模块是否已经过时
npm ls 查看安装的模块
npm init 在项目中引导创建一个package.json文件
npm help 查看某条命令的详细帮助
npm root 查看包的安装路径
npm config 管理npm的配置路径
npm cache 管理模块的缓存
npm start 启动模块
npm stop 停止模块
npm restart 重新启动模块
npm test 测试模块
npm version 查看模块版本
npm view 查看模块的注册信息
npm adduser
npm publish 发布模块
npm access 在发布的包上设置访问级别
npm package.json的语法
