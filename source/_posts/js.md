---
title: js入门基础
categories: 
- web
tags: 
- js基础
---

## 数据类型

基本数据类型

> number, string, boolean, null, undefined, symbol

引用数据类型

> object 包括 子类型和包装类型
>
> 子类型有 Function, Array, Date, RegExp
>
> 包装类型有 Number, Boolean, String

## 变量

> var, let, const

var, let, const有什么区别?

```
var在全局作用域声明的变量会挂载在window对象上
let没有变量提升,只在当前作用域有效
const有变量提升,只在当前作用域有效,
	用来申明常量, 必须初始化值,常量值不能修改,,但对象的值可以修改,不能修改指针(改变引用值的地址)

```



### 运算符

> 参考MDN
>
> [表达式和运算符 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators)

判断是否相等?

```
===(严格相等)和 ==(相等)区别在于 === 不会进行类型转换再比较,推荐使用 ===
obj === null; //false
0 === false ; //false
"" === false; //false
```



## 分支语句

> if...else
>
> switch...case

## 循环语句

> for...in
>
> for...of

for...in 和 for..on有什么区别?

```
for in用来遍历对象的索引(index)
for of用来遍历数组的值(value)
```

### 闭包

> 内部函数引用外部函数的变量

```js
示例1:
const add = (() => {
  let counter = 0; // 私有变量
  return () => {
    return counter += 1; // 箭头函数可以访问外部变量
  }
})();
使用立即执行函数(自调用函数)创建一个新的作用域，避免变量污染
```



## 对象

创建对象类(推荐)

```js
class person{
    name;
    age;
    gender;
    interests;
    constructor(name,age,gender,interests){
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.interests = interests;
    }
    // name = ['Bob', 'Smith'];
    // age = 32;
    // gender = 'male';
    // interests = ['music', 'skiing'];

    bio(params) {
        return this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
    };
    greeting(){
        return 'Hi! I\'m ' + this.name[0] + '.'
    }
}

let p = new person( ['Bob', 'Smith'],32,'male',['music', 'skiing'])
p.greeting();
```

## 常用方法

[String - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)

[Number - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number)

[内置对象方法 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)

[Array - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

[Date - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)

[Promise - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[Map - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map)

[Math - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)

[Proxy - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

[RegExp(正则表达式) - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)

[ArrayBuffer - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

### promise

> promise出现是为了解决嵌套回调问题

```js
简单示例:
const newPromise = () =>{
    return new Promise((resolve,resject) => {
        resolve("success")
    }).then((res)=>{
        console.log(res);
    }).catch((err)=>{
        console.log(err);
    })
}

console.log(newPromise());
```

宏任务（macrotask）和微任务（microtask） ?

```
都是指待执行的任务，它们之间的区别在于它们的执行顺序和触发时机

宏任务通常包括整体代码中的任务、setTimeout、setInterval、requestAnimationFrame、UI 事件以及 I/O 操作等。当执行宏任务时，JavaScript 引擎会从宏任务队列中取出第一个宏任务执行，执行完毕后再执行下一个宏任务

微任务是在当前宏任务执行完成后，立即执行的任务。 Promise.then()、Promise.catch(), Object.observe(), MutationObserver, process.nextTick (Node.js环境下)等 它们也被称为 jobs

重点: 当宏任务和微任务同时存在时，它们的执行顺序如下：
首先执行同步任务，执行完同步任务后会先执行所有微任务，直到微任务队列为空。
然后执行宏任务队列中的第一个宏任务，执行完宏任务后再执行所有微任务，依此类推。
```

```js
示例1:
console.log('1');

setTimeout(function() {
  console.log('2');
  Promise.resolve().then(function() {
    console.log('3');
  });
}, 0);

Promise.resolve().then(function() {
  console.log('4');
});

console.log('5');

输出为1,5,4,2,3
```

