&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;上周一不小心拖更了，所以这周决定痛定思痛，马上开始着手这周的博客~<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<canvas>标签本身我了解的就不多，所以很早前就想专门系统地学一次，整理一篇博客出来。这周就来说说它吧\~
* <canvas>标签概述<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Canvas是HTML5中新增的标签之一。它就像一块幕布，我们可以用JavaScript在上面绘制各种图表、动画等。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Canvas出现前，绘图只能借助Flash插件来实现，页面不得不用JavaScript和Flash进行交互。而有了Canvas后，我们就再也不需要Flash了，可以直接使用JavaScript来实现绘制。
* 基本使用方法<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在html中的写法如下：
```
<canvas id="testCanvas" width="300" height="150"></canvas>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;需要注意的是，width和height是<canvas>标签的属性而不是样式。要规定<canvas>的尺寸，必须以上面代码中的形式来写，不能写在样式中，否则画布尺寸会变得匪夷所思。另外，300 x 150也是它的默认属性。<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在JS中的写法如下：
```
var canvas = document.getElementById('testCanvas');
//var canvas = $('#testCanvas')[0];
var ctx = canvas.getContext('2d');
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先，和所有的JS方法一样，我们要先获取到它。如果是使用jQuery获取，则需要将获取到的jQuery对象转换成DOM对象，也就是加一个[0]即可。<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<canvas>元素有一个叫做 getContext()的方法，这个方法是用来获得渲染上下文和它的绘画功能的。总之，在正式开始绘制前，都要使用这个方法，才能开始正常的绘制。getContext()只有一个参数：上下文的格式。<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在绘制开始前，我们还要先了解一下Canvas的坐标系统：<br/>
![](https://cdn.webxueyuan.com/cdn/files/attachments/001436926614788af8f274570d54736bddbbf7b2b03a9eb000/l)
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Canvas的坐标以左上角为原点，水平向右为X轴，垂直向下为Y轴，以像素为单位，所以每个点都是非负整数。<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面列举一些最常用的绘制命令：
```
ctx.fillRect (x, y, width, height)  //绘制一个填充的矩形，默认为黑色
ctx.fillStyle = "rgb(0,0,0)"  //设置填充颜色
ctx.strokeRect(x, y, width, height) //绘制一个矩形的边框
ctx.clearRect(x, y, width, height) //清除指定的矩形区域，让清除部分完全透明。类似于橡皮擦的功能

```
```
ctx.beginPath()  //开始绘制
ctx.closePath()  //闭合路径
ctx.stroke()  //通过线条来绘制图形轮廓
ctx.fill()  //通过填充路径的内容区域生成实心的图形
//当调用fill()函数时，所有没有闭合的形状都会自动闭合，所以就不需要再调用closePath()函数了。但是调用stroke()时不会自动闭合
ctx.moveTo(x, y)  //移动笔触
ctx.lineTo(x, y)  //绘制直线
ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise)
//画一个以（x,y）为圆心、以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成
```
* 简单的绘制<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;终于可以开始画了~先画几个简单的例子：
```
<canvas id="testCanvas" width="500" height="500"></canvas>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如上，先在html中布置好画布。后面所有的绘制都在这块画布上进行，就不重复写明了。<br/><br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实例一：
```
<script>
    //必要的获取和申明
    var canvas = $('#testCanvas')[0]
    var ctx = canvas.getContext('2d')
    
    ctx.fillStyle = "rgb(200, 0, 0)"  //左上矩形的颜色
    ctx.fillRect (10, 10, 50, 50)  //左上矩形的位置和尺寸
    
    ctx.fillStyle = "rgba(0, 0, 200, 0.5)"  //右下矩形的颜色和透明度
    ctx.fillRect (30, 30, 50, 50)  //右下矩形的位置和尺寸
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;绘制出的效果如下：<br/>
![](https://mdn.mozillademos.org/files/228/canvas_ex1.png)
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实例二：
```
<script>
    //必要的获取和申明
    var canvas = $('#testCanvas')[0]
    var ctx = canvas.getContext('2d')
    
    ctx.fillRect(25,25,100,100)  //最外层矩形的位置和尺寸（默认黑色填充）
    ctx.clearRect(45,45,60,60)  //将它的中间部分擦除
    ctx.strokeRect(50,50,50,50)  //在擦除的位置画出一个矩形边框
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;绘制出的效果如下：<br/>
![](https://mdn.mozillademos.org/files/245/Canvas_rect.png)
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实例三：
```
<script>
    //必要的获取和申明
    var canvas = $('#testCanvas')[0]
    var ctx = canvas.getContext('2d')
    
    ctx.beginPath()  //开始绘制
    ctx.moveTo(75, 50)  //画笔的起始位置
    ctx.lineTo(100, 75)  //绘制一条直线到指定的坐标
    ctx.lineTo(100, 25)  //绘制一条直线到指定的坐标
    ctx.fill()  //将上面几个点连线成一个闭合图形，并填充相应的颜色
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;绘制出的效果如下：<br/>
![](https://mdn.mozillademos.org/files/9847/triangle.png)
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实例四：
```
<script>
    //必要的获取和申明
    var canvas = $('#testCanvas')[0]
    var ctx = canvas.getContext('2d')
    
    //填充三角形
    ctx.beginPath()
    ctx.moveTo(25,25)
    ctx.lineTo(105,25)
    ctx.lineTo(25,105)
    ctx.fill()

    //描边三角形
    ctx.beginPath()
    ctx.moveTo(125,125)
    ctx.lineTo(125,45)
    ctx.lineTo(45,125)
    ctx.closePath()  //上面提到stroke()不会自动闭合，所以在调用前要先用closePath()方法让图形闭合
    ctx.stroke()
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;绘制出的效果如下：<br/>
![](https://mdn.mozillademos.org/files/238/Canvas_lineTo.png)
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实例五：
```
<script>
    //必要的获取和申明
    var canvas = $('#testCanvas')[0]
    var ctx = canvas.getContext('2d')
    
    ctx.beginPath()
    ctx.arc(75, 75, 50, 0, Math.PI*2, true)  //绘制最外层的圆形
    ctx.moveTo(110, 75)
    ctx.arc(75, 75, 35, 0, Math.PI, false)  //嘴巴，false代表顺时针，起始点在右侧嘴角处
    ctx.moveTo(65, 65)
    ctx.arc(60, 65, 5, 0, Math.PI*2, true)  //左眼
    ctx.moveTo(95, 65)
    ctx.arc(90, 65, 5, 0, Math.PI*2, true)  //右眼
    ctx.stroke()
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;绘制出的效果如下：<br/>
![](https://ww1.sinaimg.cn/large/0060lm7Tly1flinb9r9vnj3046046t8j.jpg)
* 简单的动画<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最后来实现一段最简单的动画吧~代码如下：
```
<script>
	var canvas = $('#testCanvas')[0]
	var ctx = canvas.getContext('2d')
 	
 	//设置一个每10毫秒运行一次的函数，当它每次运行，都会刷新画布，并重新绘制一个红色小球
    setInterval(function () {
        run(ctx)
    }, 10)

    var speed = 0  //设置初始速度为0，但这个speed并不是小球真正的速度
	var startPoint = 500  //小球的初始位置，设定在画布的最右侧

	function run(cxt) {
	    speed =- 1  //每次函数运行时，speed就-1，单位是px
	    cxt.clearRect(0, 0, 500, 500) //刷新画布，擦除原有的小球
	    startPoint += speed  //更新后小球的位置
	    
	    cxt.beginPath()
	    cxt.arc(startPoint, 100, 30, 0, 2*Math.PI, true)
	    ctx.fillStyle = "red"
	    cxt.fill()
	}
</script>
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;由于没有找到特别好的办法把动画效果贴出来(= =!)，所以就简单描述一下吧~<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这是一个红色的圆形从右至左做匀速直线运动的动画。它的原理是，每隔10毫秒就把上一个小球擦除，重新在新的位置上绘制一个新的小球，这样看起来就像是同一个小球在做匀速直线运动了。其中，speed是每次函数运行小球“移动”的距离。在这段代码中，每10毫秒，小球移动1px，因为它的实际速度是100px/s。