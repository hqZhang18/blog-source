---
title: linear比例尺及ordinal比例尺的使用
date: 2017-02-28 11:05:42
categories: 
  - 技术
  - D3.js
tags: 比例尺 
---

在使用D3.js画图比例尺的使用是必不可少的，但对linear与ordinal总是处于蒙圈的状态

写了个实例，总算弄清楚两个分别时候使用比较合适了,废话少说，直接上源码
<!-- more -->

```javascript

  var width = 500
  var height = 200
  //添加svg元素
  var svg = d3.select('body')
    .append('svg')
    .attr('width', width)
    .attr('height', height)
    .style('padding', '40px')

  var data = [    
    {
      name: '江北区',
      value: 100
    },{
      name: '渝北区',
      value: 80
    },{
      name: '九龙坡区',
      value: 120
    },{
      name: '沙坪坝',
      value: 182
    },{
      name: '渝中区',
      value: 79
    }
  ]

  var cfg = {
    itemStyle: {
      width: 20,
      color: 'yellow',
      padding: 50,
      min: 10
    }
  }
  
  var dataset = []
  var xData = []    
  //处理数据
  for(var i=0, len = data.length; i<len; i++){
    dataset.push(data[i].value)
    xData.push(data[i].name)
  }

  var min = d3.min(dataset)
  var max = d3.max(dataset)

  //定义Y轴比例尺
  var yScale = d3.scale.linear()
        .domain([0, max])  //定义域
        .range([height, 0])  //值域(可用范围)

  //定义Y轴    
  var yAxis = d3.svg.axis()
       .scale(yScale)      //指定比例尺
       .orient('left')   //指定刻度的方向

  //添加Y轴     
  svg.append("g")
    .attr('class', 'axis-y')
    .call(yAxis)


  //定义X轴比例尺(序数比例尺) 因为X轴要显示文字，因此此处使用序数比例尺
  var xScale = d3.scale.ordinal()
    .domain(xData)
    .rangeRoundBands([0, width]);  

  //定义X轴    
  var xAxis = d3.svg.axis()
      .scale(xScale)      //指定比例尺
      .orient('bottom')   //指定刻度的方向
      
  //添加X轴     
  svg.append("g")
    .attr('class', 'axis-x')
    .call(xAxis)
    .attr('transform', 'translate(' + 0 + ',' + height + ')')

  var itemStyle = cfg.itemStyle  

  //x轴的比例尺 添加rect时需要算一个x的位置，再定义一个x比例尺
  var xScale2 = d3.scale.ordinal()
      .domain(d3.range(dataset.length))
      .rangeRoundBands([0, width]);
  //添加bar
  svg.selectAll('.rect')
    .data(dataset)
    .enter()
    .append('rect')
    .attr('class', 'rect')
    .attr('width', itemStyle.width)
    .attr('height', function(d, i){
      var h = yScale(d)
      if(h<=0){
        h = itemStyle.min
      }
      return h
    })   
    .attr("x", function(d, i){
        return xScale2(i) + itemStyle.width/2 + itemStyle.padding/2
    } )
    .attr("y",function(d, i){
      var y = height - yScale(d)
      if(y==height){
        y = y - itemStyle.min
      }
      return y
    })
```
