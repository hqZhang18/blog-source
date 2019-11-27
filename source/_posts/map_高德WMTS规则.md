---
title: 高德WMTS规则
date: 2019-10-14 13:49:09
categories: 
  - 技术
  - Openlayers
tags: []
---

### 高德WMTS规则

 http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=7&x={x}&y={y}&z={z}

lang可以通过zh_cn设置中文，en设置英文
size基本无作用
scl设置标注还是底图，scl=1代表注记
scl=2代表底图（矢量或者影像）
style设置影像和路网，6为影像图，7为矢量路网，8为影像路网
<!--more-->
##### 组合列表
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=7 为矢量图（含路网、含注记）
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=2&style=7 为矢量图（含路网，不含注记）
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=6 为影像底图（不含路网，不含注记）
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=2&style=6 为影像底图（不含路网、不含注记）
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=8 为影像路图（含路网，含注记）
http://wprd0{1-4}.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=2&style=8 为影像路网（含路网，不含注记）





#### 加载谷歌地图的地址总结如下：

谷歌交通地图地址：http://www.google.cn/maps/vt/pb=!1m4!1m3!1i{z}!2i{x}!3i{y}!2m3!1e0!2sm!3i380072576!3m8!2szh-CN!3scn!5e1105!12m4!1e68!2m2!1sset!2sRoadmap!4e0!5m1!1e0，

平面图地址2：http://www.google.cn/maps/vt?lyrs=m@189&gl=cn&x={x}&y={y}&z={z}，

影像图地址：http://www.google.cn/maps/vt?lyrs=s@189&gl=cn&x={x}&y={y}&z={z}，

影像注记层地址：http://www.google.cn/maps/vt?lyrs=h@189&gl=cn&x={x}&y={y}&z={z}，

地形图层：http://www.google.cn/maps/vt?lyrs=t@189&gl=cn&x={x}&y={y}&z={z}