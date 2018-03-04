---
title: 值传递和引用引用传递
date: 2017-01-04 23:29:40
categories: 
  - 技术
  - JavaScript
tags: JavaScript
---

值传递和引用引用传递 ,对象深拷贝 浅拷贝  【引用传递就是浅拷贝的一种】

<!--more--> 


```javascript
function test1(){
      var a = "1";  
      var b = a; //值传递 只要类型不是对象[数组，object] 就会重新复制一份值 赋值给 等号 左边的变量
      console.log(1, a);
      console.log(1, b);

      b = 2;

      console.log(2, a);
      console.log(2, b);

      function fun(c){
        c = "c";
        console.log("c : ",c);
        console.log("a : ",a);
      }

      fun(a);
    }


    function test2(){
      var a = ["a","b","c"]; //创建了新的数组，赋值了给 a
      var b = a;  //如果在赋值的时候 右边的变量的类型是对象，就不是值传递，而是引用传递

      console.log("a : ", a);
      console.log("b : ", b);

      b[0] = "我是新元素";

      console.log("a : ", a);
      console.log("b : ", b);

      function fun(c){
        c[0] = "在函数里面修改了对象的值";

        console.log("c : ", c);
        console.log("a : ", a);
        console.log("b : ", b);
      }

      //fun(a);
      a = ["a","b","c"];

      console.log("new a : ",a);
      console.log("b : ", b); // ??

      // js 垃圾回收站会自己去把没用的内存清除掉
      a = []; //清空的 是给 a 一个新的内存空间, 这个空间是一个空值
      //性能会高一些
      a.length = 0; // 在原来的空间把现有的值清空
    }

    // test2();
    // js 值传递，引用传递
    // js 对象深拷贝 浅拷贝  【引用传递就是浅拷贝的一种】


    function test3(){
        var a = {
          "a" : "1"
        };

        var b = a; //直接是引用传递，后果 ： 修改 b 的时候 a 会变化, 修改 a  的时候 b 会变化

        // 我们需要的效果是赋值后，a 与 b 没有任何关联

        var c = {
          "c" : "c",
          "c1" : ["1","2","3"]
        };
        // Object.assing 拷贝对象时，如果遇到元素值的类型是对象时，不会真的拷贝，而是引用传递
        /*浅拷贝*/
        b = Object.assign({}, c, {
          "a" : 3
        }, a);
        //利用 JSON.stringify 把一个对象转换成字符串
        //在把 转换后的字符串 转换成对象 【这里会创建一个新对象出来】
        //把转换后得到的 “新对象赋值”给 b, 这个新对象跟原先的就不存在关联了

        /*这个是真正的深拷贝*/
        b = JSON.parse(JSON.stringify(b));



        c["c1"][1] = "c2"; 

        console.log(b);
        console.log(c);
    }


    test3();

```
https://www.zhihu.com/question/27114726