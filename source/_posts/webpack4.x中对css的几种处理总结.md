---
title: webpack4.x中对css的几种处理总结（css分离，消除冗余的css代码，自动添加浏览器内核前缀）
date: 2018-08-08 08:47:56
categories: 
  - 技术
  - Webpack
tags: Webpack
---

webpack4.x中对css的几种处理总结（css分离，消除冗余的css代码，自动添加浏览器内核前缀）
##### 一、CSS分离

 我们知道webpack的理念就是把所有的东西都打包到js文件中，包括css、图片呀等等，好处是减少http请求，但劣势也很明显，就是随着项目越来越大，js文件也会越来越大，所以，我们就需要对css文件进行分离

css分离，嗯，其实就是将css单独打包，做法很简单，需要一个插件，extract-text-webpack-plugin@next（注意：加@next是现阶段必须要加的（前提是你使用的webpack是4.0版本及以上的，如果你使用的是3版本及以前的版本的话不需要加@next），但以后如果过渡到了这个版本，就不需要加了），目前如果不加，插件版本太低，会报错
<!--more-->
1、npm install extract-text-webpack-plugin@next 
2、在配置文件中引入  const ExtractTextWebpackPlugin = require('extract-text-webpack-plugin');
3、在plugins中加入new  ExtractTextWebpackPlugin('css提取出去的路径') 
4、在配置文件中修改针对css的设置如下所示
```javascript
{
    test:/\.css$/,
    use:ExtractTextWebpackPlugin.extract({
        fallback:'style-loader',
        use:['css-loader']
    })
}
```

```
// webpack.config插件配置
plugins: [
    new ExtractTextPlugin({
      filename: utils.assetsPath('css/[name].[hash].css'),
      allChunks: true,
    }),
 ]
```

##### 二、消除冗余的css代码


平时我们去写一些项目的时候，会引入一些框架比如bootstrap，引入这个框架后，文件会变得很大，，而我们能用到的却很少，那很多代码就浪费掉了，所以这时候我们就可以想办法优化这些代码，说白了，就是把没有用到的css代码给去除掉

我们知道webpack有很多优点，那，其中一个是可以优化代码，提高性能。消除冗余的css代码也是webpack优化性能的一种方法

步骤：

npm install --save-dev purifycss-webpack 
引入插件：const PurifyCssWebpack  = require('purifycss-webpack');
还需要引入一个额外包glob（用于扫描路径） npm i glob -D
const glob = require('glob');
在plugins中配置：
```javascript
new PurifyCssWebpack({
    paths:glob.sync(path.join(__dirname,'src/*.html'))
})
```

##### 三、自动添加浏览器内核前缀

这里需要用到post-css（预处理器）还需要一个插件 autoprefixer(是处理前缀的插件，是post-css众多插件中的一种)

步骤：

1、npm install postcss-loader autoprefixer 

2、在根目录中添加一个配置文件postcss.config.js，然后配置postcss
```javascript
module.exports = {
    plugins:[require('autoprefixer')]
}
```
如果想要分离css，可以写成
```javascript
{
    test:/\.css$/,
    use:ExtractTextWebpackPlugin.extract({
        fallback:'style-loader',
        use:['css-loader','postcss-loader']
    })
}
```