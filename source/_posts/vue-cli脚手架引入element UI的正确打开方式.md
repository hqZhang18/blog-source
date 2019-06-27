---
title: vue-cli脚手架引入element UI的正确打开方式
date: 2018-08-08 08:49:56
categories: 
  - 技术
  - Vue
tags: element UI
---

element UI官网教程：http://element-cn.eleme.io/#/zh-CN/component/quickstart


##### 1、完整引入,直接了当，但是组件文件不是按需加载，造成多余，不够优雅
在 main.js 中写入以下内容：<!--more-->


```javascript
import Vue from 'vue';
import Element from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';
 
Vue.use(Element);
 
new Vue({
  el: '#app',
  render: h => h(App)
});
```

以上代码便完成了 Element 的引入。需要注意的是，样式文件需要单独引入。

##### 2、按需引入，需要配置babel文件 .babelrc
借助 babel-plugin-component，我们可以只引入需要的组件，以达到减小项目体积的目的。

首先，安装 `babel-plugin-component` 

```javascript
{
  "presets": [["es2015", { "modules": false }]],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

此时，vue-cli项目中.babelrc文件长这样子　

```javascript
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }],
    "stage-2"
  ],
  "plugins": ["transform-vue-jsx", "transform-runtime"]
}
```

接下来就要配置了，先来了解下各配置项用途
```javascript
{
　　// 此项指明，转码的规则
  "presets": [
    ["es2015", {"modules": false }],  //需要npm install babel-preset-es2015 --save-dev
// env项是借助插件babel-preset-env，下面这个配置说的是babel对es6,es7,es8进行转码，并且设置amd,commonjs这样的模块化文件，不进行转码
// compiles ES2015+ down to ES5 具体见babel-preset-env官网：https://www.npmjs.com/package/babel-preset-env
    ["env", { "modules": false }],  // 下面这个是不同阶段出现的es语法，包含不同的转码插件//可参考babel官网
    "stage-2"
  ],
  "plugins": [//// 下面这个选项是引用插件来处理代码的转换，transform-runtime用来处理全局函数和优化babel编译
     "transform-runtime",
     //需要npm install babel-plugin-component -D//官网：http://element-cn.eleme.io/#/zh-CN/component/quickstart
     ["component", [{
        "libraryName": "element-ui",           //按需引用element-ui插件
        //"styleLibraryName": "theme-default"   //按需引用element-ui主题
     }]]  
  ],// 下面指的是在生成的文件中，不产生注释
  "comments": false,// 下面这段是在特定的环境中所执行的转码规则，当环境变量是下面的test就会覆盖上面的设置
  "env": {// test 是提前设置的环境变量，如果没有设置BABEL_ENV则使用NODE_ENV，如果都没有设置默认就是development
    "test": {
      "presets": ["env", "stage-2"],// instanbul是一个用来测试转码后代码的工具
      "plugins": [ "istanbul" ]
    }
  }
}
```


OK，到这步已经配完了?

但是你会发现在npm install babel-preset-es2015 时，你会发现有如下的 Deprecated警告：
```
deprecate babel-preset-es2015@* ????  Thanks for using Babel: we recommend using
 babel-preset-env now: please read babeljs.io/env to update!
√ All packages installed (1 packages installed from npm registry, used 44s, spe
ed 1.84kB/s, json 25(80.05kB), tarball 0B)
```
原因是Babel 的官网上在2017年9月宣布 ES2015 / ES2016/ ES2017 等等 ES20xx 时代的 presets 通通被废弃（deprecated），取而代之的是 babel-preset-env，并且承诺它将成为“未来不会过时的（future-proof）”解决方案。

- 在过去，Babel 将 babel-preset-es2015 放在 babel/babel 的主仓库中进行维护，而 babel-preset-env 则独立为一级项目，这从某种程度上也显示出 Babel 官方对这款 preset 的重视程度和更长远的规划。

#### 如何迁移
###### 首先卸载原来的 preset，然后安装 `babel-preset-env`
```
npm uninstall --save-dev babel-preset-es2015
npm install --save-dev babel-preset-env@next
```

好了，恭喜你，就这么简单，你已经可以与 ES2015+ 保持更新了！

vue-cli脚手架环境中，已经采用了最新的babel-preset-env，所以可以忽略 "presets": [["es2015", { "modules": false }]]  es2015 这项

```javascript
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }],
   // ["es2015", { "modules": false }],   //需要先cnpm install babel-preset-es2015 --save-dev ,下载es5的babel转码插件，些处是多余，已配置env
    "stage-2"
  ],
  "plugins": [
    "transform-vue-jsx",
    "transform-runtime",
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```


接下来，就可以欢快的实现按需加载啦　　

如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：

```javascript
import Vue from 'vue';
import { Button, Select } from 'element-ui';
import App from './App.vue';
 
Vue.component(Button.name, Button);
Vue.component(Select.name, Select);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Select)
 */
 
new Vue({
  el: '#app',
  render: h => h(App)
});
```

##### 全局配置
在引入 Element 时，可以传入一个全局配置对象。该对象目前仅支持 size 字段，用于改变组件的默认尺寸。按照引入 Element 的方式，具体操作如下：

###### 完整引入 Element：
```javascript
mport Vue from 'vue';
import Element from 'element-ui';
Vue.use(Element, { size: 'small' });
```
###### 按需引入 Element：
```javascript
import Vue from 'vue';
import { Button } from 'element-ui';
 
Vue.prototype.$ELEMENT = { size: 'small' };
Vue.use(Button);　
```

按照以上设置，项目中所有拥有 size 属性的组件的默认尺寸均为 'small'。