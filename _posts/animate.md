---
title: animate
date: 2018-05-22 01:11:39
tags:
---
##  动画
###  1.css3动画（transition/animation）
- transition：是过渡动画
- animation：帧动画
- transform是变形不是动画（经常依托某一种动画让元素在一定时间内实现变形效果）

### 2.js动画
- 定时器
- requestAnimationFrame
- 所谓的canvas动画就是js基于定时器完成的（canvas是一个HTML标签，可以理解为是一个画布，我们可以基于js在画布上绘制图像和效果）

###  3.flash动画（actionScript）
```
//=>需求：让BOX盒子从最左边运动到最右边(结束) [修改BOX的LEFT值即可]
let minL = 0,
    maxL = document.documentElement.clientWidth - box.offsetWidth;

//=>[固定步长的匀速运动]
// let step = 5,
//     autoTimer = setInterval(() => {
//         let curL = box.offsetLeft;//=>我们用左偏移临时代替一下LEFT值
//         curL += step;
//         if (curL >= maxL) {
//             //=>固定步长的情况下做边界判断：都是先加上步长在做判断，验证我如果走这一步会不会超，如果超了，我们直接运动到末尾即可，没超才走一步
//             box.style.left = maxL + 'px';
//             clearInterval(autoTimer);
//             return;
//         }
//         box.style.left = curL + 'px';
//     }, 17);//=>17/13MS都是比较好的动画执行时间（浏览器不会出现卡顿）

//=>[固定时间的匀速运动]
let duration = 1000,//=>总时间
    interval = 17,//=>频率:多长时间迈一步
    begin = 0,//=>起始位置
    target = maxL,//=>目标位置
    change = target - begin,//=>总距离：目标值(TARGET)-起始值(BEGIN)
    time = 0;//=>已经运动的时间
let autoTimer = setInterval(() => {
    //=>根据公式计算出当前盒子应有的位置
    time += interval;//=>time+=17;
    if (time >= duration) {
        //=>当前运动的时间超过总时间：到达边界
        box.style.left = target + 'px';
        clearInterval(autoTimer);
        return;
    }
    let curL = time / duration * change + begin;
    box.style.left = curL + 'px';
}, interval);


//1.第一种思路：步长=总距离/总时间*频率，剩下变为固定步长的匀速运动了
//2.在JS中基于定时器完成动画，不论是固定步长还是固定时间，只要算出当前盒子应该运动的位置即可(新的位置信息)

//t:TIME当前运动的时间
//d:DURATION总时间
//b:BEGIN起始位置
//c:CHANGE总距离 (TARGET-BEGIN)
// t/d:当前已经运动的时间/总时间 =>当前动画完成的百分比
// t/d*c:当前动画完成的百分比*总距离 =>当前已经走的距离
// t/d*c+b:当前走的距离+盒子的起始位置 =>当前盒子应该有的位置

```

### 封装animate
```javascript
~function () {
    let utils = (function () {
        let getCss = (ele, attr) => {
            if ('getComputedStyle' in window) {
                reg = /^-?\d+(\.\d+)?(px|pt|rem|em)?$/;
                let val = window.getComputedStyle(ele, null)[attr];
                reg.test(val) ? val = parseFloat(val) : null;
                return val;
            }
        };
        let setCss = (ele, attr, value) => {
            if (!isNaN(value)) {
                if (!/^(opacity|z-index)$/.test(attr)) {
                    value += 'px';
                }
            }
                ele['style'][attr] = value;

        };
        let setGroupCss=(ele,option)=>{
            for (let attr in option) {
                if(option.hasOwnProperty(attr)){
                    setCss(ele,attr,option[attr]);
                }
            }
        };
        let css=(...arg)=>{
            let len=arg.length;
            let fn=getCss;
           len>=3?fn=setCss:null;
            (len===2&&typeof arg[1]==='object')?fn=setGroupCss:null;
           return fn(...arg);
        };
        return{css}


    })();


    /*运动公式*/
    let effect={
        Linear:(time,duration,change,begin)=>{
            return time/duration*change+begin;
        }
    };
    window.animate=function (ele,target={},duration=1000,callback=new Function()) {
        if(duration==='function'){
            callback=duration;
            duration=1000;
        }
        let time=0,
            begin={},
            change={};
        for (let attr in target) {
            begin[attr]=utils.css(ele,attr);
            change[attr]=target[attr]-begin[attr];

        }
        clearInterval(ele.animateTimer);
        ele.animateTimer=setInterval(()=>{
            time+=17;
            if(time>=duration){
               utils.css(ele,target);
               clearInterval(ele.animateTimer);
               callback.call(ele);
               return;

            }
            let cur={};
            for (let attr in target) {
                if(target.hasOwnProperty(attr)){
                    cur[attr]=effect.Linear(time,duration,change,begin)
                } }
                utils.css(ele,cur);

        },17)
    }
}();


```