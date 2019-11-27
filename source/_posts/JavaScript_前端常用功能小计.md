---
title: 前端常用功能小计
date: 2019-11-07 15:20:15
categories: 
  - 技术
  - JavaScript
tags: JavaScript
---

#### JS获取元素的宽度（包含小数位）
```javascript
$(obj)[0].getBoundingClientRect().width.toFixed(2)
```

#### 深拷贝
```javascript
function deepClone(obj){
   var _obj = JSON.stringify(obj)
   var objClone = JSON.parse(_obj);
	 return objClone
}
```
<!--more-->

#### 清除火狐浏览器无图片时的边框
```javascript
img[src=""],img:not([src]){
    opacity:0;
}
```

#### 获取URL参数
```javascript
function getUrlParam(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if (r !== null) return decodeURI(r[2]); return null;
} 
```

#### 删除指定字符后的所有字符
```javascript
var a = "112233-abab"
var b = a.substring(0,a.indexOf('-'))//112233
```

#### 在指定位置插入字符
```javascript
var a = "201902"
var b = a.slice(0,4) + "-" + a.slice(4) //"2019-02"
```

#### 删除字符串中的所有空格
```javascript
var a = "6221 6223 3221 54200"
var b = a.replace(/\s*/g,"") //"62216223322154200"
```

#### 校验手机号
```javascript
var phone = "13622993358"
if (!(/^1[3456789]\d{9}$/.test(phone))){
    console.log("phone error")
}
```

#### 随机生成1-100数字
```javascript
var a = Math.floor(Math.random()*100 +1);
```

#### 复制指定文字到剪切板
```javascript
function copy(text,callback) {
  if(document.execCommand('Copy')){
    //创建input
    var inputZ = document.createElement('input');
    //添加Id,用于后续操作
    inputZ.setAttribute('id','inputCopy');
    //获取传入的值
    inputZ.value = text;
    //创建的input添加到body
    document.body.appendChild(inputZ);
    //选中input中的值(使用前面的Id)
    document.getElementById('inputCopy').select();
    //把值复制下来
    document.execCommand('Copy')
    alert('複製成功');
    //删除添加的input
    document.body.removeChild(inputZ);
    // 成功回調1
    callback(1);
  }else{
    // 失敗回調2
    callback(2);
  }
}

  //必须在触发事件中调用(如点击事件)
  copy("www.supersjz.cn",function(type){
    if(type == 1){console.log("复制成功")}
  })
```


#### 用callback做类似装饰器的功能(校验参数必填)
```javascript
function filter(callback){
	// 把所有校验都放在这个函数中
	name = document.getElementById("name").value
	if(!name){
		console.log("请输入姓名")
		return
	}
	callback()
}

//保存的方法跟下一步的方法调用同个过滤器

document.getElementById('save').onclick = function(){
	// 添加过滤器
	filter(function(){
		console.log("校验通过，继续执行")
	})
}

document.getElementById('next').onclick = function(){
	// 添加过滤器
	filter(function(){
		console.log("校验通过，继续执行")
	})
} 
```

#### 笛卡尔乘积(函ES6语法)
```javascript
  /*
  *	参数：
  *	单维数组结构 ["红色","蓝色"]
  *	多维数组结构 [["红色","蓝色"],["大号","小号"],["圆形","方形"]]
  */ 
  function descartes(arr) {
    // 判断是否多维数组结构
      if(typeof arr[0] == 'object'){ 
        return [].reduce.call(arr, function (col, set) {
            let res = [];
            col.forEach(c => {
                set.forEach(s => {
                    let t = [].concat(Array.isArray(c) ? c : [c]);
                    t.push(s);
                    res.push(t);
                })
            });
            return res;
        });
      }else{
        // 单维数组直接返回
        return arr;  
      }
  }
  var list = [["红色","蓝色"],["大号","小号"],["圆形","方形"]]
  var descartesList = descartes(list)
  console.log(descartesList) 
```

#### 获取URL参数
```javascript
  /*
  *	参数：
  *	单维数组结构 ["红色","蓝色"]
  *	多维数组结构 [["红色","蓝色"],["大号","小号"],["圆形","方形"]]
  */ 
  // 笛卡儿积组合
  function descartes(list){
    var point = {};  
    var result = [];  
    var pIndex = null;  
    var tempCount = 0;  
    var temp  = [];  
    for(var index in list){
      if(typeof list[index] == 'object'){  
        point[index] = {'parent':pIndex,'count'
        pIndex = index;  
      }  
    }  
    // 单维度数据结构直接返回
    if(pIndex == null){
      return list;  
    }  
    // 动态生成笛卡尔积
    while(true){  
      for(var index in list){  
        tempCount = point[index]['count'];  
        temp.push(list[index][tempCount]);  
      }
      result.push(temp);
      temp = [];
      while(true){
        if(point[index]['count']+1 >= list[inde
          point[index]['count'] = 0;
          pIndex = point[index]['parent'];
          if(pIndex == null){
            return result;
          }
          index = pIndex;
        }else{
          point[index]['count']++;
          break;
        }
      }
    }
  }
  var list = [["红色","蓝色"],["大号","小号"],["圆形","方形"]]
  var descartesList = descartes(list)
  console.log(descartesList) 
```

#### 获取URL参数
```javascript

```