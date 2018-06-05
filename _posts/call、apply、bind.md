---
title: call、apply、bind
date: 2018-05-22 01:07:18
tags:
---
###   call  apply  bind
> 都是天生自带的方法(Function.prototype)，所有的函数都可以调取这三个方法
> `三个方法都是改变THIS指向的`
####  call
`call`
> fn.call(context,para1,...)
> 把fn方法执行，并且让fn方法中的this变为context,而para1...都是给fn传递的实参
1.非严格模式下如果参数不传或者第一个传递的是null、undefined，this指向window
2.严格模式下第一个参数是谁，this就指向谁（包括null、undefined）不传this是undefined

```javascript
//=>非严格模式
function fn(num1,num2){
	console.log(this);
}
var obj={fn:fn};
fn();//=>this:window
obj.fn();//=>this:obj
var opp={};
//opp.fn();//=>报错:opp中没有fn这个属性
fn.call(opp);//=>this:opp num1&&num2都是undefined
fn.call(1,2);//=>this:1 num1=2 num2=undefined
fn.call(opp,1,2);//=>this:opp num1=1 num2=2
//->CALL方法的几个特殊性
fn.call();//=>this:window   num1&&num2都是undefined
fn.call(null);//=>this:window
fn.call(undefined);//=>this:window
```
```javascript
//=>JS严格模式下
"use strict";
fn.call();//=>this:undefined
fn.call(undefined);//=>this:undefined
fn.call(null);//=>this:null
```
####  apply
> apply的语法和call基本一致，作用原理也基本一致，唯一的区别：apply把传递给函数的实参以数组形式存放（但是也相当于在给函数一个个的传递实参值）
```javascript
fn.call(null,10,20,30);
fn.apply(null,[10,20,30]); //=>传递给fn的时候也是一个个的传递进去的
```
####  bind
`bind`预处理机制
> 也是改变THIS的方法，它在IE6~8下不兼容；它和call(以及apply)改变this的原理不一样，区别于立即执行还是等待执行。
把所有参数传给点前面的方法，返回一个接受参数后的小函数，返回值是函数的定义
预处理机制：提前把所有的事情都弄好，最终函数执行需要手动运行

```javascript
fn.call(opp,10,20); //=>把fn执行,让fn中的this变为opp,并且把10&&20分别传递给fn

fn.bind(opp,10,20); //=>预先让fn中的this指向opp,并且把10和20预先传递给fn,此时的fn没有被执行(只有当执行的时候this和实参才会起到应有的作用)
//=>需求：点击box这个盒子的时候，需要执行fn，并且让fn中的this指向opp
oBox.onclick=fn; //=>点击的时候执行了fn,但此时fn中的this是oBox

oBox.onclick=fn.call(opp); //=>绑定事件的时候就已经把fn立即执行了(call本身就是立即执行函数),然后把fn执行的返回值绑定给事件

oBox.onclick=fn.bind(opp);
//=>fn.bind(opp)：fn调取Function.prototype上的bind方法，执行这个方法返回了一个匿名函数
/*
 * function(){
 *     fn.call(opp);
 * }
 */
oBox.onclick=function(){
	//=>this:oBox
	fn.call(opp);
}
```
> 思考题
```javascript
function fn1(){console.log(1);}
 function fn2(){console.log(2);}
 fn1.call(fn2);//=>找到CALL-AA把它执行,CALL-AA中的THIS是FN1,第一个参数传递的是FN2  =>在CALL-AA中执行的是FN1 =>1

 fn1.call.call(fn2);//=>找到CALL-AA让它执行,CALL-AA中的THIS是FN1.CALL,第一个参数是FN2  (把FN1.CALL中的THIS变为FN2，再让FN1.CALL执行  =>先找到CALL-AA，把它执行，只不过此时它中的THIS是FN2 =>让FN2中的THIS变为UNDEFINED，因为执行FN1.CALL的时候没有传递参数值，然后让FN2执行)  =>2

 Function.prototype.call(fn1);//=>先找到CALL-AA把它执行，它中的THIS是Function.prototype =>让F.P中的THIS变为FN1,然后让F.P执行,F.P是一个匿名函数也是一个空函数，执行没有任何的输出
Function.prototype.call.call(fn1);//=>先找到CALL-AA把它执行，它中的THIS是F.P.CALL =>把F.P.CALL中的THIS修改为FN1,让F.P.CALL执行  =>F.P.CALL(CALL-AA)第二次把它执行(此时它里面的THIS已经是FN1) =>这一次其实在CALL-AA中是让FN1执行 =>1
```
> 查看函数原型上的方法：
call/apply/bind->改变调用主体的this关键字
call()第一个参数：用来改变`.`前面方法的this关键字，从第二个参数开始，以散列式的方式给`.`前面的方法传参.---散列式.
fn.apply()第一个参数：用来改变`.`前面方法的this关键字，第二个参数是用来给`.`前面的方法传参（把所有的参数放在数组里传给`.`前面的方法）---打包式.

非严格模式下
> call/apply第一个参数不传，传null,传undefined->`.`前面方法里的this都是window
严格模式下-》规范
好处：
1.更加安全高效
2.提高编译器编译代码的速度
3.跟高版本浏览器接轨
第一个参数不传是undefined，其他传什么就是什么
fn1.call.call.call.call(fn2);
最后一个call作用
1.让点前面方法里的this关键字改成fn2->call方法里this->fn2
2.让点前面方法运行->function.prototype.call()->this()->fn2()
