---
title: promise
date: 2018-05-22 01:11:24
tags:
---
####  promise
他是es6中新增加的类，（new promise）为了管理js中的异步编程的，也称为promise设计模式。
三个状态：
pendding(准备：初始化成功)
fulfilled（成功）
rejected（失败）

 * Promise是ES6中新增加的内置类：目的是为了管理异步操作的
    1.new Promise() 创建类的一个实例，每一个实例都可以管理一个异步操作
     ->必须传递一个回调函数进去（回调函数中管理你的异步操作）,不传递会报错
     ->回调函数中会有两个参数
       resolve：异步操作成功做的事情（代指成功后的事件队列 =>成功后要做的所有的事情都存放到成功这个事件队列中）
       reject：异步操作失败做的事情（代指失败后的事件队列）
     ->new Promise的时候立即把回调函数执行了（Promise是同步的）
 
   2.基于Promise.prototype.then方法（还有catch/finally两个方法）向成功队列和失败队列中依次加入需要处理的事情
 
   3.如果是多个THEN掉用，不是像我们想象的依次把增加的方法执行
     异步操作成功或者失败，先把第一个THEN中的方法执行，每当执行一个THEN会返回一个新的Promise实例，这个实例管控的是第一个THEN中方法执行的是成功还是失败


```javascript
new Promise((resolve,reject)=>{
//resolve:当异步操作执行成功，我们执行resolve方法
//reject：当异步操作执行失败，我们执行reject方法
//执行一个一步的任务（new promise的时候创建一个promise实例立即把当前函数体中的异步操作执行）promise本身是同步的，他可以管理异步操作，
setTimeout(()=>{resolve(100)},1000);
console.log(1);//先输出1；
}).then((resolve)=>{console.log('ok')},(reject)=>{console.log('no')});
console.log(2);//在输出2；
```
```javascript
//=>建议不要使用THEN中的第二个参数（这样看起来很乱），而是建议我们使用Promise.prototype.catch来管理失败的情况
let promise1 = new Promise((resolve, reject) => {
    $.ajax({
        url: 'json/data2.json',
        success(result) {
            resolve(result);
        },
        error(msg) {
            reject('no');
        }
    });
});
promise1.then(result => {
    console.log('THEN1 OK', result);
    100();
    return 100;
}).catch(msg => {
    //=>第一个CATCH
    //1.异步请求失败会执行它
    //2.第一个THEN方法失败也会执行它
    console.log('CATCH1', msg);
}).then(result => {
    console.log('THEN2 OK', result);
}).catch(msg => {
    console.log('CATCH2', msg);
});
```
```javascript
//=>JS中的异常捕获（目的：把抛出异常的错误捕获到，不让其阻断浏览器的继续执行）
try {
    //=>正常执行的JS代码(可能会报错)
    1();
} catch (e) {
    //=>TRY中的代码报错了会执行CATCH
    console.log(e.message);
} finally {
    //=>不管TRY中的代码成功还是失败都会执行
}

```
```javascript

let A = function A() {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve();
        }, 1000);
    });
};

let B = function B() {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve();
        }, 1000);
    });
};

let promise = A();
promise.then(() => {
    console.log(1);
    return B();//=>如果方法中返回的一个具体值，而且执行中没有错误异常，会立即执行下一个THEN中的方法（不写RETURN也是返回的了具体值：undefined），但是如果返回的是一个PROMISR实例（并且管控了一个异步操作），只能等PROMISE完成，把成功后的结果当做具体的值返回，才能进入下一个函数执行
}).then(() => {
    console.log(2);
});


```