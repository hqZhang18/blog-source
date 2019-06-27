---
title: vue-cli脚手架config目录下index.js配置文件详解
date: 2018-08-08 08:49:56
categories: 
  - 技术
  - Webpack
tags: Webpack
---

##### 此文章介绍vue-cli脚手架config目录下index.js配置文件
1.此配置文件是用来定义开发环境和生产环境中所需要的参数
 <!--more-->

```javascript
// path是node.js的路径模块，用来处理路径统一的问题
const path = require('path')

module.exports = {
  // 开发环境配置项
  dev: {
    // 引入当前目录下的dev.env.js，用来指明开发环境
    env: require('./dev.env'),
    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    // 跨域代理设置代理表，建一个虚拟api服务器用来代理本机的请求，只能用于开发模式
    proxyTable: {
      '/backendApi': {
        target: 'http://58.83.189.150:18888/',
        changeOrigin: true, //如果接口跨域，需要进行这个参数配置
        secure: false,  // 如果是https接口，需要配置这个参数
      },
      '/weather-web/resources': {
        target: 'http://58.83.189.150:18888/',
        changeOrigin: true, // // 如果接口跨域，需要进行这个参数配置
        secure: false,  // 如果是https接口，需要配置这个参数
      },
    },
    // dev-server的端口号，可以自行更改
    port: 8086,  
    devtool: 'cheap-module-eval-source-map',
    // 是否生成css，map文件，
    cssSourceMap: false
  },
  // 线上环境配置项
  build: {
    // 导入prod.env.js配置文件，只要用来指定当前环境
    env: require('./prod.env'),
    // Template for index.html
    // 相对路径的拼接，假如当前跟目录是config，那么下面配置的index属性的属性值就是dist/index.html
    index: path.resolve(__dirname, '../../dist/index.html'), // html入口文件
    // 定义的是静态资源的根目录 也就是dist目录
    assetsRoot: path.resolve(__dirname, '../../dist/'), // 打包后的目录设置
    // 定义的是静态资源根目录的子目录static，也就是dist目录下面的static
    assetsSubDirectory: 'static', // 打后的静态资源
    // 下面定义的是静态资源的公开路径，也就是真正的引用路径(服务器路径)
    assetsPublicPath: 'http://58.83.189.150:18888/',
    // 是否生成生产环境的sourcmap，sourcmap是用来debug编译后文件的，通过映射到编译前文件来实现
    productionSourceMap: false, 
    // 下面是是否在生产环境中压缩代码，如果要压缩必须安装compression-webpack-plugin
    productionGzip: true,
    // 下面定义要压缩哪些类型的文件
    productionGzipExtensions: ['js', 'css'],
    // 下面是用来开启编译完成后的报告，可以通过设置值为true和false来开启或关闭
    // 下面的process.env.npm_config_report表示定义的一个npm_config_report环境变量，可以自行设置
    bundleAnalyzerReport: process.env.npm_config_report
  }
}
```


```javascript
(1)下面是prod.env.js的配置内容
    module.exports = {
        // 作用很明显，就是导出一个对象，NODE_ENV是一个环境变量，指定production环境
        NODE_ENV: '"production"'
    }
(2)下面是dev.env.js的配置内容
    // 首先引入的是webpack的merge插件，该插件是用来合并对象，也就是配置文件用的，相同的选项会被覆盖，至于这里为什么多次一举，可能另有他图吧
    var merge = require('webpack-merge')
    // 导入prod.env.js配置文件
    var prodEnv = require('./prod.env')
    // 将两个配置对象合并，最终结果是 NODE_ENV: '"development"'
    module.exports = merge(prodEnv, {
        NODE_ENV: '"development"'
    })
(3)下面是proxyTable的一般用法
    vue-cli使用这个功能是借助http-proxy-middleware插件，一般解决跨域请求api
    proxyTable: {
        '/list': {
            target: 'http://api.xxxxxxxx.com', -> 目标url地址
            changeOrigin: true, -> 指示是否跨域
            pathRewrite: {
            '^/list': '/list' -> 可以使用 /list 等价于 api.xxxxxxxx.com/list
            }
        }
    }
```