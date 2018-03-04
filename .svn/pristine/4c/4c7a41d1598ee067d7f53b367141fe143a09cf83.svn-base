---
title: node版本管理
date: 2017-08-18 14:11:32
categories: 
  - 技术
tags: javascript
---

一些环境经常因为版本问题跑不起来，那么怎么随意切换版本呢？
<!-- more -->
#### 首先，安装nvm，安装包自己网上下吧！
#### 然后使用cmd 切换镜像源
```
nvm node_mirror https://npm.taobao.or/mirrors/node
nrm npm_mirror https://npm.taobao.org/mirrors/npm
```

#### 然后使用nvm安装你想要的node版本
```
nvm install 5.11.1
```

下面是正在安装
Downloading node.js version 5.11.1 (64-bit)...
complete
Creating D:\Dev\nvm\temp

Downloading npm version 3.8.6... Complate
Installing npm v3.8.6
安装一个node会自己对应安装一个npm版本

#### 查看已经安装过的版本 
``` 
nvm list
```

#### 使用版本，切换版本

```
nvm use 5.11.1
```

### nrm -- NPM registry 管理工具
开发的npm registry 管理工具 nrm,  能够查看和切换当前使用的registry, 使用NPM经常 down 掉, 这个还是很有用的哈哈，
如果不用nrm管理就是手动管理
npm config registry http:xxx，这会有个问题，通过这种方式切换，如果想要发布自己的模块 npm publish是发布不了的


#### Install
```
$ npm install -g nrm
```

#### 查看所有镜像源
```
$ nrm ls
```

npm ---- https://registry.npmjs.org/
cnpm --- http://r.cnpmjs.org/
taotao---https://registry.npm.taobao.org/
nj ----- https://registry.nodejitsu.com/
rednpm-http://registry.mirror.cqupt.edu.cn/
npmMirror https://skimdb.npmjs.com/registry/
edunpm-http://registry.enpmjs.org/

#### 切换镜像源
```
nrm use taobao
```

#### 查看当前使用的镜像源
```
npm config get registry
```

