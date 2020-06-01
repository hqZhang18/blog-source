---
title: JavaScript设计模式-工厂模式
date: 2019-11-29 09:54:02
categories: 
  - 技术
  - JavaScript
tags: 工厂模式
---

工厂模式是最常用的实例化对象模式，是用工厂方法代替new操作的一种模式
<!--more-->
### 简单工厂模式
- 优点：能解决多个相似的问题
- 缺点：不能识别对象的类型

```javascript
function Factory(name,age,sex){
    let person = {};
    person.name = name;
    person.age = age;
    person.sex = sex;
    person.say = function(){
        return this.name;
    };
    return person;
}

let tom = new Factory('Tom','10','male');
let jerry = new Factory('Jerry','20','female');
```
工厂模式是为了解决多个类似对象声明问题，也就是重复实例化对象的问题

### 复杂工厂模式
> 将其成员对象的实例化推迟到子类中，子类可以重写父类接口方法以便创建时指定独自的对象类型
> 父类只对创建过程中的一般性问题进行处理，子类继承，但子类之间相互独立，具体业务再各自实现
> 父类变为抽象类，不能被实例

```javascript
//工厂构造函数
function Factory(name){
    this.name = name;
    this.say = function(){
       return this.name;
    }
}
Factory.prototype = {
    constructor: Factory,
    createFactory: function(){
        throw new Error('父类抽象类无法直接调用，需要子类重写');
    }
}

//原型继承
function extend(sub,sup){
    //定义空函数
    let F= function(){};
    //空函数原型为父类原型
    F.prototype = sup.prototype;
    //实例化空函数传递给子类原型
    sub.prototype = new F();
    //使子类构造器指向自身
    sub.prototype.constructor = sub;
    //保存父类原型
    sub.sup = sup.prototyp;
    //检测父类原型为父类自身
    if(sup.prototype.constructor === Object.prototype.constructor){
        sup.prototype.constructor = sup;
    }
}

function Person(name){
    this.name = name;
    Factory.call(this,name);
} 

extend(Person,Factory);

Person.prototype.createFactory = function(){
    switch(this.name){
        case 'Tom': return {name: 'Tom', age: 10, sex: 'male'};
        case 'Jerry': return {name: 'Jerry', age: 20, sex: 'female'};
        default : return {};
    }
}

let Tom = new Person('Tom');
let tom1 = Tom.createFactory();
```