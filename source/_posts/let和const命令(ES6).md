
title: let和const命令(ES6)
date: 2016-01-03 23:44:30
categories: 
  - 技术
  - ES6
tags: ES6
toc: true
---
#### let命令
##### 基本用法 
ES6新增了 <code>let</code> 命令，用来声明变量。它的用法类似于 <code>var</code>，但是所声明的变量，只在let命令所在的代码块内有效。
<!--more-->

```javascript
{
  let a = 10;
  var b = 1;
}
a // ReferenceError: a is not defined.
b // 1
```
以上分别用 <code>let</code> 和 <code>var</code>声明了两个变量。然后在代码块之外调用这两个变量，结果<code>let</code>声明的变量报错，
<code>var</code>声明的变量返回了正确的值。这表明，let声明的变量只在它所在的代码块有效。

常用的for循环的计数器，就很合适使用let命令。
```javascript
for (let i = 0; i < 10; i++) {}

console.log(i);
//ReferenceError: i is not defined
```
以上for循环i只在循环体内有效，在循环体外引用就会报错。

<code>let</code>与<code>var</code>在for循环的比较

```javascript
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6  数组a[0-9]的值与i的值一一对应
```
使用let，声明的变量仅在块级作用域内有效，最后输出的是6。
```javascript
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10  数组a[0-9]的值都是10
```
变量i是var声明的，在全局范围内都有效。所以每一次循环，新的i值都会覆盖旧值，导致最后输出的是最后一次i的值。
##### 不存在变量提升 

let不像var那样会发生“变量提升”现象。所以，变量一定要在声明后使用，否则报错。

```javascript
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```
#####  暂时性死区 
只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

```javascript
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```
以上存在全局变量tmp，但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个块级作用域，所以在let声明变量前，对tmp赋值会报错。
ES6明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。
```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```
“暂时性死区”也意味着typeof不再是一个百分之百安全的操作。
```javascript
typeof x; // ReferenceError
let x;
```
以上变量x使用let命令声明，所以在声明之前，都属于x的“死区”，只要用到该变量就会报错。因此，typeof运行时就会抛出一个ReferenceError。
作为比较，如果一个变量根本没有被声明，使用typeof反而不会报错。
```javascript
typeof undeclared_variable // "undefined"
```
undeclared_variable是一个不存在的变量名，结果返回“undefined”。所以，在没有let之前，typeof运算符是百分之百安全的，永远不会报错。现在这一点不成立了。这样的设计是为了让大家养成良好的编程习惯，变量一定要在声明之后使用，否则就报错。

有些“死区”比较隐蔽，不太容易发现。
```javascript
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错
```
调用bar函数之所以报错（某些实现可能不报错），是因为参数x默认值等于另一个参数y，而此时y还没有声明，属于”死区“。如果y的默认值是x，就不会报错，因为此时x已经声明了。
```javascript
function bar(x = 2, y = x) {
  return [x, y];
}
bar(); // [2, 2]
```
ES6规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。这样的错误在ES5是很常见的，现在有了这种规定，避免此类错误就很容易了。

总之，暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。

##### 思考题
思考以下tmp的值分别打印出什么？
```javascript
var tmp = 123
if (true) {
  tmp = 'abc'
  let tmp;
}
tmp ?
```

```javascript
var tmp = 123
if (true) {
  let tmp = 'abc'
  tmp ?
}

```

```javascript
var tmp = 123;
if (true) {
  let tmp = 'abc'; 
}
 tmp ?
```

```javascript
var tmp = 123;
if (true) {
   tmp = 'abc'
}
tmp ?
```
```javascript
let tmp = 123
if (true) {
   var tmp = 'abc'
}
tmp ?
```

#### const命令 
<code>const</code>声明一个只读的常量。一旦声明，常量的值就不能改变。
```javascript
const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```
<code>const</code>一旦声明变量，就必须立即初始化，不能留到以后赋值。
```javascript
const foo;
// SyntaxError: Missing initializer in const declaration
```
<code>const</code>的作用域与let命令相同：只在声明所在的块级作用域内有效。
```javascript
if (true) {
  const MAX = 5;
}

MAX // Uncaught ReferenceError: MAX is not defined
```
<code>const</code>命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
也就是说必须先声明后使用
```javascript
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```
<code>const</code>声明的常量，也与<code>let</code>一样不可重复声明。
```javascript
var message = "Hello!"
let age = 25

// 以下两行都会报错
const message = "Goodbye!" //Identifier 'message' has already been declared
const age = 30  //Identifier 'message' has already been declared
```