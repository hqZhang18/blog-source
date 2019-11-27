---
title: vue和react的区别之我见
date: 2019-07-22 16:29:28
categories: 
  - 技术
  - JavaScript
tags: [vue, react]
---


react和vue都是做组件化的，整体的功能都类似，但是他们的设计思路是有很多不同的。使用react和vue，主要是理解他们的设计思路的不同。
<!--more-->
### 1.数据是不是可变的
react整体是函数式的思想，把组件设计成纯组件，状态和逻辑通过参数传入，所以在react中，是单向数据流，推崇结合immutable来实现数据不可变。react在setState之后会重新走渲染的流程，如果shouldComponentUpdate返回的是true，就继续渲染，如果返回了false，就不会重新渲染，PureComponent就是重写了shouldComponentUpdate，然后在里面作了props和state的浅层对比。

 而vue的思想是响应式的，也就是基于是数据可变的，通过对每一个属性建立Watcher来监听，当属性变化的时候，响应式的更新对应的虚拟dom。

 总之，react的性能优化需要手动去做，而vue的性能优化是自动的，但是vue的响应式机制也有问题，就是当state特别多的时候，Watcher也会很多，会导致卡顿，所以大型应用（状态特别多的）一般用react，更加可控。
 
### 2.通过js来操作一切，还是用各自的处理方式
react的思路是all in js，通过js来生成html，所以设计了jsx，还有通过js来操作css，社区的styled-component、jss等，

vue是把html，css，js组合到一起，用各自的处理方式，vue有单文件组件，可以把html、css、js写到一个文件中，html提供了模板引擎来处理。

### 3.类式的组件写法，还是声明式的写法

react是类式的写法，api很少，

而vue是声明式的写法，通过传入各种options，api和参数都很多。所以react结合typescript更容易一起写，vue稍微复杂。
