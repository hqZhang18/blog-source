---
title: svg动画（多个元素绕同一路径匀速运动）
date: 2017-08-24 14:18:24
tags: SVG
---

画了一个椭圆路径，有n个小球围绕着旋转，并且每个要平均分配间隔匀速转，代码如下：

#### 添加一个椭圆动画路径
```javascript
 svg.append('path')
  .attr({
    d: 'M474.355,6.586 C731.169,9.309 921.500,70.804 921.500,148.329 C921.500,225.854 728.360,285.500 471.531,285.500 C214.701,285.500 6.500,222.653 6.500,145.128 C6.500,67.603 219.408,3.882 474.355,6.586 Z',
    fill: 'none',
    stroke: 'none',
    id: 'cubicCurve' // id用于后面使用该路径
  })
```
<!--more-->

#### 创建要运动的元素
```javascript
  /**
   *  设置图片元素属性
   *  @param    {array}   roots 根元素
   *  @param    {object}  cfg   配置项
   *  @param    {array}    data  数据
   */
  function outerCircle(roots, cfg, data) {
    roots.attr({
      'xlink:href': function(d, i) {
        if(cfg.type==1) {
          var href = ''
          i === 0 ? href = IMG_PATH + 'index/inner-circle.png' : href = cfg.href
          return href
        }
        return cfg.href
      },
      width: cfg.width,
      height: cfg.height,
      class: function(d, i) {
        // 添加样式，自动切换使用
        return cfg.class + ' '+cfg.class + i+''
      },
      x: cfg.x,
      y: cfg.y
    })
    .on('click', function(d, i) {
      console.log('dddd')
      if(cfg.type==1) {
        toggleData(d3.select(this), i)
        clearInterval(timer)  // 停止自动切换
        // 间隔15秒自动切
        setTimeout(function() {
          setInterVal(data)
        }, 15000)
      }
    })
    .call(addAnimateMotion, cfg)  //调用动画
  } 
```


#### 添加动画并使用路径
```javascript
  /**
   *  添加动画
   *  @param    {object}  cfg   动画配置项
   */
  function addAnimateMotion(roots, cfg) {
    roots.append('animateMotion')
    .attr({
      begin: function(d, i) {
         return i * cfg.begin
      },
      dur: cfg.dur,
      fill: 'freeze',
     // rotate: 'auto',
      repeatCount: 'indefinite',
    })
    .append('mpath')
    .attr({
      'xlink:href': cfg.mpath
    })
  }

```
- begin 是延迟时间
- dur是完成时间