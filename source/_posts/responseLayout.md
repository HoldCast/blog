title: 响应式布局和移动端适配方案
tags:
  - 响应式
  - 移动适配
  - rem
---
前端响应式开发包括两个方向,web(pc)端的页面显示和移动端的页面显示,一般页面内容比较少,布局相对简单的页面可以直接采用媒体查询的方式来实现响应式;
移动端和PC端需要展示不同的页面样式风格的页面,可以采用pc端响应式,移动端自动适配的方案.
1.响应式布局 2.移动端适配-rem

>不同的需求,采用不同的方案

### 一.响应式布局
1.设计思路：
使用CSS3中媒体查询的大致思路就是判断网页在不同设备中所处的宽度范围，这样的范围可能有三种（PC、平板、手机），也可能有四种（PC、平板、中大屏手机、小屏手机），当然也可能只需要两种（平板、手机，PC端单独开发一版时可不作为CSS3媒体查询的使用对象），并为各种宽度范围情况下的所需页面元素套用不同的CSS样式，从而适配各种设备。

<!-- more -->

2.响应式网页开发中的宽度问题：
在实际开发中，通常需要设置响应式网页宽度的最大值，一旦忽略最大宽度，臃肿或零散的网页布局都会造成视觉洪灾，也就是我们常说的看起来很low。
目前最为常见的宽度基本上都是：大于或等于960px的PC端（1920px、1600px、1440px、1280px、1140px、960px）、960px至640px之间的平板端（768px、640px）以及640px以下的手机端（480px、320px），以上宽度存在已久，且显示设备中的网页宽度会长期处于这样的状态下，在响应式网页宽度设计上，基本从这几个尺寸考虑就已经足够。

3.初始化设置：
在HTML文件中，网页顶部<head></head>标签中插入一句话：
```
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
```
这句话在于对响应式网页做一个初始化设置，主要包括：
name="viewport"：标记显示设备为视口；
width = device-width：宽度等于当前设备的宽度；
initial-scale：初始的缩放比例（默认设置为1.0）；
minimum-scale：允许用户缩放到的最小比例（默认设置为1.0）；
maximum-scale：允许用户缩放到的最大比例（默认设置为1.0）；
user-scalable：用户是否可以手动缩放（默认设置为no，因为我们不希望用户放大缩小页面）。

4.解决IE浏览器的兼容性问题：
因为IE浏览器(IE8)不支持HTML5和CSS3中的media，所以要加载用于解决IE浏览器兼容性问题的JS文件：
```
    <!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
    <script src="https://oss.maxcdn.com/libs/respond.js/1.3.0/respond.min.js"></script>
    <![endif]-->
```
两个<script></script>标签中的src属性所指向的文件链接地址为固定地址中的文件，直接异地引用就好，不用下载到本地引用。

5.设置IE的渲染方式为最高：
现在有很多人的IE浏览器都升级到IE9以上，这个时候会有很多诡异的事情发生，例如现在是IE9的浏览器，但是浏览器的文档模式却是IE8，为了防止这种情况，我们需要下面这段代码来让IE的文档模式永远都是最新：
```
<meta http-equiv="X-UA-Compatible"content="IE=edge">
```
当然还有一个更给力的写法：
```
<meta http-equiv="X-UA-Compatible"content="IE=Edge，chrome=1">
```
这段代码后面加了一个chrome=1，这是由于Google Chrome Frame（谷歌内嵌浏览器框架GCF），如果用户电脑安装这个chrome插件，就可让电脑内的IE浏览器规避版本因素，使用Webkit引擎及V8引擎进行排版及运算。当然如果用户没装这个插件，这段代码就会让IE浏览器以最高的文档模式展现效果。

6.CSS3 media 媒体查询的写法：
```
@media screen and (max-width: 960px){body{background:#000;}}
```
这是一个media的标准写法，在CSS文件中，意为：当页面小于960px时执行以下CSS代码，具体内容暂不用管。
对于上述代码中的screen，意为在告知设备在打印页面时使用衬线字体，在屏幕上显示时用无衬线字体。目前很多网站都会直接省略screen,从而不需要考虑用户打印网页的需求，所以又有这种写法：
```
@media (max-width: 960px){
    body{background:#000;}
}
```
本着思维严谨的原则，一般不采用这种写法。

7.CSS3媒体查询主体代码组合：
在响应式网页布局中需要持续运用媒体查询代码组合，主要作用在于判断所适配屏幕的宽度，并根据各种宽度条件套用不同的CSS样式。
- 如当屏幕宽度等于960px时，将网页背景色变为红色：
```
@media screen and (max-device-width:960px){
    body{background:red;}
}
```

- 如当屏幕宽度最大为960px（小于960px）时，将网页背景色变为黑色：
```
@media screen and (max-width: 960px){
    body{background:#000;}
}
```

- 如当屏幕宽度最小为960px（大于960px）时，将网页背景色变为桔色：
```
@media screen and (min-width:960px){
    body{background:orange;}
}
```

- 更为常见的是混合使用，如当屏幕宽度介于960px和1200px之间时，将网页背景色变为黄色：
```
@media screen and (min-width:960px) and(max-width:1200px){
    body{background:yellow;}
}
```

8.media媒体查询所有参数汇总：
媒体查询器中还包含并不常用的相关功能，悉如示下：
width:浏览器可视宽度，
height:浏览器可视高度，
device-width:设备屏幕的宽度，
device-height:设备屏幕的高度，
orientation:检测设备目前处于横向还是纵向状态，
aspect-ratio:检测浏览器可视宽度和高度的比例(例如：aspect-ratio:16/9)，
device-aspect-ratio:检测设备的宽度和高度的比例，
color:检测颜色的位数（例如：min-color:32就会检测设备是否拥有32位颜色），
color-index:检查设备颜色索引表中的颜色（他的值不能是负数），
monochrome:检测单色楨缓冲区域中的每个像素的位数（这个太高级，估计咱很少会用的到），
resolution:检测屏幕或打印机的分辨率(例如：min-resolution:300dpi或min-resolution:118dpcm)，
grid：检测输出的设备是网格的还是位图设备。

9.扩展——在CSS2中同样有媒体查询：
media媒体查询并不是CSS3诞生之后的专用功能，早在CSS2开始就已经支持media，比如：
在HTML文件中的<head></head>标签中写入这句：
```
<link rel="stylesheet"type="text/css" media="screen"href="style.css">
```
以上是CSS2实现的衬线用法，href属性中写入在某单一显示设备中链接的CSS文件，但仅供入门，
如要判断移动设备是否为纵向放置的显示屏，可以这样写：
```
<link rel="stylesheet" type="text/css"media="screen and (orientation:portrait)"href="style.css">
```
如要让小于960px的页面执行指定的CSS样式文件，可以这样写：
```
<link rel="stylesheet"type="text/css" media="screen and (max-width:960px)"href="style.css">
```
CSS2中的媒体查询方法放到现在并不推荐使用，最大的弊端在于这样会增加页面http的请求次数，增加页面负担，使用CSS3中的媒体查询才是目前的最佳方法。

---
### 二.移动端rem适配
---
1.设计思路:
rem是css3相对根节点(html)的字体大小的单位,通过设备宽度算出每个rem所对应的px,来实现动态适配.

2.动态设置html的font-size,根据参照的设备宽度设置1rem = ?px;
屏幕的总宽度即为(均分份数)16rem.
```
var html = document.documentElement;
var width = html.getBoundingClientRect().width;     //设备尺寸绝对宽度(width = window.screen.width)
html.style.fontSize = width / 16 + 'px';            //将屏幕分成16份：iphone5下（320/16） 1rem = 20px;
//html.style.fontSize = width / 15 + 'px';          //将屏幕分成15份：iphone6下（375/15） 1rem = 25px;
//html.style.fontSize = width / 18 + 'px';          //将屏幕分成15份：iphone6s调试
```

3.编写样式时,所有的尺寸单位均使用rem即可,实际开发中可使用编辑器的转换插件将px转成对应的rem值.

---
[【查看源码】](https://github.com/HoldCast/resposive)