# 开发报告：
### 策划思路：
1、	希望构建一个书评和乐评一体的评论性网站页面，页面简洁。<br>
2、	详细页的文章来自豆瓣
### 页面结构与说明：
1、	组成：站点由欢迎界面（welcome.html）、首页（首页.html）、列表页（列表页.html）、某书评页（详细页_bookc.html）、某乐评页（详细页_musicc.html）和之前做的表单页（调查问卷.html）<br>
2、	欢迎界面：主要使用了js插件，形成页面滑动的情况。最终页面从：“进入”按钮进入首页。<br>
3、	首页：上部分由网站名，搜索栏以及导航栏组成。主体部分为上下两块，上部分左边为推荐栏，右边为音乐播放器。音乐播放器随机播放歌曲，可以切换歌曲或者切换频道。
下部分由最新栏和排行榜（最热）组成，最新栏分为书评、乐评、评论（不针对某本书或某首歌，针对某个作者歌手甚至某个类别）、专题（主要为一些专访，以及相似主题的推荐）。<br>
4、列表页：上部分与首页一样，多了一个目录栏（类似“首页>书评>文章”），主题部分保留音乐播放器和排行榜。左边部分形成列表，下方有页码切换栏（只有样子，暂不能执行）。<br>
5、某书评页：上部分与列表页相同，也有目录栏。保留音乐播放器。原排行榜部分改为相关书评。左边部分包括文章标题，笔者，评论的书，评论时间，正文部分，以及书籍信息。<br>
6、某乐评页：整体与书评页类似，去掉了音乐随机播放器，相关书评改为相关乐评。原书籍信息部分改为音乐信息：歌名，歌手，专辑，词曲，这首音乐的播放，歌词。

### 技术指标：（列表）

|兼容设置|`<meta>http-equiv="x-ua-compatible" content="IE=EmulateIE9`|
|------|------|
|使用版本| 主要是html和css|
|html5|`<audio>`,`<section>`|
|css3|background-size;border-radius;overflow;box-shadow|
|开发工具|浏览器：谷歌浏览器；编辑器：Sublime Text|

### 技术点说明：
一、<br>
1、要求：在欢迎页面的下方，在同一行能出现几个圆点（并且能设置大小）。使得点击时，能切换到相应页面。<br>
2、前提：运用了js模板，只要能新建出以`<ul>``<li>``<li>``<ul>`标签为基础的元素，并将class名与模板的js文件中相对应，点击时就能实现切换。<br>
3、相关知识背景：<br>
（1）border-radius：圆角边框
- 详细值：border-top-left-radius
border-top-right-radius
border-bottom-left-radius
border-bottom-right-radius
- 如果省略 bottom-left，则与 top-right 相同。如果省略 bottom-right，则与 top-left 相同。如果省略 top-right，则与 top-left 相同。
- 例：
border-radius: 2em 1em 4em / 0.5em 3em;
等价于：
border-top-left-radius: 2em 0.5em;
border-top-right-radius: 1em 3em;
border-bottom-right-radius: 4em 0.5em;
border-bottom-left-radius: 1em 3em;

（2）display：
- display:block：
block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。
block元素可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。
block元素可以设置margin和padding属性。
- display:inline：
inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。
inline元素设置width,height属性无效。
inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。
- display:inline-block：
简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性
4、最终解决方案：每个圆就是一个li块，通过给li块设置border- radius来实现其成为一个圆。并且给li设置`display:inline-block。最终给ul设置文本居中：text-align:center，使得几个圆可以呈现在中央（就左右而言）<br>
5、关键代码说明：
```
ul{
	position: absolute;
	bottom:20px;
	text-align: center;
	width:100%;
	padding: 0px;
}
li{
	display: inline-block;
	border-radius: 100%;
	width:20px;
	height:20px;
}
```
二、<br>
1、要求：在页面切换的过程中整个ul会向上浮动，切换完毕又回到原本位置？清除浮动。<br>
2、相关知识背景及关键代码说明：
- overflow 属性规定这个属性定义溢出元素内容区的内容会如何处理。如果值为 scroll，不论是否需要，用户代理都会提供一种滚动机制。因此，有可能即使元素框中可以放下所有内容也会出现滚动条。
- 例子：两个div:
```
#box{ 
          width:500px; 
          background:#000; 
          height:500px;
 } 
#content { 
          float:left; 
          width:600px; 
          height:600px; 
          background:red;
 }
 ```
- overflow:hidden这个属性的作用是隐藏溢出，并且可以清除浮动。给box加上这个属性后，content 的宽高自动的被隐藏掉了。另外，若将box这个div的高度值删除后，box的高度自动的被content 这个div的高度值给撑开了。上述的浮动不仅仅是一个平面上的浮动，而是一个立体的浮动。也就是说，当content 这个div加上浮动这个属性的时候，在显示器的侧面，它已经脱离了box这个div，也就是说，此时的content 的宽高是多少，对于已经脱离了的box来说，都是不起作用的。当我们全面的理解了浮动这个词的含义的时候，我们就理解overflow:hidden这个属性中的解释，清除浮动是什么意思了。也就是说，当我们给box这个div加上overflow:hidden这个属性的时候，其中的content 等等带浮动属性的div的在这个立体的浮动已经被清除了。这就是overflow:hidden这个属性清除浮动的准确含义。当我们没有给box这个div设置高度的时候，content 这个div的高度，就会撑开box这个div，而在另一个方面，我们要注意到的是，当我们给box这个div加上一个高度值，那么无论content 这个div的高度是多少，box这个高度都是我们设定的值。而当content 的高度超过box的高度的时候，超出的部分就会被隐藏。这就是隐藏溢出的含义。<br>

4、	最终解决方案：给body设置overflow:hidden;<br>
三、<br>
1、要求：想在网页中运用字体库中没有的字体，但下载字体到电脑字体库中后，应用仍无效。<br>
2、关键代码说明：
```
@font-face { 
/* font-properties */ 
font-family: pictos; 
src:url(‘pictos/pictos-web.woff’),    //也可以是网页链接
url(‘pictos/pictos-web.ttf’), 
url(‘pictos/pictos-web.eot’); /* IE9 */ 
} 
```
font-family定义字体的名字，接下来的src是加载字体文件的位置，之所有有多个url就是因为浏览器兼容问题。<br>
3、最终解决方案：<br>
在css文件中输入以下：
```
@font-face {
font-family: 'Hakku'; 
src:url('../font/白舟·白雨.ttf');
} 
@font-face {
font-family: 'XinGothic-ZhangYue W6'; 
src:url('../font/信黑体 W6.ttf');
}
```
四、<br>
1、问题：顶栏使用了display :inline-block发现块下沉。设置div块的margin发现div中的元素位置不变，但是div的整体框架向外扩。导致无法调整div块中元素的位置。想要在不改变position：static为absolute（块会重叠）的情况下实现。<br>
2、相关知识背景：<br>
vertical-align 属性设置元素的垂直对齐方式。<br>
该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。

|值|描述|
|--|----|
|baseline|默认。元素放置在父元素的基线上。|
|sub|垂直对齐文本的下标。|
|super|垂直对齐文本的上标|
|top|把元素的顶端与行中最高元素的顶端对齐|
|text-top|把元素的顶端与父元素字体的顶端对齐|
|middle|把此元素放置在父元素的中部。|
|bottom|把元素的顶端与行中最低的元素的顶端对齐。|
|text-bottom|	把元素的底端与父元素字体的底端对齐。|
|%|使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。|
|inherit|规定应该从父元素继承 vertical-align 属性的值。|

4、	最终解决方案：将下沉的块设置vertical-align:top;再定位。<br>
5、	关键代码说明：
```
.smalltitle{
	display:inline-block;
	margin-left: 30px;
	margin-top:50px;
	vertical-align: top;
	font-size: 25px;
}
```
### 开发心得：
    这次网站的困难主要集中在初期。因为第一个做的是欢迎界面，接触的一开始就是相对不熟悉一些的js，尽管我只是用了个插件，将相关的代码扒了出来。但是因为不熟悉，我需要看着demo网页一点点地查代码，将没用的去掉。尽管耗时较长，但也从中学到了许多。我认为其中最有用的是，我开始习惯用浏览器修改代码，而不是向一开始那样，在sublime text 上埋头苦干，做了好长一大段，才打开浏览器看一眼。这些熟练和经验使得我后面的页面做的速度比起一开始快了不少。<br>
	并且，我发现，很多问题若不是在真真切切地做网页，是一直发现不了的。像是上面列出的技术难题，在第一次遇到的时候真的是没有头绪很苦恼，只好一点点查手册寻找解决办法。但是在解决了之后，做后面的页面时我发现这些的问题是经常出现的，这些我自己摸索出来的解决方法其实很实用。<br>
	学习这门课程一开始很多都听不懂，也有点跟不上。直到一次我误解了老师不知道的作业，以为老师的要求很高，于是只好自己去网上把html和css的主要课程看下来。在这之后，我才开始慢慢适应这门课。这恰好证明了如何做好网页——自学和动手做。总体来说，感觉自己收获了许多。<br>

