---
title: Webpack的安装与基本配置
date: 2016-12-17 22:06:11
categories:
- 技术
- Webpack
tags: Webpack 
toc: true
---


首先要安装 Node.js， Node.js 自带了软件包管理器 npm，Webpack 需要 Node.js v0.6 以上支持，建议使用最新版 Node.js。

#### 安装
用 npm 安装 Webpack：

```javascript 
$ npm install webpack -g
```
此时 Webpack 已经安装到了全局环境下，可以通过命令行 webpack -h 试试。

通常我们会将 Webpack 安装到项目的依赖中，这样就可以使用项目本地版本的 Webpack。

#### 使用
1.将 Webpack 安装到项目的依赖中，这样就可以使用项目本地版本的 Webpack。
```javascript 
npm install --save-dev webpack
 ```

2.初始化一个新的项目
```javascript 
npm init # (answer the questions)
```

#### 配置文件
Webpack 在执行的时候，除了在命令行传入参数，还可以通过指定的配置文件来执行。默认情况下，会搜索当前目录的 <code>webpack.config.js </code> 文件，这个文件是一个 node.js 模块，返回一个 json 格式的配置信息对象，或者通过 <code>--config</code> 选项来指定配置文件。

修改根目录已经创建好的package.json 来添加 webpack 需要的依赖：

```javascript 
{
  "name": "React-dome",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "webpack && webpack-dev-server --hot --inline --port 3002"
  },
  "author": "zhanghongqiao",
  "license": "ISC",
  "dependencies": {
    "babel-core": "^6.14.0",
    "babel-loader": "^6.2.5",
    "jquery": "^3.1.1",
    "path": "^0.12.7",
    "webpack": "^1.13.2",
    "webpack-dev-server": "^1.16.1"  //启服务
  },
  "devDependencies": {
    "babel-preset-es2015": "^6.14.0",
    "babel-preset-react": "^6.11.1",
    "babel-preset-react-hmre": "^1.1.1",
    "webpack-hot-middleware": "^2.12.2"   //host loading
  }
}
```


别忘了执行 npm install。

然后创建一个配置文件 webpack.config.js：
```javascript 
var webpack = require('webpack')
var path = require('path')

module.exports = {
    entry: [
        'webpack/hot/dev-server',
        './src/index.js'
    ],
    output: {
        path: path.join(__dirname, 'build'),
        filename: 'index.js',
        publicPath: '/build/'
    },
    module: {
        loaders: [
            {
                test: /\.js?$/,
                loader: 'babel',
                exclude: /node_modules/,
                query: {
                    'env': {
                        'development': {
                            'presets': ['react-hmre', 'es2015', 'react']
                        }
                    }
                }
            },
            {
                test: /\.css$/,
                loader: 'style!css'
            }
        ]
    }
}
```
在src目录下新建一个index.js
```javascript 
import $ from 'jquery';

$('<h1>webpack test</h1>').appendTo('body');

```


#### 运行
在根目录新建一个index.html
```html 
<!DOCTYPE html>
 <html>
     <head>
         <meta charset="utf-8">
     </head>
     <body>
         <script src="build/index.js" charset="utf-8"></script>
     </body>
 </html>

```

然后执行命令
 ```javascript 
npm start
```

http://webpack.github.io/docs/usage.html
http://webpackdoc.com/install.html