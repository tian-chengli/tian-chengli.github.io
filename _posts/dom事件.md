---
title: dom事件
date: 2018-05-22 01:12:12
tags:
---
###  dom事件
> - 1.什么是事件？
>  事件就是一件事情或者行为（对于元素来说他的很多事件都是天生自带）只要我们去操作这个元素就会触发事件。
事件就是元素天生自带的行为，我们操作元素就会触发相关的事件行为


> - 2.事件绑定：给元素天生自带的事件行为绑定方法，当事件触发会把对应的方法执行
- 3.元素天生自带的事件
 > **鼠标事件**
`click`:点击（pc端是点击，移动端的click代表单击，并且使用click会有300ms的延迟）
`dblclick`:双击
`mouseover`:鼠标经过
`mouseout`:鼠标移出
`mouseenter`:鼠标进入
`mouseleave`:鼠标离开
`mousemove`:鼠标移动
`mousedown`:鼠标按下（鼠标左右键都起作用他是按下即触发，click是按下抬起才出发，而且是先把down和up先触发，click才触发）
`mouseup`:鼠标抬起
`mousewheel`:鼠标滚轮滚动
**键盘事件**
`keydown`:键盘按下
`keyup`:键盘抬起
`keypress`:和keydown类似只不过keydown返回的是键盘码。keypress返回的是ASCII码值
`input`:由于pc有实体物理键盘，可以监听到键盘的按下和抬起，但是`移动端`是虚拟的键盘，所以keydown和keyup在大部分手机上都没有，我们使用input事件统一代替他们（内容改变事件）

**表单元素常用的事件**
`focus`：获取焦点
`blur`:失去焦点
`change`:内容改变
**其他常用事件**
`load`:加载完成
`unload`:
`beforeunload`:
`scroll`:滚动条滚动事件
`resize`：大小改变事件window.onresize=function(){}当浏览器窗口大小发生改变会触发这个事件执行对应的事情。
`readystatechange`:ajax状态改变
**移动端手指事件**
`gesture`:多指操作
`touchstart`:手指按下
`touchmove`:手指移动
`touchend`：手指离开
`touchcancel`:因为意外情况导致手指操作取消
`gesturestart`:多指按下
`gesturechange`:多指改变
`gestureend`:手指离开
**h5中的audio、video音频事件**
`canplay`；可以播放（播放过程中可能出现由于资源没有加载完成导致卡顿
`canplaythrough`：资源加载完成可以正常无障碍播放

事件绑定
>**DOM0级事件绑定**
[element].onxxx=function(){};


----------


>**DOM2级事件绑定**
[element].addEventListener('xxx',function(){},false);
[element].attachEvent('onxxx',function(){});[ie6-8];


----------
> 给元素的事件行为绑定方法，当行为触发的时候浏览器会把绑定的方法执行
    1.方法中的this：当前操作的元素（除非自己改动this，比如箭头函数，或者bind）
    2.事件绑定属于异步操作，绑定的时候方法没有执行，还是创建方法的阶段呢，当行为触发浏览器才会把方法执行。（当然也有变态的执行方式：bo.onclick(),这样执行仅仅是把它当做一个变量和函数执行，和事件没啥关系。）
    3.浏览器不仅把这个方法执行了，还记录了当前本次操作的相关信息（如果是鼠标点击，浏览器记录点击的位置，点的是谁等信息），把这些信息都存储到一个对象中（这个对象就是实践对象：记录当前本次操作信息的对象）；更重要的是标准浏览器会把这个对象（堆内存）传递给执行的方法。我们可以在方法中通过形参或者实参集合等方式受到传递的事件对象信息；

>目的：给当前元素的某个事件绑定方法不管是基于dom0还是dom2都是为了触发元素的相关行为的时候能做点事情也就是把绑定的方法执行；不仅把方法执行了而且浏览器还给方法传递了一个实参信息值===》这个值就是`事件对象ev`
>目的：事件对象中记录了很多属性名和属性值，这些信息中包含了当前操作的基础信息，例如鼠标点击位置的x/y轴坐标，鼠标点击的是谁（事件源）等信息

```javascript
    box.onclick=function(ev){//定义一个形参ev用来接收方法执行的时候，浏览器传递的信息值（事件对象mouseevent鼠标事件对象，keyboardevent键盘事件对象，event普通事件对象。。）
    //目的：事件对象中记录了很多属性名和属性值，这些信息中包含了当前操作的基础信息，例如鼠标点击位置的x/y轴坐标，鼠标点击的是谁（事件源）等信息

    console.log(ev);}
```
>   `ev.target`:事件源（操作的是哪个元素） `ev.srcElement;`低版本浏览器
 `ev.clientX/ev.clientY`:当前鼠标触发点距离当前窗口左上角的x/y轴坐标
    `ev.pageX/ev.pageY`:当前鼠标触发点距离body（第一屏）左上角的x/y轴坐标。
    `ev.preventDefault()`:阻止默认行为
    `ev.stopPropagation()`:阻止事件的冒泡传播
     `ev.cancelBubble = true;`//=>低版本阻止冒泡传播
   `ev.type`:当前事件类型
   ```javascript
      [用到其中的几个属性,需要处理兼容]
       box.onclick=function(ev){
       ev=ev||window.event;
       let target=ev.target||ev.srcElement,
       pageY=ev.pageY||(ev.clientY+(document.documentElement.scrollTop||document.body.scrollTop))};
       [很多地方都用到这些属性,而且用的多]
       function handleEvent(ev){
      if(window.event&&!ev){//低版本浏览器，我们需要处理的不仅仅是把ev赋值，还要把高版本中有低版本没有的属性给ev加上
      ev=window.event;
      ev.target=ev.srcElement;
      ev.pageX=ev.clientX+(document.documentElement.scrollLeft||document.body.scrollLeft);
      ev.pageY=ev.clientY+(document.documentElement.scrollTop||document.body.scrollTop);
      ev.which=ev.keyCode;
      ev.preventDefault=function(){
      ev.return=false;
    }
   ev.stopPropagation=function(){
   ev.cancelBubble=true
   }
      }
       return ev;
       }
       box.onclick=function(ev){
       ev.handleEvent(ev);
       let target=ev.target;
       }
   ```


   ----------
   > **keyboardEvent**
   > ev.code:当前按键“keyE”
   > ev.key:当前按键'e'
   > ev.which/ev.keycode:当前按键的键盘码69


   ----------
   >常用的键盘码
   >  `左 - 上 - 右 - 下` ：37-38-39-40
   >  `Backspace删除键`：18
   >  `Enter`：13
   >  `Space`：32
   > `Delete`：46
   >
   > `Shift`：16
   > `Alt`：18
   > `Ctrl`：17
   > `Esc`：27
   > `F1-F12`：112-123
   > `0-9`：48-57
   > `a-z`：小写字母
```javascript
box.onclick = function(ev){
	if(!ev){
	//兼容思想：低版本没有的属性，我们手动设置一些：按照自己有的先获取到值，然后赋值给标准对应的新属性（经过判断处理后，低版本中也有target/pageX/pageY这些属性），后期在使用的时候，直接按照高版本的使用即可
		ev = window.event;
		console.log(ev.srcElement); //=>ev.srcElement是获取事件源（标准浏览器使用的是ev.target）
		console.log(ev.ev.pageX); //=>低版本浏览器的事件对象中不存在pageX/pageY
		ev.target = ev.srcElement;
		ev.pageX = ev.clientX+(document.documentElement.scrollLeft||document.body.scrollLeft)
		ev.pageY = ev.clientX+(document.documentElement.scrollTop||document.body.scrollTop)
		ev.which = ev.keyCode;
		//ev.preventDefault  ev.stopPropagation 低版本不存在
		ev.preventDefault = function(){
			ev.returnValue = false; //低版本阻止默认行为
		}
		ev.stopPropagation = function(){
			ev.cancelBubble= true; //低版本阻止冒泡传播
		}

	}
	//=>直接按照高版本的规则使用
	console.log(ev.target,ev.which);
}
//兼容处理方法二
box.onclick = function(){
        //用到谁，给谁处理兼容
        ev=ev || window.event;
        var target = ev.target || ev.srcElement;
        ev.preventDefault()?ev.preventDefault()():ev.returnValue=false;
    }
```
####  事件的默认行为
>事件本身就是天生就有的，某些事件触发即使你没有绑定方法也会存在一些效果，这些默认的效果就是`事件的默认行为`
 1.点击A实现页面跳转
    2.锚点定位（href=“元素的ID”），点击的时候url中设置对应的hash值（#xxx），页面加载完成后会定位到ID和hash值相同的盒子位置。真实项目中就是一个普通按钮，不想实现页面跳转或者锚点定位。此时我们需要阻止点击A的时候的默认行为。
    结构上阻止：`href="JavaScript:;"`或者void(0),null;undefined;
    js方法阻止：
```
link.onclick=function（ev）{
    ev=ev||window.event;
    ev.preventDefault?ev.preventDefault():ev.returnValue=false;
    }
```


```
 或者link.onclick=function(){
    return false;
    //原理：点击A的时候首先触发的是click其次才会触发它的默认行为，我们在click中返回false其意思是阻止下一步继续操作。
    }
```

基于hash值可以实现spa单页面应用
**input标签也有自己的默认行为**
1.输入内容可以呈现到文本框中
2.输入内容的时候会把之前输入的一些信息呈现出来，并不是所有浏览器和所有情况下都有

```
    //真实项目中我们根据需求可能会组织文本框输入内容，此时其实就是阻止他的默认行为
userInp.onkeydown=userInp.onkeyup=function(ev){
let val=this.value.trim(),
len=val.length;
if(len>10){
this.value=val.substr(0,10);超过十位的截掉
有值的键是不允许输入的del/back-space/space/shift/ctrl/alt/tab...
}
}
```

**submit按钮也存在默认行为**
1.点击按钮页面会刷新

```
<from action='wangzhi'><input type='submit'></from>
```
####   事件的传播机制
> 冒泡传播：触发当前元素的某一个事件（点击事件）行为不仅当前元素事件行为触发，而且其祖先元素的相关事件行为也会一次被触发，这种机制就是`事件的冒泡传播机制`。
>-  捕获阶段：点击inner的时候首先会从最外层开始向内查找的（找到操作的事件源），查找的目的是构建出冒泡传播阶段需要传播的路线（查找就是按照HTML层级结构找的）
- 目标阶段：把事件源的相关操作行为触发（如果绑定了方法则把方法执行）
- 冒泡传播：按照捕获阶段规划的路线自内而外把当前事件源的祖先元素的相关事件行为一次触发（如果某一个祖先元素事件行为绑定了方法，则把方法执行，没绑定方法，行为触发了，什么都不做，继续向上传播即可）


```
  xxx.onxxx=function(){};dom0事件绑定，给元素的事件行为绑定方法这些都是在当前元素事件行为的冒泡阶段或者目标阶段执行的
    xxx.addEventListener('xxx',function(){},false)第三个参数false也是控制绑定的方法在事件传播的冒泡阶段或者目标阶段执行，只有第三个参数为true才代表让当前方法在事件传播的冒泡阶段或者目标阶段执行

```

> 不同浏览器对最外层祖先元素的定义是不一样的
谷歌：window->document->html->body...
IE高：window->html->body...
IE低：html->body...
**关于事件对象的一些理解**
1.事件对象是用来存储当前本次操作的相关信息，和操作有关，和元素无必然关联，
2.当我们基于鼠标或者键盘等操作的时候，浏览器会把本次操作的信息存储起来（标准浏览器存储到默认的内存中（自己找不到），IE低版本存储到window.event中了）存储的值是一个对象（堆内存）;操作肯定会触发元素的某个行为，绑定的方法，执行此时标准浏览器会把之前存储的对象（准确来说是堆内存地址）当做实参传递给每一个执行方法，所以操作一次即使更多方法中都有ev，但是存储的值都是一个（本次操作信息的对象而已）
**mouseenter和mouseover区别**
over属于滑过覆盖事件，从父元素进入到子元素属于离开了父元素，会触发父元素的out触发子元素的over
enter属于进入，从父元素进入子元素，并不算离开父元素，不会触发父元素的leave触发子元素的enter。
enter和leave阻止了事件的冒泡传播，而over和out还存在冒泡传播。
所以对于父元素嵌套子元素这种情况使用over会发生很多不愿意操作的事情，此时我们使用enter会更简单，操作方便，所以真实项目中用enter的使用会比over多。
####  事件委托
> 利用事件的冒泡传播机制，如果一个容器的后代元素中很多元素的点击行为都要做一些处理此时我们不需要像以前一样一个一个获取然后绑定了，我们只需要给容器的click绑定方法即可，这样不管点击是哪个后代元素，都会根据冒泡传播的传递机制，把容器的click行为触发，把对应的方法执行，根据事件源我们可以知道点击的是谁从而做不同的事情

####  初步了解JS中事件绑定的方式
> DOM0事件绑定
```javascript
oBox.onclick=function(e){
	//=>this:oBox
	e=e||window.event;
}
oBox.onmouseenter=function(e){};
...
```

> DOM2事件绑定
```javascript
//=>标准浏览器
oBox.addEventListener('click',function(e){
	//=>this:oBox
	//=>e:事件对象
},false);
//=>false:让当前绑定的方法在冒泡传播阶段执行（一般都用FALSE）
//=>true:让当前绑定的方法在捕获阶段执行(一般不用)

//=>IE6~8
oBox.attachEvent('onclick',function(e){
	//=>e:事件对象，不同于DOM0事件绑定，使用attachEvent绑定方法，当事件触发方法执行的时候，浏览器也会把事件对象当做实参传递给函数（传递的值和window.event是相同的），所以IE6~8下获取的事件对象对于：pageX\pageY\target...依然没有，还是存在兼容性（事件对象兼容处理在DOM2中依然存在）
});
//=>此时绑定的方法都是在冒泡传播阶段执行
```

> 有DOM0和DOM2事件绑定，那么DOM1事件绑定呢？
> 因为在DOM第一代升级迭代的时候，DOM元素的事件绑定方式依然沿用的是DOM0代绑定的方式，在此版本DOM中，事件绑定没有升级处理

####  DOM0事件绑定和DOM2事件绑定的区别
> **`DOM0事件绑定的原理`**
> 1、给当前元素对象的某一个私有属性（onxxx这样的私有属性）赋值的过程（之前属性默认值是null，如果我们给赋值一个函数，相当于绑定了一个方法）
> 2、当我们赋值成功（赋值一个函数），此时浏览器会把DOM元素和赋值的函数建立关联，以及建立DOM元素行为操作的监听，当某一个行为被用户触发，浏览器会把相关行为赋值的函数执行
>
> 特点：
```javascript
//=>1、只有DOM元素天生拥有这个私有属性（onxxx事件私有属性），我们赋值的方法才叫做事件绑定，否则属于给当前元素设置一个自定义属性而已
document.body.onclick=function(){}//->事件绑定
/*
 * 手动点击页面中的BODY触发方法执行
 * document.body.onclick() 这样执行也可以
*/

document.body.onzhufeng=function(){}//->设置自定义属性
/*
 * 只能document.body.onzhufeng()这样执行
 */

//=>2、移除事件绑定的时候，我们只需要赋值为null即可
document.body.onclick=null;

//=>3、在DOM0事件绑定中，只能给当前元素的某一个事件行为（某一个事件私有属性）绑定一个方法，绑定多个方法，最后一次绑定的会把之前绑定的都替换掉
document.body.onclick=function(){
	console.log(1);
}
document.body.onclick=function(){
	console.log(2);
}
//=>点击BODY只能输出2，因为第二次赋值的函数把第一次赋值的函数给替换了
```

> **`DOM2事件绑定的原理`**
> 1、我们DOM2事件绑定使用的addEventListener/attachEvent都是在EventTarget这个内置类的原型上定义的，我们调取使用的时候，首先通过原型链找到这个方法，然后执行完成事件绑定的效果
>
> 2、浏览器首先会给当前元素的某一个事件行为开辟一个事件池（事件队列）[其实是浏览器有一个统一的事件池，我们每个元素的某个行为绑定的方法都放在这个事件池中，只是通过相关的标识来区分的]，当我们通过addEventListener做事件监听的时候，会把绑定的方法存放在事件池中
>
> 3、当元素的某一个行为触发，浏览器会到对应的事件池中，把当前存放在事件池中的所有方法，依次按照存放的先后顺序执行
>
> 特点：
```javascript
//=>1、所有DOM0支持的事件行为，DOM2都可以使用，不仅如此，DOM2还支持一些DOM0没有的事件行为：DOMContentLoaded...

window.onDOMContentLoaded === undefined; //=>DOM0中没有这个属性

window.addEventListener('DOMContentLoaded',function(){
	//=>标准浏览器中兼容这个事件：当浏览器中的DOM结构加载完成，就会触发这个事件（也会把绑定的方法执行）
},false);

window.attachEvent('onDOMContentLoaded',function(){
	//=>IE6~8中的DOM2也不支持这个事件
});

//=>2、DOM2中可以给当前元素的某一个事件行为绑定‘多个不同的方法’（因为绑定的所有方法都存放在事件池中了）
function fn1(){
	console.log(1);
}
function fn2(){
	console.log(2);
}
function fn3(){
	console.log(3);
}
document.body.addEventListener('click',fn1,false);
document.body.addEventListener('click',fn3,false);
document.body.addEventListener('click',fn2,false);
document.body.addEventListener('click',fn3,false);//=>本次向事件池中存储的时候，发现fn3已经在事件池中存在了，不能再存储了

//3、DOM2事件绑定的移除比较麻烦一些，需要和绑定的时候：事件类型、绑定的方法、传播阶段，三个完全一致才可以移除掉
document.body.removeEventListener('click',fn2,false);

document.body.addEventListener('click',function(){
	console.log(1);
},false);

document.body.removeEventListener('click',function(){
	console.log(1);
},false);
//=>DOM2事件绑定需要我们养成‘未雨绸缪’的能力，绑定方法的时候尽量不用匿名函数，为后期可能会把方法在事件池中移除掉做准备
```
>  dom0:
   box.onclick=function(){};每一个元素对象都是对应类的实例，浏览器天生为其设置了很多私有属性和公有的属性方法，而onclick就是其中的一个私有属性（事件类私有属性，还有很多其他的事件私有属性，）
这些属性值默认为null
dom0事件绑定的原理：就是给元素的某一个事件私有属性赋值（浏览器会建立监听机会，当我们触发元素的某个行为，浏览器会把属性中赋的值去执行）
dom0事件绑定，只允许给当前元素的某个事件行为绑定一个方法，多次绑定后面绑定的会替换前面绑定的，以最后一次绑定的方法为主

> dom2：
box.addEventListener('click',function(){},false)还有removeEventListener('click',function(){},false)移除，（使用的方法都是EventTarget.prototype定义的），完成时间帮顶是基于事件池机制完成的。
在IE低版本当中使用的是attachEvent来处理的，box.attachEvent('onclick',function(){})移除使用的是dettachEvent


 > dom2事件绑定可以给当前元素的某一个事件行为绑定“多个不同的方法”。
dom2事件绑定的兼容
谷歌vsie高版本
在一处事件绑定的时候如果移除操作发生在正要执行的方法之前，如点击的时候，正要执行F8但是在执行Fn4的时候沃恩吧fn8从是坚持中移除了，谷歌下是立即移除生效，第一次也不再执行FN8了而IE是当前本次不生效，下一次点击才生效，第一次点击还是要执行FN8的
标准vsIE低版本
标准：addEventListener/removeEventListener
Ie低版本：attchEvent/dettachEvent
1.this问题：标准浏览器中行为触发方法执行方法中的this是当前元素本身，IE低版本中this执行了window
2.重复问题：标准浏览器中的是坚持是默认去重复的，同一个元素的同一个事件行为不能出现相同的绑定方法，但是IE低版本的事件池机制没有那么完善，不能默认去重，也就是可以给同个元素的同个事件绑定相同的方法了
3.顺序问题：标准浏览器是按照向事件池中存放的顺序依次执行的，而IE低版本是乱序执行的没有规律
IE低版本浏览器出现的所有问题都是由于本身自带的事件池机制不完善导致的


> `dom0和dom2事件绑定的区别`：
1.机制不同：
dom0采用给私有属性赋值，所以只能绑定一个方法
dom2采用的是事件池机制，能绑定多个不同的方法
2.移除的操作不同：
box.onclick=function(){};
box.onclick=null;赋值为null就移除了
box.addEventListener('click',function(){console.log(1)},false);
box.removeEventListener('click',function(){console.log(1)},false);
dom2在移除的时候必须清楚要移除哪一个方法才能在事件池中移除掉所以基于dom2做事件绑定，我们要有瞻前顾后的思路，也就是绑定的时候考虑一下如何移除（技巧不要绑定匿名函数，都绑定实名函数）
3.dom2事件绑定中增加了一些domo无法操作的事件行为，例如DOMContentLoaded事件（当页面中的HTML结构加载完成就会触发执行）

> JQ中的事件绑定
 on / off：基于DOM2事件绑定实现事件的绑定和移除（兼容了所有的浏览器）
one：只绑定一次，第一次执行完成后，会把绑定的方法移除(基于ON/OFF完成的)
click / mouseover / mouseout ...：JQ提供快捷绑定方法，但是这些方法最后都是基于ON/OFF完成的
delegate：事件委托方法（1.7版本以前用的是live方法）
 bind / unbind：正常绑定
 **window.onload和$(document).ready()**
```
window.onload = function () {
        //=>当页面中的资源都加载完成（HTML结构加载完、CSS和JS等资源加载完成等）才会触发执行
    };
    // window.addEventListener('load',function(){}); //=>这样处理也可以执行多次了

    //=>$(document).ready(function(){})
    //原理：基于DOMContentLoaded完成的(IE中用的是onreadystatechange监听的，在document.readyState === "complete"时候执行函数)
    $(function () {
        //=>当页面中的HTML结构加载完成就会执行

    });

    $(function(){
        //=>基于DOM2事件绑定的，所以在同一个页面中可以执行多次（绑定多个不同的方法），当结构加载完成，会依次执行这些方法
    });

```

####  window.onload和$(document).ready()的区别
> window.onload：当浏览器中所有的资源内容（DOM结构、文本内容、图片...）都加载完成，触发load事件
> 1、它是基于DOM0事件绑定完成的，所以在同一个页面中只能给它绑定一个方法（绑定多个也以最后一个绑定的为主）
>
> 2、如果想在一个页面中使用多次，我们应该是基于DOM2事件绑定的
```javascript
function fn1(){
	//=>第一件事情
}
function fn2(){
	//=>第二件事情
}
window.addEventListener('load',fn1,false);
window.addEventListener('load',fn2,false);

...
```

> \$(function(){}) 或者 $(document).ready(function(){})
> 当文档中的DOM结构加载完成就会被触发执行，而且在同一个页面中可以使用多次
>
> 1、JQ中提供的方法，JQ是基于DOMContentLoaded这个事件完成这个操作的
> 2、JQ中的事件绑定都是基于DOM2事件绑定完成的
> 3、但是DOMContentLoaded在IE6~8下使用attachEvent也是不支持的，JQ在IE6~8中使用的是readystatechange这个事件处理的

#### DOM2事件绑定的兼容处理
> 语法上的兼容处理
> [标准]
> curEle.addEventListener('type',fn,false);
> [IE6~8]
> curEle.attachEvent('ontype',fn);
```javascript
//=>ON:给当前元素的某个事件绑定某个方法
var on = function (curEle, type, fn) {
    if (document.addEventListener) {
        //=>标准浏览器
        curEle.addEventListener(type, fn, false);
        return;
    }
    //=>IE6~8
    curEle.attachEvent('on' + type, fn);
};

//=>OFF:移除当前元素某个事件绑定的某个方法
var off = function (curEle, type, fn) {
    if (document.removeEventListener) {
        curEle.removeEventListener(type, fn, false);
        return;
    }
    //=>IE6~8
    curEle.detachEvent('on' + type, fn);
};
```

> 除了语法上的区别，在处理的机制上有一些区别
>
> 在IE6~8中使用attachEvent做事件绑定（把方法存放在当前元素指定事件类型的事件池中）
>
> 1、顺序问题：当事件行为触发，执行对应事件池中存放方法的时候，IE低版本浏览器执行方法的顺序是乱序（标准浏览器是按照绑定的先后顺序依次执行的）
>
> 2、重复问题：IE低版本浏览器在向事件池中增加方法的时候，没有去重机制，哪怕当前方法已经存放过了，还会重复的添加进去（标准浏览器的事件池机制很完善，可以自动去重：已经存在过的方法不允许在添加进来）
>
> 3、THIS问题：IE低版本浏览器中，当事件行为触发，把事件池中方法执行，此时方法中的this指向window，而不是像标准浏览器一样，指向当前元素本身
>
> 究其根本：其实都是IE低版本浏览器对于它内置事件池处理机制的不完善导致的
>
> DOM2事件绑定兼容处理的原理：告别LOW的IE6~8的内置事件池，而是自己创建一个类似于标准浏览器的“自定义事件池”，标准浏览器不需要处理兼容，只有IE6~8中才需要处理兼容


