---
title: H5、css3常用标签
date: 2018-05-22 01:09:55
tags:
---
###   HTML5、CSS3

> HTML5新增标签
>|标签|描述|
|--|--|
|header|头部|
|footer|尾部|
|nav|导航|
|section|区分大模块|
|aside|侧边栏|
|article|文章|
|figure|配图|
|figcaption|配图说明|
|video|视频|
|audio|音频|<
|main|主体|
>| video 视频| audio音频|
|--|--|
| src="" 视频路径| autoplay 自动播放|
|controls 是否显示控件|loop 循环播放|<
|--|--|
>|表单|功能|
|--|--|
|input type="number"|数字|
|input type="tel"|电话号码输入框|
|input type="url"|输入URL地址|
|input type="range"|特定范围内的数值选择器（通过拖动滚动条改变一定范围内的数字）|
|input type="search"|搜索输入框|
|input type="email"|邮箱|
|input type="color"|颜色选取器|
|input type="datetime"|显示完整日期和时间UTC标准时间|
|input type="datetime"|显示完整日期和时间|
|input type="time"|显示时间|
|input type="month"|显示月|
|input type="week"|显示周|
|input type="file"|上传文件|<
|input type="text"|"placeholder"输入框占位符，常用作输入提示，在光标聚焦时，占位符自动消失|
|input type="text"|"autocomplete"是否保存用户输入值，默认on，关闭提示选择off|
|input type="text"|"autofocus"自动聚焦|
|input type="text"|"required":此项必填不能为空|
|input type="text"|"Pattern":正则验证pattern="\d{1,5}"|
from属性只要加上from属性，表单元素可以放到页面的任意位置。
formnovalidate和novalidatae他俩都表示不需要验证表单直接提交，novalidate用于form标签；formnovalidate用于submit类型的提交按钮。
表单验证
- validity对象，通过下面的valid可以查看验证是否通过
- oTex.addEvectListener("invalid",fn1,false);
- valid:验证不通过时返回false
- valueMissing:输入值为空时
- typeMismatch：控件值与预期类型不匹配
- patternMismatch:输入值不满足pattern正则
- customError：不符合自定义验证
- setCustomValidity();自定义验证



####  input类型

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-- input表单元素的类型
text  文本类型
password  密码类型
button 按钮类型
submit 提交按钮类型
reset 重置按钮类型
file 文件类型
radio 单选框类型
checkbox 复选框类型
-->
<!-- 文本类型 -->
<input type="text">

<!--密码类型-->
<input type="password">

<!-- 按钮类型 -->
<input type="button" value="百度一下">

<!-- 提交按钮 -->
<input type="submit" value="登录">

<!-- 重置按钮-->
<input type="reset">

<!--文件类型-->
<input type="file">

<!--多选框类型-->
<label><input type="checkbox"> 自动登录</label>
<label><input type="checkbox"> 敲代码</label>
<label><input type="checkbox"> 滑板</label>
<label><input type="checkbox"> 健身</label>

<!--单选框-->
<label><input type="radio" name="sex"> 男</label>
<label><input type="radio" name="sex"> 女</label>
<label><input type="radio" name="sex"> 性别不详</label>

<input type="image">
<input type="hidden">
</body>
</html>

```
以上为常用HTML5标签
在之前的HTML页面中，大家基本上都是用了Div+CSS的布局方式。而搜索引擎去抓取页面的内容的时候，它只能猜测你的某个Div内的内容是文章内容容器，或者是导航模块的容器，或者是作者介绍的容器等等。也就是说整个HTML文档结构定义不清晰，HTML5中为了解决这个问题，专门添加了：页眉、页脚、导航、文章内容等跟结构相关的结构元素标签。

1.header
标签定义文档的页眉,通常是一些引导和导航信息，它不局限写在网页头部，也可以写在网页内容里面。通常`<header>`标签至少包含（但不局限于）一个标题标记`(<h1>~<h6>)`,还可以包括`<hgroup>`标签，还可以包括表格内容、标识、搜索表单、`<nav>`导航等；
```
<header>
    <hgroup>
        <h1>网站标题</h1>
        <h2>网站副标题</h2>
    </hgroup>
</header>
```
> 2.nav
nav标签代表页面的一个部分,是一个可以作为页面导航的链接组，其中的导航元素链接到其他页面或者当前页面的其他部分，使html代码在语义化方面更加精确，同时对于屏幕阅读器等设备的支持也更好；
```
<nav>
    <ul>
        <li>珠峰培训首页</li>
        <li>node培训课程</li>
        <li>html5培训课程</li>
        <li>珠峰论坛</li>
    </ul>
</nav>
```
> 3.section
    section标签，定义文档中的节。比如章节、页眉、页脚或文档中的其他部分。一般用于成节的内容，会在文档流中开始一个新的节。它用来表现普通的文档内容或应用区块，通常由内容及其标题组成。但section元素标签并非一个普通的容器元素，它表示一段专题性的内容，一般会带有标题。

  >  当我们描述一件具体的事物的时候，通常鼓励使用artice来代替section;当我们使用section时，仍然可以使用h1来作为标题，而不用担心它所处的位置，以及其它地方是否用到;当一个容器需要被直接定义样式或通过脚本定义行为时，推荐使用div元素而非section;
```
<section>
    <h1>section是什么？</h1>
    <p>是一个独立的章节</p>
    <article>
       <h2>关于section</h1>
        <p>section的介绍</p>
    </article>
 </section>
```
> 4.article
article是一个特殊的section标签，它比section具有更明确的语义，它代表一个独立的，完整的相关内容块，可独立于页面其他内容使用。例如一篇完整的论坛帖子，一篇博客文章，一个用户评论等等。一般来说，article会有标题部分(通常包含在header内),有时也会包含footer。article可以嵌套，内层的article对外层的article标签有隶属关系。例如，一篇博客文章，可以用article显示，然后一些评论可以以article的形式嵌入其中;
```
<article>
    <header>
        <hgroup>
            <h1>这是一篇介绍HTML 5结构标签的文章</h1>
            <h2>HTML 5的革新</h2>
       </hgroup>
       <time datetime="2016-11-18">2016.11.18</time>
  </header>
  <p>文章内容详情</p>
 </article>
```
> 5.aside
aside标签用来装载非正文的内容，被视为页面里面一个单独的部分。它包含的内容与页面的主要内容是分开的，可以被删除，而不会影响网页的内容、章节或是页面所要传达的信息。例如广告，成组的链接，侧边栏等等。
```
<aside>
     <h1>简介</h1>
     <p>我是简介内容，嘿嘿</p>
 </aside>
```
> 6.footer
footer标签定义section或document的页脚，包含了与页面、文章或是内容有关的信息，比如说文章的作者或者日期。作为页面的页脚时，一般包含了版权、相关文件和链接。它和header标签使用基本一样，可以在一个页面中多次使用，如果在一个区段的后面加入footer,那么它就相当于该区段的页脚了。
```
<footer>
   <span>copyRight@珠峰培训</span>
</footer>
```
> 7.hgroup
hgroup标签是对网页或区段section的标题元素(h1~h6)进行组合。例如,在一区段中你有连续的h系列的标签元素，则可以用hgroup将他们括起来。
```
<hgroup>
    <h1>主标题</h1>
    <h2>副标题</h2>
</hgroup>
```
> 8.figure
用作文档中插图的图像，带有一个标题
```
<figure>
      <figcaption>标题</figcaption>
      <img src="img.jpg" alt="figure标签" title="figure标签" />
 </figure>
```
> 9.figcaption
标签定义figure元素的标题(caption)。"figcaption"元素应该被置于"figure"元素的第一个或最后一个子元素的位置。
```
<figure>
      <img src="img.jpg" alt="figure标签" title="figure标签" />
      <figcaption>标题</figcaption>
 </figure>
```
> 10.datalist
datalist标签定义选型列表。请与input元素配合使用该元素，来定义input可能的值。datalist及其选项不会被显示出来，它仅仅是合法的输入值列表。请使用input元素的list属性来 绑定datalist。所有主流浏览器都支持此标签，除了Internet Explorer和Safari。
```
<input id="myCar" list="cars" />
<datalist id="cars">
  <option value="BMW">
  <option value="Ford">
  <option value="Volvo">
</datalist>
```
> 11.audio
定义声音，比如音乐或其它音频流：其相关的属性
autoplay 如果出现该属性，则音频在就绪后马上播放;
controls 如果出现该属性，则向用户显示控件，比如播放按钮;
loop 如果出现该属性，则每当音频结束时重新开始播放；
muted 规定视频输出应该被静音；
preload 如果出现该属性，则音频在页面加载时进行加载，并预备播放,如果出现"autoplay"则忽略该属性；
src 要播放的音频的url
```

<audio id="audio" preload="auto" autoplay="autoplay" loop="loop" src="http://song4u.u.qiniudn.com/blog/audio/gt.mp3">
</audio>
```
> 12.video
定义视频，比如电影片段或其它视频流：其相关的属性
autoplay 如果出现该属性，则视频在就绪后马上播放;
controls 如果出现该属性，则向用户显示控件，比如播放按钮;
height 设置视频播放器的高度;
loop 如果出现该属性，则当媒介文件完成播放后再次开始播放；
preload 如果出现该属性，则视频在页面加载时进行加载，并预备播放,如果出现"autoplay"则忽略该属性；
src 要播放的音频的url；
width 设置视频播放器的宽度；
```
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">

    您的浏览器不支持 video 标签。
</video>
```
13.canvas
canvas标签定义图形，比如图表和其他图像，canvas标签只是图形容器，您必须使用脚本来绘制图形;
```
<canvas id="myCanvas"></canvas>
<script type="text/javascript">

var canvas=document.getElementById('myCanvas');
var ctx=canvas.getContext('2d');
ctx.fillStyle='#FF0000';
ctx.fillRect(0,0,80,100);
</script>
```
总结：
1、新增加一些构建页面语义化的结构标签 ，对原有 标签进行了修改
```
header、nav、section、footer、article、aside、figure、figcaption、hgroup…
(在IE6~8浏览器中不识别这些新增加的标签,导致布局结构混乱)在页面中引入```
<!–[if lt IE 9]>

<![endif]–>
```

2、给我们的INPUT表单元素增加了很多新的类型(不兼容)
```javascript
原有:text、password、radio、checkbox、button、submit、reset、file…
新增:search、url、email、tel、number、date、time、color、range…
作用:
1)根据TYPE的类型不一样,会调取出最符合用户输入的物理键盘;
2)传统的表单验证:当某个行为触发的时候,我们获取用户输入的内容和自己编写的正则进行验证从而判断用户输入的是否符合规则;
3) HTML5中提供了CSS3/JS的新验证方式,不需要自己写正则,浏览器自己就已经实现了验证,我们只需要控制成功/不成功的样式或者其他操作即可
```

3、新增加了音视频处理AUDIO、VIDEO

4、新增加CANVAS绘图
```javascript
http://www.hcharts.cn/(Highcharts)
http://echarts.baidu.com/(echarts)
D3.js

```
5、新增加一些新的有助于开发的API:
本地存储localStorage/sessionStorge、
地理位置navigator.geolocation.getCurrentPosition、调取手机内部的GPS定位系统获取当前手机所在地的经纬度以及精准度
还提供了一些API，让我们可以通过浏览器调取手机内部的软件或者硬件（但是性能都不咋高，而且兼容性不是特别好）
websocket：socket.io、客户端和服务端新的传输方式（及时通讯IM系统基本上都是基于它完成的）
webworks…离线缓存
####   CSS3
ID
target

> A  .B{}   后代
A.B{}    子代
A>B{}   具备A也具备B
A+B{}   下一个弟弟
A~B{}   兄弟
`:nth-chld`某个元素下任意类型的子元素
`:nth-of-type`某个元素下的同一类型中的第几个子元素
`否定选择器`
`:not()`
`属性选择器`
E[attr=val]
E[attr|=val]只能等于var或只能以val-开头
E[attr*=val]包含val字符串
E[attr~=val]属性值有多个，其中有一个时val
E[attr^=val]以val开头
E[attr$=val]以val结尾
`目标伪类选择器`
`:target`用来匹配url指向的目标元素
存在url指向该匹配元素时样式效果才会生效
伪元素
:first-line匹配第一行文本
;first-letter匹配第一首字符
:before和after DOM元素前后插入额外的内容
`圆角`
`border-radius`:左上 右上 右下 左下；
`渐变`
`linear-gradient`([<起点>||<角度>,]?<点>,<点>...)
只能用在背景上
颜色是沿着一条直线轴变化
参数
-起点：从什么方向开始渐变》left、top、left top
-角度：从什么角度开始渐变》xxx deg的形式
-点：渐变点的颜色和位置》red50%,位置可选
重复现行渐变


`径向渐变`
`radial-gradient`([[<shape>||<size>][at <position>]?,|at<position>,]?<color-stop>[,<color-stop>]+);
从“一个点”向多方向颜色渐变
shape形状：ellipse、circle或设置水平半径，垂直半径
size：渐变的大小，即渐变到哪里停止，有如关键词：
closest-side：最近边；farthest-side:最远边；
closest-corner:最近角；farthest-corner：最远角（默认值）
position;关键词|数值|变化
重复的径向渐变


----------
`背景`
background -color/-image/-position/-repeat/-attachment
`background-origin`
padding-box从padding区域显示
border-box从border区域显示
contert-box从content区域显示
`background-clip`
padding-box从padding区域向外裁剪
border-box从border区域往外裁剪
content-box从content区域往外裁剪
`text文本裁剪`
`background-size`
100px 100px:宽高具体值
100% 100%宽高百分比
cover以合适的比例图片进行缩放不会变形，用来铺满整个容器
contain原始比例收缩，显示完整但不一定铺满（一边碰到容器的边缘，则停止覆盖，导致部分区域是没有背景图的）
cover按原始比例收缩，可能显示不完整但铺满整个容器
`background-attachment`
背景图片是滚动的还是固定的fixed(固定的)默认是滚动的
`box-shadow`:h水平方向偏移，v垂直方向偏移，blur模糊半径，spread扩展半径，color颜色，inset奖赏这个表示内阴影默认是外阴影。
`text-shadow`:x y blur color
x轴偏移 y轴偏移 模糊度 颜色
多层阴影制作的文字立体效果设置多种颜色中间以逗号隔开
`text-stroke`：2px blue
通过设定1px的透明边框，可以让文字变得平滑
颜色设定透明能创建镂空字体
mask-image遮罩
mask-position
mask-repeat
transform2D变换
box-sizing:border-box/padding-box/content-box(默认值)改变的就是我们在css中设置的width、height到底代表啥，border-box让其代表整个盒子的宽高当我们去修改padding或者border盒子大小不变只会让内容缩放
columns:多列布局
flex：弹性盒子模型，布局
perspective：视距 实现3D必用属性
@media：媒体查询 实现响应式布局的一种方案
@font-face：导入字体图标
transition
animation

----------
### CSS样式表

|元素|描述|
|--|--|
|style|写样式|
|link|引入标签|
|list-style：none|去除ul，ol，dl默认样式|
|text-decoration: none;|去除a的下划线|
|font-weight: normal;|去除字体加粗，斜体|
|color: #ccc;|字体颜色|
|background-color:#faa770;|背景颜色|
|width: 100px;|盒子宽度|
|height :100px;|盒子高度|
|border-radius: 20px;|盒子圆角|
|line-height:100px;|文本行高|
|font-size : 16px ;|字体大小|
|font-weight: bold;|字体加粗|
|font-style: italic;|字体倾斜|
|letter-spacing: 10px;|字体间距|
|text-indent: 2em;|段落首行缩进|
|cursor:pointer|鼠标经过加小手|
|z-index:1;|改变重叠盒子层级关系|
|border-top:1px solid red;|上边框|
|border-right:1px solid red;|右边框|
|border-bottom:1px solid red;|下边框|
|border-left:1px solid red;|左边框|
|border-width:10px; | 边框的宽度|
|border-color:red; |边框的颜色|
|border-style:solid(实线);dashed（虚线）；| 边框的样式|
|border:10px solid #fff;|边框宽度 样式 颜色缩写|
|padding:1px 2px 3px 4px;|盒子内边距 上 右  下 左|
|margin:1px 2px 3px 4px;|盒子外边距 上 右  下 左|
|position: relative;|相对定位|
|position：absolute；|绝对定位|
|position: fixed;|固定定位|
|float：left|左浮动|
|float：right|右浮动|
|display：block|转为块元素|
|display：inline|转为行内元素|
|display:inline-block|转为行内块元素|
|display：none|让元素隐藏|
|overflow: hidden;|溢出盒子高度隐藏|
|overflow: scroll;|不管内容是否超出，都会出现滚动条|
|overflow: auto;|系统判断超出则出现滚动条不超出则不出现|
|white-space: nowrap;|让文本强制换行|
|text-overflow:ellipsis;|让超出的文本以三个小点的方式出现|
|hover |鼠标经过时的状态|
|active| 鼠标点击时的状态|
|visited| 鼠标点击后的状态|
|text-align:  right ; left ；|文字水平居右，左|
|text-align: center;|文字水平居中|
|line-height: 50px;|文本垂直居中|
|vertical-align：top|平级元素顶部对齐|
|vertical-align：middle；|平级元素中部对齐|
|vertical-align：bottom;|平级元素底部对齐|
|margin:0 auto;|盒子，版心，位置居中|
|box-shadow: .02rem .02rem .02rem .02rem rgba(178,178,178,.75),-.02rem .02rem .02rem .02rem rgba(178,178,178,.75);|盒子阴影|
|text-shadow： .02rem .02rem .02rem .02rem rgba(178,178,178,.75);|文字阴影|
|link rel="icon" href="img/favicon.ico" type="image/x-icon|引入图标(页面标题的前面--页卡)|
|给body或者父级元素设置font-size:0;|清除间隙问题|
|opacity:0.5;|设置透明度|
|filter:alpha(opacity=50)|设置透明度 兼容ie低版本8以下浏览器|
|background: url("图片路径") no-repeat（不平铺）;|背景图片|
|background-position: center center；|改变背景图片的位置、水平垂直居中|
| background-size:100% 100%;|改变背景图片的大小|



> **background: red url("pic_02.png") no-repeat center center;-----这种写法格式是在项目中最常用**
 **background:背景颜色  背景图片的路径  背景图片是否平铺   改变背景图片的位置**>



> **实现隔行变色**<
-**单独获取容器中的某一个子元素** ——|||||||||||——  **EVEN : 偶数 \ ODD : 奇数**-
```
     * nth-child(n):当前容器所有子元素中的第N个
         *    .box li:nth-child(1)：BOX容器所有子元素中的第一个并且标签名是LI的
     * nth-of-type(n):先给当前容器按照某一个标签名进行分组,获取分组中的第N个
         *    .box li:nth-of-type(1)：先获取BOX中所有的LI，在获取LI中的第一个
```

**实心小三角**
```javascript
<style>
        div{
            border-color:  transparent（边框透明）  transparent   transparent   #0d0d0d ;
            border-style: solid;
            border-width: 40px;  }
    </style>
    <div></div>
```

|色值|描述|
|--|--|
|英文单词|red,yellow,green,blue---工作中不用，在低版本浏览器下不兼容|
|16进制|#ff0000 #666767   简写：#f00  #fff(白色)/#000(黑色) ---常用|
|rgb|red红,green绿,blue蓝|
|rgba|red红,green绿,blue蓝,a透明度(值：0-1)---常用|
| 颜色值在工作中最常用的是 |16进制、rgba，|
| 白色rgb(255,255,255)|
| 黑色rgb(0,0,0)|

>|标签|描述|
|--|--|
|header|头部|
|footer|尾部|
|nav|导航|
|section|区分大模块|
|aside|侧边栏|
|article|文章|
|figure|配图|
|figcaption|配图说明|
|video|视频|
|audio|音频|<
|main|主体|
>| video 视频| audio音频|
|--|--|
| src="" 视频路径| autoplay 自动播放|
|controls 是否显示控件|loop 循环播放|<
|--|--|
>|表单|功能|
|--|--|
|input type="number"|数字|
|input type="email"|邮箱|
|input type="file"|上传文件|
|input type="search"|搜索框|<


|REM布局|最终版|
|--|--|
|参照iphone5/5s | 设计稿尺寸640 分辨率320*2  dpr:2.0|
|参照iphone5/5s| 分辨率320*2 html{ font-size:50px;}|
|参照iphone6/6s| 分辨375*2 html{font-size:58.59375px;}|
|参照iphone6Plus| 分辨率：414*3 html{font-size:64.6875px;}|
|分辨率：640 | html{font-size:100px;}|
|--|--|
| 照iphone6/6s | 设计稿尺寸750 分辨率375*2 dpr:2.0 |
|--|--|
|参照物iphone6/6s |分辨率：375*2  html{font-size:50px;}|
|iphone5/5s |分辨率：320*2 dpr:2.0 html{font-size:42.66px;}|
|iphone6Plus |分辨率：414*3  dpr:3.0 html{font-size:55.2px;}|
||分辨率：640    html{font-size:85.33px;}|
|--|--|
|--|--|

**transform---2D转换**
| 属性值 | 描述 |
|--|--|
|translate() 平移 |元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标） 位置参数|
|rotate() 旋转 |	元素顺时针旋转给定的角度（角度单位：deg）。允许负值，元素将逆时针旋转|
|scale() 放大或缩小|	元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数|
|skew() 倾斜、翻转|	元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）参数|

