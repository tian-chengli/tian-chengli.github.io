---
title: ajax
date: 2018-05-24 01:25:15
tags:
---
###  ajax
>  async javascript and xml
在ajax的异步不是我们理解的同步异步编程，而是泛指局部刷新，但是我们在以后的Ajax请求中尽可能使用异步获取数据（因为异步数据获取不会阻塞下面代码的执行）
客户端从服务器端获取数据
XML:可扩展标记语言，利用扩展有规则标记，来存储相关数据和内容。
好处是：清晰的展示出数据的结构
json:也很清晰的展示出数据的结构，并且访问数据的时候操作起来比XML更方便
现实项目中服务器返回给客户端数据不单纯的是数据，而是数据和需要展示的结构拼接好的结果，类似于我们自己做的字符串拼接，是服务端把数据和结构拼接好返回给我们，此时返回的数据格式一般是XML格式的字符串

ajax:客户端js中的方法，用来向服务器端发送请求，然后把服务器端返回的内容获取到，一般运行在客户端的浏览器中

**ajax的诞生是为了实现局部刷新**
`局部刷新 VS 全局刷新` 
> 在非完全前后端分离项目中，前端开发只需要完成页面的制作，并且把一些基础的人机交互效果使用js完成即可，页面中需要动态呈现内容的部分，都是交给后台开发工程师做数据绑定和基于服务器进行渲染的（服务器端渲染）
>  
> [优势]
> 1、动态展示的数据在页面的原代码中可以看见，有利于SEO优化推广（有利于搜索引擎的收录和抓取）
> 2、从服务器端获取的结果就已经是最后要呈现的结果了，不需要客户端做额外的事情，所以页面加载速度快（前提是服务器端处理的速度够快，能够处理过来），所以类似于京东、淘宝这些网站，首屏数据一般都是经由服务器端渲染的
>  
> [弊端]
> 1、如果页面中存在需要实时更新的数据，每一次想要展示最新的数据，页面都要重新的刷新一次，这样肯定不行
> 2、都交给服务器端做数据渲染，服务器端的压力太大，如果服务器处理不过来，页面呈现的速度更慢（所以京东淘宝这类网站，除了首屏是服务器端渲染的，其它屏一般都是客户端做数据渲染绑定）
> 3、这种模式不利于开发（开发效率低）

>**服务器端渲染的好处**
 1.有利于seo优化，有利于引擎收录，但是客户端做字符串拼接，呈现出来的内容在页面源代码是没有 的不利于seo
> 2.只要服务器端并发给力，页面加载速度与会比客户端渲染更快
> 很多大网站比如淘宝京东，首屏内容都是基于服务器端渲染的客户端获取XML数据后直接呈现，增加页面第一次打开速度而剩下屏中的内容都是基于Ajax获取数据，在客户端进行数据拼接渲染的



>- 基于Ajax向服务器发送请求获取数据，不管是json还是服务器渲染好的XML文档都是**前后端分离**的项目
A:不利于SEO优化（源代码中看不到动态添加的数据）
B：都可以实现“局部刷新”
例如京东，首屏数据是基于Ajax从服务器端获取的XML字符串（服务器端渲染）其他屏数据是从服务器获取json，客户端拼接字符串掺入到指定的区域中（客户端渲染）

>- 不基于Ajax，直接通过浏览器向服务器发送请求，服务器把需要呈现的内容返回，这种模式是**非前后端分离项目**
A:不利于SEO优化
B:只能实现全局刷新
C:请求页面的后缀名一般都不是HTML，而是.php/.jsp/.aspx/.asp...也有HTML，但是是基于node做后台实现服务器渲染的，注意原始地址可能被重新修改URL重写

>- 还有一些项目，首屏是不分离的，浏览器向服务器发送请求，服务器端直接把首屏内容返回，客户端h直接显示，但是其他屏都是基于AJAX获取的，这种叫做**前后端半分离**，例如淘宝


----------


>一：let xhr=new XMLHttpRequest;
 - 创建一个Ajax对象，ie6中不兼容的，使用的是new ActiveXobject来实现


----------


>二：xhr.open("get","json/data.json",false，[username],[userpass]);
- 发送前的基本信息配置：
1.get:从服务器获取数据，最常用，一般使用问号传参的方式，传递给服务器的内容存在`大小限制`，因为浏览器对于url有长度限制，还会出现`缓存`问题。可以在末尾加一个随机数解决。一般来说get不安全，而post相对安全一些
2.打开一个URL地址:向服务器端发送请求的API接口地址，
3.同步还是异步，true是异步；项目中都使用异步编程，防止阻塞后续代码执行。


----------


>三：xhr.onreadystatechange=function(){
if（xhr.readyState=====4&&xhr.status=====200）{
let val=xhr.responseText;l}}


>- 事件监听：一般监听的都是ready-state-change事件，基于这个时间可以获取服务器返回的响应头响应主体内容
给onreadystatechange绑定一个方法，监听状态改变，一改变就触发

> **xhr.readyState:**
0 unsent 当前概念的请求还没有发送
1 opened url 地址已经打开
2 headers —received响应头已经接受
3 loading 主要返回的内容正在服务器端进行准备处理
4 done 响应主题的内容已经成功返回到客户端


----------

>**xhr.status状态码**
>根据状态吗能够清楚的反映出当前交互的结果以及原因
200 ok 成功，只能证明服务器成功返回信息了，但是信息不一定是你业务需要的
301 永久转移/永久重定向 =》域名更改重新定向到新的域名
302 临时转移
 网站现在是基于https协议运作的，如果访问的是HTTP协议会基于307重定向到HTTPS协议上，一般用做服务器负载均衡。
 当一台服务器达到最大并发数的时候会把后续访问的用户临时转移到其他的服务器机组上处理。
 偶尔真实项目中会把所有的图片放到单独的服务器上、图片处理服务器这样减少主服务器的压力当用户向主服务器访问图片的时候，主服务器都把他转移到图片服务器上处理
307 临时重定向
304 not modified 设置缓存
对于不经常更新的资源文件例如../js/html/img等，服务器会结合客户端设置304缓存，第一次加载过这些资源就缓存到客户端了，下次再获取的时候是从缓存中获取；如果资源更新了，服务器端会通过最后修改时间来强制让客户端从服务器重新拉取；基于CTRL+F5强制刷新页面，304做的缓存就没有用了

>400   请求参数出现错误
401  无访问权限
404 客户端访问的地址不存在
413 和服务器交互的内容资源超过服务器最大限制


>500 未知的服务器错误
503 服务器超负载。


----------


**`AJAX中其它常用的属性和方法`**
> 面试题：AJAX中总共支持几个方法？
>  
> let xhr=new XMLHttpRequest();
> console.dir(xhr);
>  
> [属性]
> - readyState：存储的是当前AJAX的状态码
> - response / responseText / responseXML ：都是用来接收服务器返回的响应主体中的内容，只是根据服务器返回内容的格式不一样，我们使用不同的属性接收即可
>    +  responseText是最常用的，接收到的结果是字符串格式的（一般服务器返回的数据都是JSON格式字符串）
>    + responseXML偶尔会用到，如果服务器端返回的是XML文档数据，我们需要使用这个属性接收
> - status：记录了服务器端返回的HTTP状态码
> - statusText：对返回状态码的描述
> - timeout：设置当前AJAX请求的超时时间，假设我们设置时间为3000(MS)，从AJAX请求发送开始，3秒后响应主体内容还没有返回，浏览器会把当前AJAX请求任务强制断开
>  
> [方法]
> - abort()：强制中断AJAX请求
> - getAllResponseHeaders()：获取全部的响应头信息（获取的结果是一堆字符串文本）
> - getResponseHeader(key)：获取指定属性名的响应头信息，例如：xhr.getResponseHeader('date') 获取响应头中存储的服务器的时间
> - open()：打开一个URL地址
> - overrideMimeType()：重写数据的MIME类型
> - send()：发送AJAX请求（括号中书写的内容是客户端基于请求主体把信息传递给服务器）
> - setRequestHeader(key,value)：设置请求头信息（可以是设置的自定义请求头信息）
>  
> [事件]
> - onabort：当AJAX被中断请求触发这个事件
> - onreadystatechange：AJAX状态发生改变，会触发这个事件
> - ontimeout：当AJAX请求超时，会触发这个事件
> - ...
```javascript
let xhr = new XMLHttpRequest();
// xhr.setRequestHeader('aaa', 'xxx');//=>Uncaught DOMException: Failed to execute 'setRequestHeader' on 'XMLHttpRequest': The object's state must be OPENED. 设置请求头信息必须在OPEN之后和SEND之前
xhr.open('get', 'temp.xml?_=' + Math.random(), true);
// xhr.setRequestHeader('cookie', '珠峰培训');//=>Uncaught DOMException: Failed to execute 'setRequestHeader' on 'XMLHttpRequest': '珠峰培训' is not a valid HTTP header field value. 设置的请求头内容不是一个有效的值（请求头部的内容中不得出现中文汉字）
xhr.setRequestHeader('aaa', 'xxx');

//=>设置超时
xhr.timeout = 100000;
xhr.ontimeout = ()=> {
    console.log('当前请求已经超时');
    xhr.abort();
};

xhr.onreadystatechange = ()=> {
    let {readyState:state, status}=xhr;

    //=>说明请求数据成功了
    if (!/^(2|3)\d{2}$/.test(status)) return;

    //=>在状态为2的时候就可以获取响应头信息
    if (state === 2) {
        let headerAll = xhr.getAllResponseHeaders(),
            serverDate = xhr.getResponseHeader('date');//=>获取的服务器时间是格林尼治时间(相比于北京时间差了8小时)，通过new Date可以把这个时间转换为北京时间
        console.log(headerAll, new Date(serverDate));
        return;
    }

    //=>在状态为4的时候响应主体内容就已经回来了
    if (state === 4) {
        let valueText = xhr.responseText,//=>获取到的结果一般都是JSON字符串(可以使用JSON.PARSE把其转换为JSON对象)
            valueXML = xhr.responseXML;//=>获取到的结果是XML格式的数据(可以通过XML的一些常规操作获取存储的指定信息)  如果服务器返回的是XML文档,responseText获取的结果是字符串而responseXML获取的是标准XML文档
        console.log(valueText, valueXML);
    }
};
xhr.send('name=zxt&age=28&sex=man');
```
----------



> 四：xhr.send([请求主体内容])；
- 发送请求，参数是请求主体中传递服务器的内容；
从这步开始当前Ajax任务开始，如果Ajax是同步的后续代码不会执行，要等到Ajax状态成功后再执行，反之异步不会


----------


> 关于HTTP请求方式的一点学习
所有的请求都可以给服务器端传递内容，也都可以从服务器端获取内容
get:从服务器获取数据，最常用，一般使用问号传参的方式，传递给服务器的内容存在`大小限制`，因为浏览器对于url有长度限制，还会出现`缓存`问题。可以在末尾加一个随机数解决。一般来说get不安全，而post相对安全一些
post:一般用于向服务器推送数据，一般使用请求主体的方式
put:一般用于，给服务器增加资源文件（上传图片）
delete:一般用于从服务器删除资源文件
head：一般用于获取服务器的响应头信息。
options:一般使用它向服务器发送一个探测性请求，如果服务器端返回的信息了，说明当前客户端和服务器建立了连接，我们可以继续执行其他请求了（trace是干这件事的，但是axios这个Ajax类库再给予cross domain进行跨域请求的时候，就是先发送options请求进行探测尝试，如果能连通服务器，才会继续发送其他请求的）
trace:回显服务器收到的请求，主要用于测试或诊断
connect:HTTP/1.1协议中预留给能够连接改为管道方式的


----------


>get  vs  post
传递给服务器信息的方式不一样
get是基于URL地址问号传参的方式把信息传递给服务器，post是基于请求主体把信息传递给服务器.
get不安全，post相对安全
post是基于请求主体传递，相对来说不好被劫持，所以登陆注册等涉及安全性的交互操作，我们都应该用post请求
get 会产生不可控制的缓存，post不会
不可控：不是想要就要的，这是浏览器自主记忆的缓存，我们无法基于JS控制，真实项目中我们都会把这个缓存干掉
get请求产生缓存的原因;连续多次向相同的地址并且传递的参数信息也是相同的发送请求浏览器会把之前或获取的数据从还从中拿到返回，导致无法获取服务器最新的数据（post不会）
解决方案：
```
 xhr.open('get',`https://www.easy-mock.com/mock/5b0412beda8a195fb0978627/temp/list ?id=1000&lx=2000&_=${Math.random()}`);//保证每次请求的地址不完全一致，在每一次请求的末尾追加一个随机数即可，(使用_作为属性名就是不想和其他的属性名冲突)
```
####  实战案例：倒计时抢购
```javascript
~function () {
    let box = document.getElementById('box'),
        serverTime = null;

    let fn = ()=> {
        //=>1、计算当前时间和目标时间的差值
        //=>new Date()：获取的是客户端本机时间(会受到客户端自己调整时间的影响),重要的时间参考不能基于这个完成,不管是哪一个客户端都需要基于相同的服务器时间计算
        //=>每间隔1S中,我们需要把第一次获取的服务器时间进行累加
        serverTime = serverTime + 1000;
        let tarTime = new Date('2017/12/14 13:12:20').getTime(),
            spanTime = tarTime - serverTime;

        //=>2、计算差值中包含多少时分秒
        if (spanTime < 0) {
            //=>已经错过了抢购的时间(已经开抢了)
            box.innerHTML = '开抢啦！！';
            clearInterval(autoTimer);
            return;
        }
        let hours = Math.floor(spanTime / (1000 * 60 * 60));
        spanTime -= hours * 3600000;
        let minus = Math.floor(spanTime / (1000 * 60));
        spanTime -= minus * 60000;
        let seconds = Math.floor(spanTime / 1000);
        hours < 10 ? hours = '0' + hours : null;
        minus < 10 ? minus = '0' + minus : null;
        seconds < 10 ? seconds = '0' + seconds : null;
        box.innerHTML = `距离开抢还剩下 ${hours}:${minus}:${seconds}`;
    };
    let autoTimer = setInterval(fn, 1000);

    //=>从服务器端获取服务器时间
    let getServerTime = ()=> {
        let xhr = new XMLHttpRequest();
        xhr.onreadystatechange = ()=> {
            //console.log(xhr.readyState);//=>HEAD请求方式,状态码中没有3(不需要等待响应主体内容)
            if (!/^(2|3)\d{2}$/.test(xhr.status)) return;
            if (xhr.readyState === 2) {
                serverTime = new Date(xhr.getResponseHeader('date')).getTime();
                fn();
            }
        };
        xhr.open('head', 'temp.xml', true);
        xhr.send(null);

        /*
         * 获取服务器时间总会出现时间差的问题：服务器端把时间记录好，到客户端获取到事件有延迟差（服务器返回的时候记录的是10:00，我们客户端获取的时候已经是10:01，但是我们获取的结果依然是10:00，这样就有1分钟时间差）
         *
         * [尽可能的减少时间差，是我们优化的全部目的]
         * 
         * 1、服务器返回的时间在响应头信息中就有，我们只需要获取响应头信息即可，没必要获取响应主体内容，所以请求方式使用 HEAD 即可
         * 2、必须使用异步编程：同步编程我们无法在状态为2或者3的时候做一些处理，而我们获取响应头信息，在状态为2的时候就可以获取了，所以需要使用异步
         * 3、在状态为2的时候就把服务器时间获取到
         * ...
         */
    };
    getServerTime();
}();
```
#### JS中常用的编码解码方法
> 正常的编码解码（非加密）
> 1、escape / unescape：主要就是把中文汉字进行编码和解码的（一般只有JS语言支持：也经常应用于前端页面通信时候的中文汉字编码）

> 2、encodeURI / decodeURI：基本上所有的编程语言都支持

> 3、encodeURIComponent / decodeURIComponent：和第二种方式非常的类似，区别在于



> 也可以通过加密的方法进行编码解码
> 1、可逆转加密（一般都是团队自己玩的规则）
> 2、不可逆转加密（一般都是基于MD5加密完成的，可能会把MD5加密后的结果二次加密）
> 
> ----
> 需求：我们URL问号传递参数的时候，我们传递的参数值还是一个URL或者包含很多特殊的字符，此时为了不影响主要的URL，我们需要把传递的参数值进行编码。使用encodeURI不能编码一些特殊字符，所以只能使用encodeURLComponent处理
```javascript
let str = 'http://www.baidu.com/?',
	obj = {
		name:'珠峰培训',
		age:9,
		url:'http://www.zhufengpeixun.cn/?lx=1'
	};
//=>把OBJ中的每一项属性名和属性值拼接到URL的末尾（问号传参方式）
for(let key in obj){
	str+=`${key}=${encodeURIComponent(obj[key])}&`;
	//=>不能使用encodeURI必须使用encodeURIComponent，原因是encodeURI不能编码特殊的字符
}
console.log(str.replace(/&$/g,''));

//=>后期获取URL问号参数的时候，我们把获取的值在依次的解码即可
String.prototype.myQueryUrlParameter=function myQueryUrlParameter(){
	let reg=/[?&]([^?&=]+)(?:=([^?&=]*))?/g,
	obj={};
	this.replace(reg,(...arg)=>{
	    let [,key,value]=arg; 		
	    obj[key]=decodeURIComponent(value);//=>此处获取的时候可以进行解码	
	});
	return obj;
}
```

####  AJAX中的同步和异步
> AJAX这个任务：发送请求接收到响应主体内容（完成一个完整的HTTP事务）
> xhr.send()：任务开始
> xhr.readyState===4：任务结束
```javascript
let xhr = new XMLHttpRequest();
xhr.open('get', 'temp.json', false);
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
xhr.send();
//=>只输出一次结果是4
```



```javascript
let xhr = new XMLHttpRequest();
xhr.open('get', 'temp.json', false);
xhr.send();//=>[同步]开始发送AJAX请求,开启AJAX任务,在任务没有完成之前,什么事情都做不了(下面绑定事件也做不了) => LOADING => 当readyState===4的时候AJAX任务完成，开始执行下面的操作
//=>readyState===4
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
//=>绑定方法之前状态已经为4了,此时AJAX的状态不会在改变成其它值了,所以事件永远不会被触发,一次都没执行方法（使用AJAX同步编程，不要把SEND放在事件监听前，这样我们无法在绑定的方法中获取到响应主体的内容）
```

```javascript
let xhr = new XMLHttpRequest();
xhr.open('get', 'temp.json');
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
xhr.send();
//=>输出3次，结果分别是 2 3 4
```



```javascript
let xhr = new XMLHttpRequest();
xhr.open('get', 'temp.json');
xhr.send();
//=>xhr.readyState===1
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
//=>2 3 4
```

```javascript
let xhr = new XMLHttpRequest();
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
xhr.open('get', 'temp.json');
xhr.send();
//->1 2 3 4
```

```javascript
let xhr = new XMLHttpRequest();
//=>xhr.readyState===0
xhr.onreadystatechange = ()=> {
    console.log(xhr.readyState);
};
xhr.open('get', 'temp.json', false);
//=>xhr.readyState===1 AJAX特殊处理的一件事：执行OPEN状态变为1,会主动把之前监听的方法执行一次，然后再去执行SEND
xhr.send();
//=>xhr.readyState===4 AJAX任务结束,主任务队列完成
//=>1 4
```




###  AJAX类库的封装
> JQ中的AJAX使用及每一个配置的作用（包含里面的一些细节知识）
```javascript
$.ajax({
	url:'xxx.txt',//=>请求API地址
	method:'get',//=>请求方式GET/POST...在老版本JQ中使用的是type，使用type和method实现的是相同的效果
	dataType:'json',//=>dataType只是我们预设获取结果的类型，不会影响服务器的返回（服务器端一般给我们返回的都是JSON格式字符串）,如果我们预设的是json，那么类库中将把服务器返回的字符串转换为json对象，如果我们预设的是text(默认值)，我们把服务器获取的结果直接拿过来操作即可，我们预设的值还可以是xml等
	cache:false,//=>设置是否清除缓存，只对GET系列请求有作用，默认是TRUE不清缓存，手动设置为FALSE，JQ类库会在请求URL的末尾追加一个随机数来清除缓存
	data:null,//=>我们通过DATA可以把一些信息传递给服务器；GET系列请求会把DATA中的内容拼接在URL的末尾通过问号传参的方式传递给服务器，POST系列请求会把内容放在请求主体中传递给服务器；DATA的值可以设置为两种格式：字符串、对象，如果是字符串，设置的值是什么传递给服务器的就是什么，如果设置的是对象，JQ会把对象变为 xxx=xxx&xxx=xxx 这样的字符串传递给服务器
	async:true,//=>设置同步或者异步，默认是TRUE代表异步，FALSE是同步
	success:function(result){
		//=>当AJAX请求成功 (readyState===4 & status是以2或者3开头的)
		//=>请求成功后JQ会把传递的回调函数执行，并且把获取的结果当做实参传递给回调函数	（result就是我们从服务器端获取的结果）
	},
	error:function(msg){},//=>请求错误触发回调函数
	complate:function(){},//=>不管请求是错误的还是正确的都会触发回调函数（它是完成的意思）
	...
});
```
> 封装属于自己的AJAX类库
> 
> [支持的参数]
> - url
> - method / type
> - data
> - dataType
> - async
> - cache
> - success
> - ...
```javascript
~function () {
    class ajaxClass {
        //=>SEND AJAX
        init() {
            //=>THIS:EXAMPLE
            let xhr = new XMLHttpRequest();
            xhr.onreadystatechange = ()=> {
                if (!/^[23]\d{2}$/.test(xhr.status)) return;
                if (xhr.readyState === 4) {
                    let result = xhr.responseText;
                    //=>DATA-TYPE
                    try {
                        switch (this.dataType.toUpperCase()) {
                            case 'TEXT':
                            case 'HTML':
                                break;
                            case 'JSON':
                                result = JSON.parse(result);
                                break;
                            case 'XML':
                                result = xhr.responseXML;
                        }
                    } catch (e) {
                        
                    }
                    this.success(result);
                }
            };

            //=>DATA
            if (this.data !== null) {
                this.formatData();

                if (this.isGET) {
                    this.url += this.querySymbol() + this.data;
                    this.data = null;
                }
            }

            //=>CACHE
            this.isGET ? this.cacheFn() : null;

            xhr.open(this.method, this.url, this.async);
            xhr.send(this.data);
        }

        //=>CONVERT THE PASSED OBJECT DATA TO STRING DATA
        formatData() {
            //=>THIS:EXAMPLE
            if (Object.prototype.toString.call(this.data) === '[object Object]') {
                let obj = this.data,
                    str = ``;
                for (let key in obj) {
                    if (obj.hasOwnProperty(key)) {
                        str += `${key}=${obj[key]}&`;
                    }
                }
                str = str.replace(/&$/g, '');
                this.data = str;
            }
        }

        cacheFn() {
            //=>THIS:EXAMPLE
            !this.cache ? this.url += `${this.querySymbol()}_=${Math.random()}` : null;
        }

        querySymbol() {
            //=>THIS:EXAMPLE
            return this.url.indexOf('?') > -1 ? '&' : '?';
        }
    }

    //=>INIT PARAMETERS
    window.ajax = function ({
        url = null,
        method = 'GET',
        type = null,
        data = null,
        dataType = 'JSON',
        cache = true,
        async = true,
        success = null
    }={}) {
        let _this = new ajaxClass();
        ['url', 'method', 'data', 'dataType', 'cache', 'async', 'success'].forEach((item)=> {
            if (item === 'method') {
                _this.method = type === null ? method : type;
                return;
            }
            if (item === 'success') {
                _this.success = typeof success === 'function' ? success : new Function();
                return;
            }
            _this[item] = eval(item);
        });
        _this.isGET = /^(GET|DELETE|HEAD)$/i.test(_this.method);
        _this.init();
        return _this;
    };
}();
```
#### promise版Ajax
```javascript
~(function anonymous(window) {
    //=>设置默认的参数配置项
    let _default = {
        method: 'GET',
        url: '',
        baseURL: '',
        headers: {},
        dataType: 'JSON',
        data: null,//=>POST系列请求基于请求主体传递给服务器的内容
        params: null,//=>GET系列请求基于问号传参传递给服务器的内容
        cache: true
    };

    //=>基于PROMISE设计模式管理AJAX请求
    let ajaxPromise = function ajaxPromise(options) {
        //=>OPTIONS中融合了:默认配置信息、用户基于DEFAULTS修改的信息、用户执行GET/POST方法时候传递的配置信息，越靠后的优先级越高
        let {url, baseURL, method, data, dataType, headers, cache, params} = options;

        //=>把传递的参数进一步进行处理
        if (/^(GET|DELETE|HEAD|OPTIONS)$/i.test(method)) {
            //=>GET系列
            if (params) {
                url += `${ajaxPromise.check(url)}${ajaxPromise.formatData(params)}`;
            }
            if (cache === false) {
                url += `${ajaxPromise.check(url)}_=${+(new Date())}`;
            }
            data = null;//=>GET系列请求主体就是什么都不放
        } else {
            //=>POST系列
            if (data) {
                data = ajaxPromise.formatData(data);
            }
        }

        //=>基于PROMISE发送AJAX
        return new Promise((resolve, reject) => {
            let xhr = new XMLHttpRequest;
            xhr.open(method, `${baseURL}${url}`);
            //=>如果HEADERS存在,我们需要设置请求头
            if (headers !== null && typeof headers === 'object') {
                for (let attr in headers) {
                    if (headers.hasOwnProperty(attr)) {
                        let val = headers[attr];
                        if (/[\u4e00-\u9fa5]/.test(val)) {
                            //=>VAL中包含中文:我们把它进行编码
                            //encodeURIComponent/decodeURIComponent
                            val = encodeURIComponent(val);
                        }
                        xhr.setRequestHeader(attr, val);
                    }
                }
            }
            xhr.onreadystatechange = () => {
                if (xhr.readyState === 4) {
                    if (/^(2|3)\d{2}$/.test(xhr.status)) {
                        let result = xhr.responseText;
                        dataType = dataType.toUpperCase();
                        dataType === 'JSON' ? result = JSON.parse(result) : (dataType === 'XML' ? result = xhr.responseXML : null);
                        resolve(result);
                        return;
                    }
                    reject(xhr.statusText);
                }
            };
            xhr.send(data);
        });
    };

    //=>把默认配置暴露出去,后期用户在使用的时候可以自己设置一些基础的默认值(发送AJAX请求的时候按照用户配置的信息进行处理)
    ajaxPromise.defaults = _default;

    //=>把对象转换为URLENCODED格式的字符串
    ajaxPromise.formatData = function formatData(obj) {
        let str = ``;
        for (let attr in obj) {
            if (obj.hasOwnProperty(attr)) {
                str += `${attr}=${obj[attr]}&`;
            }
        }
        return str.substring(0, str.length - 1);
    };
    ajaxPromise.check = function check(url) {
        return url.indexOf('?') > -1 ? '&' : '?';
    };

    //=>GET
    ['get', 'delete', 'head', 'options'].forEach(item => {
        ajaxPromise[item] = function anonymous(url, options = {}) {
            options = {
                ..._default,//=>默认值或者基于defaults修改的值
                ...options,//=>用户调取方法传递的配置项
                url: url,//=>请求的URL地址(第一个参数:默认配置项和传递的配置项中都不会出现URL，只能这样获取)
                method: item.toUpperCase()//=>以后执行肯定是ajaxPromise.head执行，不会设置METHODS这个配置项，我们自己需要配置才可以
            };
            return ajaxPromise(options);
        };
    });

    //=>POST
    ['post', 'put', 'patch'].forEach(item => {
        ajaxPromise[item] = function anonymous(url, data = {}, options = {}) {
            options = {
                ..._default,
                ...options,
                url: url,
                method: item.toUpperCase(),
                data: data
            };
            return ajaxPromise(options);
        };
    });

    window.ajaxPromise = ajaxPromise;
})(window);


```