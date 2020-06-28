---
title: JavaScript深入之call、apply、bind的模拟实现
date: 2020-06-15 
tags: JavaScript深入之call、apply、bind的模拟实现
---

- call
> call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。

注意几点
1. call 改变了 this 的指向。this 参数可以传 null，当为 null 的时候，视为指向 window
2. 函数执行了
3. call 函数还能给定参数执行函数，传入的参数不确定
4. 函数可以有返回值

代码如下
```
 Function.prototype.call2 =  function (context = window, ...args) {
    context = context || window;
    // 从this中获取调用call2的函数
    const fn = this;
    context.fn = fn;

    // 获取传入的参数

    // 可以有返回值  参数数组放到要执行的函数的参数里面去
    const result = context.fn(...args);
    delete context.fn;
    return result;
}

function bar (name, age) {
    console.log(this.a);
}

let obj = {
    a: 'obj'
}

bar.call2(obj, 'zhp', 18);
```
- apply
> apply实现基本与call一致

代码如下
```
Function.prototype.apply2 =  function (context = window, arr) {
    context = context || window;
    const fn = this;
    context.fn = fn;
    let result;
    if (!arr) {
        result = context.fn();
    }else {
        const args = arr.map((item, index) => `arr[${index}]`);
         result = eval('context.fn(' + args + ')');
    }
    delete context.fn
    return result;
}

function bar (name, age) {
    console.log(this.a, name,age);
}

let obj = {
    a: 'obj'
}

bar.apply2(obj, ['zhp', 18])
```

- bind
> bind() 方法会创建一个新函数。当这个新函数被调用时，bind() 的第一个参数将作为它运行时的 this，之后的一序列参数将会在传递的实参前传入作为它的参数。(来自于 MDN )

bind函数特点：
1. 返回一个函数
2. 可以传入参数

代码如下
```
 Function.prototype.bind2 =  function (context = window, ...args) {
    context = context || window;
    // 调用bind的必须是函数
    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }
    const fn = this;
    // 通过一个空函数来进行中转：
    const fNOP = function () {};
   const foundFn =  function (...subArgs) {
       // 当 bind 返回的函数作为构造函数的时候，bind 时指定的 this 值会失效，但传入的参数依然生效。
       // 当作为构造函数时，this 指向实例，fn 指向绑定函数
       // 当作为普通函数时，this 指向 window，fn 指向绑定函数
       context = this instanceof fn ? this: context;
       return fn.call(context, ...args, ...subArgs);
   }
   fNOP.prototype = this.prototype
   foundFn.prototype = new fNOP();

   return foundFn;
}

function bar (name,age) {
    console.log(this.a, name,age);
}

let obj = {
    a: 'obj'
}

const returnFn = bar.bind2(obj, 'zhp');
const res = returnFn(18);
// const res = new returnFn(18);
console.log(res);
```

参考连接： 
[JavaScript深入之call和apply的模拟实现][callAndApplyLink]
[JavaScript深入之bind的模拟实现][bindLink]


[callAndApplyLink]: https://github.com/mqyqingfeng/Blog/issues/11  'JavaScript深入之call和apply的模拟实现'
[bindLink]: https://juejin.im/post/59093b1fa0bb9f006517b906  'JavaScript深入之bind的模拟实现'

