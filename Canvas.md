## canvas

[TOC]

### 1.什么是 canvas?

- canvas 是 HTML5提供的一个新标签,可通过javascript脚本绘制2D 图形.
- canvas 最早在 Apple 引入,后来又在 Safari 和 Google Chrome中实现
- canvas 是非常炫酷的功能,它能很简洁的进行2D 绘图,还可以进行游戏的开发
- 低版本的 IE 不支持

### 2.canvas 的特点

- canvas 是一个矩形区域的画布,可以用 JavaScript 在上面绘画,控制其每一个像素.
- canvas 标签使用 JavaScript 在网页绘制图像,本身不具备绘图功能.
- 如果浏览器不支持,它就显示 canvas 的内容

### 3.canvas 的应用领域

- 游戏:
- 可视化数据:数据图表化 比如:百度的 echart
- banner广告
- 未来模拟器
- 未来远程计算机控制
- 未来图形编辑器

### 4.canvas 语法

- 不要使用 CSS 控制它的宽和高,会让图片进行拉伸
- canvas 要在标签内设置宽和高,也就是标签内的自己的属性,canvas 默认宽高300px 和 150px
- 不能在 css 和 js 里边设置宽和高,可以 canvas.width 和 canvas.height 设置
- 重新设置 canvas标签的宽高属性会让画布擦除所有的内容
- 可以给 canvas画布通过 style 属性设置其它属性
- canvas 是行元素
- canvas 坐标遵循笛卡尔坐标系,原点在左上角

### 5.常用操作方法

#### a. getContext("2d");

- 用于获得画布上下文对象,然后才可以对画布进行操作,参数2d 表示当前画布支持2D 绘图,如果希望将当前画布支持3d ,则传入" webgl"

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext();
```

#### b. ctx.beginPath() 设置绘制的开始

#### c. ctx.closePath() 设置绘制的结束

#### d. ctx.moveTo(x,y) 设置绘制的线段起点

#### e. ctx.lineTo(x,y) 设置绘制线段的终点 

- x,y 代表坐标值

#### f. ctx.stroke() 对绘制路径进行描边填充

#### g. ctx.fill() 对绘制路径进行内部填充

```javascript
// 绘制一条线段
cxt.beginPath(); // 开始作画

cxt.moveTo(100,100); // 设置开始坐标,参数皆为 number类型
cxt.lineTo(500,400);

cxt.lineWidth = 5; // 线条宽度
cxt.strokeStyle = "blue";  // 线条颜色

cxt.stroke();  // 描边
cxt.closePath();

// 绘制一个三角形
cxt.beginPath();
cxt.moveTo(300,100);
cxt.lineTo(150,300);
cxt.lineTo(450,300);
cxt.lineTo(300,100);

cxt.lineWidth = 2; // 线条宽度
cxt.strokeStyle = "#ff0";  // 线条颜色

cxt.stroke();  // 描边
cxt.closePath();
```

#### h. ctx.rect( x,y,width,height) 绘制矩形路径

- x ,y 代表左上角位置坐标
- width 和 height 代表矩形的宽和高

#### i. ctx.fillRect(x,y,width,height) 绘制填充矩形

#### j. ctx.strokeRect(x,y,width,height) 绘制描边矩形

#### k. ctx.clearRect(x,y,width,height) 擦除矩形

```javascript
// 绘制矩形
cxt.beginPath();
cxt.rect(100,100,300,300);

cxt.lineWidth  = 3;
cxt.strokeStyle = "#333";

// 注意: 先设置样式,再进行喧染
cxt.stroke();
cxt.closePath();

cxt.beginPath()
cxt.strokeRect(200,200,300,300);
cxt.closePath();
```

#### l. ctx.arc(x,y,r,sAngle,eAngle,counterclockwise) 绘制圆弧

- x,y 圆心的位置坐标
- sAngle, 和 eAngle 是开始弧度和结束弧度
- counterclockwise 是 bool 值,决定是否逆时针 默认 false

```javascript
// 画弧形
    // 1. 在 canvas中,角度都是弧度
    // 2. 0角度为3点钟方向,顺时针为正,逆时针为负
    // 3. cxt.arc(圆心 x, 圆心 y, 半径长度,起始角度,结束角度,是否逆时针);

cxt.beginPath();
cxt.arc(200,200,100,0,2 * Math.PI ,false);
cxt.fillStyle = "#000";
cxt.strokeStyle = "#000";
cxt.fill();
cxt.stroke();
cxt.closePath();
```

```javascript
// 扇形
cxt.beginPath();
cxt.arc(300,300,200,0,Math.PI/2,false);
cxt.moveTo(300,502);
cxt.lineTo(300,302);
cxt.lineTo(500,302);
cxt.stroke();
cxt.fillStyle = "#f00";
cxt.fill();
cxt.closePath();
```

#### m.arcTo(第一个点 x,第一个点 y,第二个点 x,第二个点 y,半径长度) 画弧形,两个点确定一个弧

```javascript
// arcTo(第一个点 x,第一个点 y,第二个点 x,第二个点 y,半径长度) 画弧形,两个点确定一个弧
// 使用该方法需要在使用之前加一个起点

cxt.beginPath();
cxt.moveTo(20,20);
cxt.arcTo(300,100,100,300,50);
cxt.lineTo(100,300);
cxt.stroke();
cxt.closePath();
```

### 6. 常用属性

#### a. ctx.strokeStyle 设置描边颜色

```javascript
ctx.strokeStyle = "red";
ctx.strokeStyle = "#efe";
ctx.strokeStyle = "rgba(0,0,0,0.5)";
```

#### b. ctx.fillStyle 设置填充颜色

#### c. ctx.lineWidth 设置线条宽度

```javascript
ctx.lineWidth= 3px;
```

#### d. cxt.font  设置文字属性

```javascript
cxt.font = "bold 50px 'STKaiti'";
```

#### e. cxt.textAlign 设置水平对齐方式

```javascript
// cxt.textAlign 设置水平对齐方式 start,end,left,center,right
cxt.textAlign = "center";
```

#### f. cxt.textBaseline

```javascript
// cxt.textBaseline 设置垂直对齐方式 top,bottom.middle
cxt.textBaseline = "middle";
```

#### g. 阴影 x 轴的偏移量 / y 轴的偏移量 (shadowOffsetX/shadowOffsetY)

#### h. 阴影颜色 /模糊度 (shadowColor / shadowBlur)

```javascript
cxt.shadowOffsetX = 30;
cxt.shadowOffsetY = 30;
cxt.shadowColor = "#0f0";
cxt.shadowBlur = 10;
```

#### i. 坐标轴形变 translate( x , y) / scale(x缩放倍数, y 缩放倍数) / rotate(旋转弧度)

```javascript
// 坐标轴形变:先移动,然后旋转,最后再缩放,超出画布内容不显示

// cxt.translate(目标 x, 目标 y) 坐标轴平移
// cxt.scale(x 缩放倍数, y 缩放倍数) 缩放
// cxt.rotate(旋转弧度)

// 把坐标轴的原点平移到坐标轴的最中间

cxt.beginPath();
cxt.translate(300,300);
// 坐标轴旋转 67 度
cxt.rotate(Math.PI/180*67);
cxt.scale(3,2);

cxt.shadowOffsetX = 30;
cxt.shadowOffsetY = 30;
cxt.shadowColor = "#0f0";
cxt.shadowBlur = 10;

cxt.arc(0,0,50,0,2*Math.PI,false);
cxt.fill();

cxt.closePath();
```

#### j.旋转 window.requestAniamationFrame()

```javascript
// window.requestAnimationFrame 帧动画,按照关键帧的频率进行循环操作

// 正方形旋转
var deg = 0;
cxt.fillStyle = "#f00";
function rect() {
    deg++;
    cxt.save();
    cxt.clearRect(0,0,600,600);
    // 移动坐标原点
    cxt.translate(300,300);
    cxt.rotate(Math.PI/180 * deg);
    cxt.fillRect(-100,-100,200,200);
    cxt.restore();
    window.requestAnimationFrame(rect);
}
rect();
```

#### k. cxt.globalAlpha 透明

### 7.应用实例

#### 绘制点线 moveTo() 和 lineTo()

```javascript
<!-- 1. 新建画布区域 -->
    <canvas id="canvas" width="1000" height="1000"></canvas>
    
    <script type="text/javascript">
    var canvas = document.getElementById('canvas'); 
    // 2. 获得画布 上下文对象 ‘2d’ 表示当前画布支持 2D绘图
    var ctx = canvas.getContext('2d');
    
    // 设置绘制开始 每次重新绘制一个路径的开始
    ctx.beginPath();
    // 移动绘制的起始位置
    ctx.moveTo(170,170);
    // 绘制点的位置
    ctx.lineTo(300,300);
    // 描边
    ctx.stroke();
    // 设置绘制结束
    ctx.closePath(); 
    
    ctx.beginPath();
    ctx.moveTo(50,50);
    ctx.lineTo(150,50);
    ctx.lineTo(150,150);
    ctx.lineTo(50,150);
    ctx.lineTo(50,50);
    
    // 内部填充
    ctx.fill();
    ctx.closePath();
    </script>
```

#### 绘制矩形 fillRect() 和 strokeRect()

```javascript
<canvas id="canvas" width="300" height="300"></canvas>
    <script type="text/javascript">
    var canvas = document.getElementById('canvas');
    // 2. 获得画布 上下文对象 ‘2d’ 表示当前画布支持 2D绘图
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    // 绘制矩形 起点位置 10 10 width 50px height 50px
    ctx.rect(10,10,50,50);

    // 填充矩形  （指定位置）
    ctx.fillStyle = "red";
    ctx.fillRect(20,20,20,20);
    // 矩形描边 需要对属性先进行设置
    ctx.lineWidth = 3;
    ctx.strokeStyle = "#300";
    // 绘制矩形 起点位置 10 10 width 50px height 50px
    ctx.strokeRect(10,10,50,50);

    ctx.closePath();
    ctx.beginPath();
    // 擦除矩形
    // ctx.clearRect(x,y,width,height);

    // 绘制圆弧
    ctx.fillStyle = "blue";
    ctx.arc(250, 250, 100, 0, Math.PI * 0.5, false);
    ctx.fill();
    </script>
```

#### 绘制文本  fillText() 和 strokeText()

```javascript
// cxt.font 设置文字属性
// cxt.textAlign 设置水平对齐方式 start,end,left,center,right
// cxt.textBaseline 设置垂直对齐方式 top,bottom.middle

<canvas id="canvas" width="300" height="300"></canvas>
    <script type="text/javascript">
      var canvas = document.getElementById('canvas');
      // 获得画布
      var ctx = canvas.getContext('2d');
      
      ctx.font = "50px '宋体'";
      ctx.textAlign = "center";
      // fillText(text,x,y,maxwidth) maxwidth 可设置最大宽度
      // 绘制实体文本
      ctx.fillText("fillText",100,100);
      // 绘制边框文本
      ctx.strokeText("strokeText",100,200);
    </script>
```

#### 绘制弧形 arc()

```javascript
<canvas id="canvas" width="300" height="300">你的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      canvas.style.border = "1px solid red";
      // 获得画布
      var ctx = canvas.getContext('2d');

      ctx.fillStyle = "blue";
      ctx.arc(100, 50, 100, 0, Math.PI, false);
      ctx.fill();
    </script>
```

#### 绘制贝塞尔曲线 (二次cxt.quadraticCurveTo)/(三次cxt.bezierCurveTo)

```javascript
// 二次贝塞尔曲线
// cxt.quadraticCurveTo(控制点 x, 控制点 y, 终点 x, 终点 y);

cxt.beginPath();
cxt.moveTo(300,300);
cxt.quadraticCurveTo(200,200,300,240);
cxt.stroke();
cxt.moveTo(300,300);
cxt.quadraticCurveTo(400,200,300,240);
cxt.stroke();
cxt.fillStyle = "#FF0000";
cxt.fill();
cxt.closePath();

// 三次贝塞尔曲线
// cxt1.bezierCurveTo(控制点1x,控制点1y, 控制点2x, 控制点2y, 终点 x, 终点 y)
cxt1.translate(150,100);

cxt1.beginPath();
cxt1.moveTo(0,100);
cxt1.bezierCurveTo(50,70,90,120,0,200);
cxt1.stroke();
cxt1.fillStyle = "#FF0000";
cxt1.fill();
cxt1.closePath();

// 关于 y = 0 对称

cxt1.beginPath();
cxt1.moveTo(0,100);
cxt1.bezierCurveTo(-50,70,-90,120,0,200);
cxt1.stroke();
cxt1.fillStyle = "#FF0000";
cxt1.fill();
cxt1.closePath();
```

#### 绘制图片 drawImage()

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>空地反弹</title>
	<style media="screen">
		#canvas {
			border: 2px solid red;
			display: block;
			margin: 0 auto;
		}
	</style>
</head>
<body>
	<canvas id="canvas" width="400" height="400">
		您的浏览器不支持 canvas! 太low了,赶快升级吧!
	</canvas>

	<script src="./js/jquery-2.0.3.js" charset="utf-8"></script>
	<script type="text/javascript">
		var canvas = $("#canvas");
		var cxt = canvas.get(0).getContext("2d");

		// 1. drawImage(图片资源,开始点的 x, 开始点的 y);
		// 		注意: 图像不会被压缩,完全显示在 canvas区域中

		var img = $("<img />");
		img.prop("src","./img/bg2.jpg");

		// 注意:只有在图片加载完成之后,才能完成 canvas 的图片绘制
		img.load(function() {
			// cxt.drawImage(this,0,0);
		});

		// 2. drawImage("资源",绘制图片的左上角 x, 绘制图片的左上角的 y, 绘制宽度,绘制高度);
		// 		注意: 把图片绘制到指定的区域,图片会被压缩
		img.load(function() {
			// cxt.drawImage(this,0,0,200,200);
		});

		// 3. drawImage("资源",图像起始 x, 图像起始 y, 图像的宽,图像的高,canvas 起始 x,canvas 起始 y,canvas 图像宽,canvas图像高);
		// 		注意:

		img.load(function() {
			cxt.drawImage(this,100,100,100,100,200,200,100,100);
		});
	</script>
</body>
</html>
```

#### 绘制阴影

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      // 获得画布
      var ctx = canvas.getContext("2d");

      //  阴影颜色
      ctx.shadowColor = 'green';

      // 阴影模糊级别
      ctx.shadowBlur = 10;

      // 水平移动距离
      ctx.shadowOffsetX = 10;

      // 垂直移动距离
      ctx.shadowOffsetY = 10;

      // 填充颜色
      ctx.fillStyle = 'red';

      // 绘制填充矩形
      ctx.fillRect(100,100,100,100);
    </script>
```

#### 线性渐变 createLinearGradient()

```javascript
// 线性渐变 (起点 x, 起点 y, 终点 x,终点 y)
var circle = cxt.createLinearGradient(100,200,100,500);
circle.addColorStop(0, '#0f0');
//添加一个渐变颜色，第一个参数介于 0.0 与 1.0 之间的值，表示渐变中开始与结束之间的位置。
circle.addColorStop(0.2, '#0ff');
circle.addColorStop(0.4, '#f0f');
circle.addColorStop(0.6, '#0ff');
circle.addColorStop(0.8, '#f00');
circle.addColorStop(1, '#ff0');
//关键点，把渐变设置到 填充的样式
cxt.fillStyle = circle ;
cxt.fillRect(100,200,100,300);

// 
var circle1 = cxt.createLinearGradient(100,200,100,500);
circle1.addColorStop(0.0, '#0f0');
circle1.addColorStop(0.2, '#0f0');
circle1.addColorStop(0.2, '#f0f');
circle1.addColorStop(0.4, '#f0f');
circle1.addColorStop(0.4, '#0ff');
circle1.addColorStop(0.6, '#0ff');
circle1.addColorStop(0.6, '#f00');
circle1.addColorStop(0.8, '#f00');
circle1.addColorStop(0.8, '#ff0');
circle1.addColorStop(1.0, '#ff0');
//关键点，把渐变设置到 填充的样式
cxt.fillStyle = circle1 ;
cxt.fillRect(300,200,100,300);
```

#### 径向渐变 createRadialGradient()

```javascript
// 径向渐变 (起始圆心 x, 起始圆心 y, 结束圆心 x,结束圆心 y,半径)
var circle = cxt.createRadialGradient(300,300,100,300,300,300);
circle.addColorStop(0.0, '#0f0');
circle.addColorStop(0.2, '#0f0');
circle.addColorStop(0.2, '#f0f');
circle.addColorStop(0.4, '#f0f');
circle.addColorStop(0.4, '#0ff');
circle.addColorStop(0.6, '#0ff');
circle.addColorStop(0.6, '#f00');
circle.addColorStop(0.8, '#f00');
circle.addColorStop(0.8, '#ff0');
circle.addColorStop(1.0, '#ff0');
//关键点，把渐变设置到 填充的样式
cxt.fillStyle = circle ;
cxt.fillRect(0,0,600,600);
```

#### 画布缩放 scale()

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");

      ctx.strokeStyle = "red";
      ctx.lineWidth = 4;
      ctx.strokeRect(0,0,100,100);

      ctx.scale(2,2);
      ctx.strokeRect(0,0,100,100);
      ctx.strokeRect(100,100,10,10);
    </script>
```

#### 画布原点的移动 translate()

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");

      ctx.translate(100,100);
      ctx.strokeStyle = "red";
      ctx.lineWidth = 4;
      ctx.strokeRect(10,10,100,100);
    </script>
```

#### 画布旋转 rotate()

```javascript
<canvas id="canvas" width="500" height="500"></canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");
      // 旋转 20度
      ctx.rotate( 20 * Math.PI / 180);
      // 设置画布填充颜色为红色
      ctx.fillStyle = "red";
      // 绘制矩形
      ctx.fillRect(300,0,200,200);
      // 填充颜色
      ctx.fill();
    </script>
```

#### 画布状态保存和恢复 save() 和 restore()

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      // 获得画布
      var ctx = canvas.getContext("2d");
      // 
      ctx.strokeStyle = "red";
      ctx.strokeRect(0,0,100,100);
      // 保存状态
      ctx.save();
      
      ctx.scale(2,2);
      ctx.strokeRect(0,0,100,100);
      
      // 恢复到没有放大的状态
      ctx.restore();
      ctx.strokeRect(100,100,50,50);
    </script>
```

#### 画布保存为图片 canvas.toDataURL()

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      // 获得画布
      var ctx = canvas.getContext("2d");

      ctx.fillStyle = "red";
      ctx.fillRect(10,10,100,100);

      // 将画布导出为图片
      var img1 = canvas.toDataURL('image/png',1);
      // base64 编码格式的图片
      console.log(img1);

      var str = new Image();
      str.src = img1;
      document.body.appendChild(str);

      /*
        base64 格式的图片的优缺点
        优点:将图片转换为字符串，不用发送http请求，减少去请求的数量，减轻服务器端的压力
        缺点:转换之后体积会变大
        应用场景: 图片体积很小的时候可以使用
      */
    </script>
```

#### 画布透明 cxt.globalAlpha

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas> 
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");
      
      // 第一块 黄色
      ctx.fillStyle = '#FD0';
      ctx.fillRect(0,0,75,75);
      // 第二块 绿色
      ctx.fillStyle = '#6C0';
      ctx.fillRect(75,0,75,75);
      // 第三块 蓝色
      ctx.fillStyle = '#09F';
      ctx.fillRect(0,75,75,75);
      // 第四块 红色
      ctx.fillStyle = '#F30';
      ctx.fillRect(75,75,75,75);
      
      ctx.fillStyle = '#fff';
      ctx.globalAlpha = 0.2;
      
      for (i=0;i<7;i++){
        ctx.beginPath();
        // 原点坐标 75 75  半径 相差10
        ctx.arc(75,75,10+10*i,0,Math.PI*2,false);
        ctx.fill();
      }
    </script>
```

#### 画布裁剪 cxt.clip()

```javascript
<canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");
      // 绘制圆
      ctx.strokeStyle = "red";
      ctx.arc(100,100,100,0,Math.PI * 2,false);
      ctx.stroke();
      // 画布裁剪
      ctx.clip();
      
      // 绘制矩形
      ctx.fillStyle = "green";
      ctx.fillRect(0,0,100,100);
    </script>
```

#### 画布渲染画布 

```javascript
<div id="draw">将画布1上的部分区域显示到画布2上</div>
    <canvas id="canvas-1" width="234" height="300"></canvas>
    <canvas id="canvas-2" width="468" height="600"></canvas>

    <script type="text/javascript">
      var draw = document.getElementById("draw");
      var canvas1 = document.getElementById("canvas-1");
      var canvas2 = document.getElementById("canvas-2");

      canvas1.style.border = "1px solid red";
      canvas2.style.border = "1px solid red";

      var ctx1 = canvas1.getContext("2d");
      var ctx2 = canvas2.getContext("2d");

      // 绘制图片
      var img = new Image();
      img.onload = function() {
        // 图片加载完毕之后，绘制到ctx1上
        ctx1.drawImage(img,0,0,234,300);
      }
      img.src = "./mi.jpg";

      // 将画布1上的部分区域显示到画布2上
      draw.onclick = function() {
        ctx2.drawImage(canvas1, 67, 71, 110, 50, 0, 0, 110*2, 50*2);
      }
    </script>
```

#### 视频播放 video.oncanplay

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>视频播放</title>
		<style type="text/css">
			#canvas {
				border: 2px solid red;
				display: block;
				margin: 0 auto;
			}
			
			video {
				display: none;
			}
		</style>
	</head>
	<body>
		<canvas id="canvas" width="600" height="400">
			你的浏览器不支持canvas!
		</canvas>
		<video id="vplay" width="600" height="400">
			<source src="./video/1.mp4" type="video/mp4"></source>
		</video>
		<script type="text/javascript">
			var canvas = document.getElementById("canvas");
			var cxt = canvas.getContext("2d");
			
			var video = document.getElementById("vplay");
			// canvas 视频播放就像电影胶片一样,把视频整理成一张张生动的图片,
			// 然后使用绘图方法循环绘制到 canvas 中,形成动画效果
			// 只有在视频加载完成之后,才能播放
			// video.oncanplay 视频加载完成播放
			
			video.oncanplay = function(){
				// 播放视频
				video.play();
				function move(){
					cxt.clearRect(0,0,600,400);
					cxt.drawImage(video,0,0,600,400);
					window.requestAnimationFrame(move);
				}
				move();
			};
		</script>
	</body>
</html>
```

### 8.实例

#### 空地反弹

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>空地反弹</title>
	<style media="screen">
		#canvas {
			border: 2px solid red;
			display: block;
			margin: 0 auto;
		}
	</style>
</head>
<body>
	<canvas id="canvas" width="600" height="600">
		您的浏览器不支持 canvas! 太low了,赶快升级吧!
	</canvas>

	<script src="./js/jquery.min.js" charset="utf-8"></script>
	<script type="text/javascript">

		var myCan = $("#canvas");
		var cxt = myCan.get(0).getContext("2d");

		// 设置 Ball 构造函数
		function Ball() {
			this.r = ranNum(5,20);
			this.x = ranNum(this.r,myCan.width() - this.r);
			this.y = ranNum(this.r,myCan.height() - this.r);
			this.color = "rgb("+ ranNum(0,255) +","+ ranNum(0,255) +","+ ranNum(0,255) +")";
			this.speedX = ranNum(2,10) * (ranNum(0,1) ? 1 : -1);
			this.speedY = ranNum(2,10) * (ranNum(0,1) ? 1 : -1);
		}

		// 添加方法
		Ball.prototype = {
			// 绘制
			draw:function() {
				cxt.beginPath();
				cxt.arc(this.x , this.y , this.r , 0 , Math.PI * 2 ,false);
				cxt.fillStyle = this.color;
				cxt.fill();
				cxt.closePath();
			},

			// 移动
			move:function() {
				this.x += this.speedX;
				this.y += this.speedY;

				// 碰左
				if (this.x <= this.r) {
					this.x = this.r;
					this.speedX *= -1;
					// this.speedY *= -1;
				}

				// 碰右
				if (this.x >= myCan.width() - this.r) {
					this.x = myCan.width() - this.r;
					this.speedX *= -1;
					// this.speedY *= -1;
				}

				// 碰上
				if (this.y <= this.r) {
					this.y = this.r;
					// this.speedX *= -1;
					this.speedY *= -1;
				}

				// 碰下
				if (this.y >= myCan.height() - this.r) {
					this.y = myCan.height() - this.r;
					// this.speedX *= -1;
					this.speedY *= -1;
				}
			}
		}

		// 创建小球
		var balls = [];
		myCan.get(0).onclick = function() {
			var ball = new Ball();
			balls.push(ball);
		}
		for (var i = 0; i < 20; i++) {
			var ball = new Ball();
			balls.push(ball);
		}

		// 小球运动
		var timeId = setInterval(function() {
			cxt.clearRect(0,0,myCan.width(),myCan.height());
			for (var i = 0; i < balls.length; i++) {
				balls[i].draw();
				balls[i].move();
			}
		},15);

		// 随机数
		function ranNum(a, b){
			var max = Math.max(a, b);
			var min = Math.min(a, b);
			return Math.floor(Math.random() * (max - min + 1) + min);
		}
	</script>
</body>
</html>
```

#### 碰撞检测

```html
<!doctype html>
<html>

<head>
	<meta charset="UTF-8">
	<title>碰撞检测</title>
	<style type="text/css">
		* {
			margin: 0;
			padding: 0;
		}

		#wp {
			width: 600px;
			height: 500px;
			border: 1px solid;
			position: relative;


		}

		#box {
			width: 50px;
			height: 50px;
			background: red;
			position: absolute;
			border-radius: 50%;
		}

		#box2 {
			width: 100px;
			height: 100px;
			background: orange;
			position: absolute;
			top: 150px;
			left: 250px;
		}
	</style>

</head>

<body>
	<div id="wp">
		<div id="box"></div>
		<div id="box2"></div>
	</div>

	<script type="text/javascript">
		var wp = document.getElementById('wp');
		var box = document.getElementById('box');
		var box2 = document.getElementById('box2');


		var bl = box.offsetLeft;

		var bt = box.offsetTop;
		var bv = 1;
		var bv2 = 1;
		var aa;

		setInterval(function() {

			if (bl >= (wp.clientWidth - box.offsetWidth) || bl < 0) {
				bv *= -1;
			}
			if (bt >= (wp.clientHeight - box.offsetHeight) || bt < 0) {
				bv2 *= -1;
			}


			//左上角，右上角，左下角，右下角
			if (!(bl == box2.offsetLeft - box.offsetWidth && bt == box2.offsetTop - box.offsetHeight || bl == box2.offsetLeft + box2.offsetWidth && bt == box2.offsetTop - box.offsetHeight || bl == box2.offsetLeft - box.offsetWidth && bt == box2.offsetTop +
					box2.offsetHeight || bl == box2.offsetLeft + box2.offsetWidth && bt == box2.offsetTop + box2.offsetHeight)) {
				if (bl > (box2.offsetLeft - box.offsetWidth) && bl < box2.offsetLeft + box2.offsetWidth && bt > (box2.offsetTop - box.offsetWidth) && bt < (box2.offsetTop + box2.offsetHeight)) {
					bv *= -1;
					bv2 *= -1;
				}

				// 左侧
				else if (bl == (box2.offsetLeft - box.offsetWidth) && bt >= (box2.offsetTop - box.offsetWidth) && bt <= (box2.offsetTop + box2.offsetHeight)) {
					bv *= -1;
				}
				// 上侧
				else if (bt == (box2.offsetTop - box.offsetHeight) && bl >= (box2.offsetLeft - box.offsetWidth) && bl <= box2.offsetLeft + box2.offsetWidth) {
					bv2 *= -1
				}

				// 右侧
				else if (bl == (box2.offsetLeft + box2.offsetWidth) && bt >= (box2.offsetTop - box.offsetWidth) && bt <= (box2.offsetTop + box2.offsetHeight)) {
					bv *= -1;
				}
				// 下侧
				else if (bt == (box2.offsetTop + box2.offsetHeight) && bl >= (box2.offsetLeft - box.offsetWidth) && bl <= box2.offsetLeft + box2.offsetWidth) {
					bv2 *= -1
				}
			}

			bl += bv;
			bt += bv2;

			box.style.left = bl + "px";
			box.style.top = bt + "px";
		}, 10)
	</script>
</body>
</html>
```

#### 图像合并

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>图像合并</title>
	<style media="screen">
		#canvas {
			border: 2px solid red;
			display: block;
			margin: 0 auto;
		}
	</style>
</head>
<body>
	<canvas id="canvas" width="600" height="600">
		您的浏览器不支持 canvas! 太low了,赶快升级吧!
	</canvas>

	<script type="text/javascript">
		var canvas = document.getElementById("canvas");
		var cxt = canvas.getContext("2d");

		// cxt.globalCompositionOperation() 合并图像属性
		// source-over:默认值,表示新图在老图上面
		// source-in:保留新老图的重合部分,其他部分清空,新图在上面
		// source-out:保留 新图中 新图和老图 的 非 重合部分,其他全部清空
		// source-atop:保存老图 和 新图与老图的重叠部分,新图在上,其他全部清空

		// destination-over:保留新图和老图,老图在上
		// destination-in:保留新老图的重合部分,其他部分清空,老图在上面
		// destination-out:保留 老图中 新图和老图 的 非 重合部分,其他全部清空
		// destination-atop:保存新图 和 新图与老图的重叠部分,老图在上,其他全部清空
		cxt.beginPath();
		cxt.fillStyle = "#f00";
		cxt.fillRect(100,100,200,200);
		cxt.closePath();

		cxt.globalCompositeOperation = "destination-atop";

		cxt.beginPath();
		cxt.fillStyle = "#ff0";
		cxt.fillRect(200,200,200,200);
		cxt.closePath();

		// copy:只保留新图,其他清空
		// lighter:贤显示新图和老图
		// xor:保留新图和老图之间的非重叠部分
	</script>
</body>
</html>
```

#### 制作房产证

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>制作房产证</title>
	<style media="screen">
	 	* {
	 		margin: 0;
			padding: 0;
	 	}
		.wrap {
			padding-top: 20px;
			text-align: center;
		}

		#canvas {
			border: 2px solid red;
			display: block;
			margin: 0 auto;
		}
	</style>
</head>
<body>
	<div class="wrap">
		<input id="getName" type="text" name="" value="">
		<input id="btn1" type="button" name="" value="提交">
		<input id="btn2" type="button" name="" value="导出">
		<canvas id="canvas" width="549" height="412">
			您的浏览器不支持 canvas!
		</canvas>
	</div>
	<script src="./js/jquery-2.0.3.js" charset="utf-8"></script>
	<script type="text/javascript">
		var canvas = document.getElementById('canvas');
		var cxt = canvas.getContext("2d");

		$("<img/>").prop("src","./img/bg3.jpg").load(function() {
			cxt.drawImage(this,0,0);
		});

		$("#btn1").click(function() {
			var value = $.trim($("#getName").val());
			if (value!="") {
				cxt.beginPath();
				cxt.font = "20px '宋体'";
	     		cxt.textAlign = "center";
				cxt.fillStyle = "#555";
				cxt.fillText(value,230,125);
				cxt.closePath();
			} else {
				alert("请输入姓名!");
			}
		});

		$("#btn2").click(function() {
			// canvas中的图片存储在 URL中,并且进行了 base64 转码
			// cxt.toDataURL(图片格式,压缩比例) 参数都是可选,默认为 img, 比例为0.92
			// 压缩比例在 0-1之间
			// 图片类型: image/web image/jpeg

			// 注意:保存图片的时候尽量保存在服务器上
			var imgURL = canvas.toDataURL('image/png',0.5);
			console.log(imgURL);
			window.open(imgURL,'_blank');
		});
	</script>
</body>
</html>
```

#### 刮刮乐

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>刮刮乐</title>
	<style media="screen">
	 	* {
	 		margin: 0;
			padding: 0;
	 	}
		.wrap {
			width: 320px;
			height: 568px;
			margin: 0 auto;
			background: url("./img/bg.png") no-repeat;
			background-size: 100% 100%;
			display: block;
			position: relative;
		}
		.wrap p ,
		#canvas{
			position: absolute;
			top: 190px;
			left: 28px;
		}

		.wrap p {
			font-size: 30px;
			text-align: center;
			line-height: 134px;
			height: 134px;
			width: 263px;
		}
	</style>
</head>
<body>
	<div class="wrap">
		<p></p>
		<canvas id="canvas" width="263" height="134">
			您的浏览器不支持 canvas! 太low了,赶快升级吧!
		</canvas>
	</div>
	<script src="./js/jquery.min.js" charset="utf-8"></script>
	<script type="text/javascript">
		var canvas = $("#canvas")
		var cxt = canvas.get(0).getContext("2d");

		// 绘制灰色图层
		cxt.beginPath();
		cxt.fillStyle = "#ccc";
		cxt.fillRect(0,0,263,134);
		cxt.closePath();

		// 刮刮操作
		canvas.mousedown(down);

		// 创建鼠标按下方法
		function down() {
			canvas.mousemove(move);
			//
			function move(ev) {
				// 获取鼠标在 canvas中的坐标点
				var dx = ev.pageX - $(this).offset().left;
				var dy = ev.pageY - $(this).offset().top;
				// console.log(dx,dy);

				// 设置合并属性
				cxt.globalCompositeOperation = "destination-out";

				// 绘制新图
				cxt.beginPath();
				cxt.arc(dx,dy,20,0, 2 * Math.PI,false);
				cxt.fill();
				cxt.closePath();

				// 当清空面积达到 80%;清空所有
				// getImageData(起始 x, 起始 y, 获取图形的宽度,获取图像的高度)
				var imgData = cxt.getImageData(0,0,canvas.width(),canvas.height());
				// console.log(imgData);

				var colorBox = imgData.data;
				// console.log(colorBox.length);
				var count = 0;
				for (var i = 0; i < colorBox.length; i+=4) {
					if (colorBox[i+3] == 0) {
						count++;
					}
				}

				console.log(count);
				// 判断是否是 50% ;
				if (count >= colorBox.length/ 4 * 0.5) {
					cxt.clearRect(0,0,canvas.width(),canvas.height());
				}
			}

			// 设置 up方法
			canvas.mouseup(up);
			function up() {
				$(this).off("mousemove");
			}
		}

		$(".wrap p").text("你上当了");
	</script>
</body>
</html>
```

#### 放大镜

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas放大镜</title>
	<style media="screen">
		#canvas {
			border: 2px solid red;
			display: block;
			margin: 0 auto;
		}
	</style>
</head>
<body>
	<canvas id="canvas" width="300" height="450">
		您的浏览器不支持 canvas!
	</canvas>

	<script src="./js/jquery-2.0.3.js" charset="utf-8"></script>
	<script type="text/javascript">
		var canvas = $("#canvas");
		var cxt = canvas.get(0).getContext("2d");

		$("<img/>").prop("src","./img/bg4.jpg").load(function() {
			cxt.drawImage(this,0,0,canvas.width(),canvas.height());
		});

		// 设置鼠标进入图片操作
		function enter() {

			canvas.mousemove(move);

			function move(ev) {
				cxt.clearRect(0,0,canvas.width(),canvas.height());

				// 再次绘制
				var img1 = $("<img/>").prop("src","./img/bg4.jpg").get(0);
				cxt.drawImage(img1,0,0,canvas.width(),canvas.height());

				var dx = ev.pageX - canvas.offset().left;
				var dy = ev.pageY - canvas.offset().top;

				// 设置合并属性
				// cxt.globalCompositeOperation = "destination-out";

				// 开始绘制
				cxt.beginPath();
				cxt.arc(dx,dy,40,0,Math.PI*2,false);
				cxt.fill();
				cxt.closePath();

				// 设置合并属性
				// cxt.globalCompositeOperation = "destination-over";

				var img2 = $("<img/>").prop("src","./img/bg4.jpg").get(0);
				cxt.drawImage(img2,dx*2-40,dy*2-40,80,80,dx-40,dy-40,80,80);
			}

			canvas.mouseleave(leave);

			function leave() {
				cxt.clearRect(0,0,canvas.width(),canvas.height());
				
				var img1 = $("<img/>").prop("src","./img/bg4.jpg").get(0);
				cxt.drawImage(img1,0,0,canvas.width(),canvas.height());
			}
		}

		enter();
	</script>
</body>
</html>
```

#### 钟表

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>canvas钟表</title>
		<style media="screen">
			body {
				background-color: #eee;
			}
	
			#canvas {
				border: 2px solid red;
				display: block;
				margin: 0 auto;
			}
	</style>
	</head>
	<body>
		<canvas id="canvas" width="600" height="600">
			您的浏览器不支持 canvas! 太 low 了,赶快升级吧!
		</canvas>
		<script type="text/javascript">
			var canvas = document.getElementById("canvas");
			var cxt = canvas.getContext("2d");
			// 画表
			var positions = [
				["#333",0,0,200,0,Math.PI * 2,false], // 外圈
				["#fff",0,0,180,0,Math.PI * 2,false], // 内圈
				["#333",0,0,10,0,Math.PI * 2,false] //  中心点
			];
			
			var deg = 0;
			function draw() {
				deg++;
				cxt.clearRect(0,0,canvas.width,canvas.height);
				cxt.save();
				cxt.translate(300,300);
				// 起始点设置为12点
				cxt.rotate(-Math.PI/2);
				// 边框
				for (var i = 0; i < 3; i++) {
					cxt.beginPath();
					cxt.fillStyle = positions[i][0];
					cxt.arc(positions[i][1],positions[i][2],positions[i][3],positions[i][4],positions[i][5],positions[i][6]);
					cxt.fill();
					cxt.closePath();
				}

				// 刻度
				for (var i = 0; i < 60; i++) {
					cxt.save();
					cxt.beginPath();
					cxt.rotate(Math.PI/180 * (i*6));
					if(i%5 == 0){
						//大刻度
						cxt.fillRect(-180,-5,20,10);
					} else {
						// 小刻度
						cxt.fillRect(-180,-2,10,4);
					}
					cxt.closePath();
					cxt.restore();
				}
				
				// canvas 文字
				cxt.beginPath();
				cxt.rotate(Math.PI/2);
				cxt.font = "50px '宋体'";
				cxt.fillStyle = "crimson";
				cxt.textAlign = "center";
				cxt.fillText("canvas",5,100);
				cxt.closePath();
				
				cxt.rotate(-Math.PI/2);
				
				// 时针
//				cxt.beginPath();
//				cxt.fillStyle = "#333";
//				cxt.rotate((Math.PI/180) * (deg * 1/3600/60));
//				cxt.fillRect(-20,-4,130,8);
//				cxt.closePath();
//	
//				// 分针
//				cxt.beginPath();
//				cxt.fillStyle = "#333";
//				cxt.rotate((Math.PI/180) * (deg * 1/10));
//				cxt.fillRect(125,-3,-150,6);
//				cxt.closePath();
//	
//				// 秒针
//				cxt.beginPath();
//				cxt.fillStyle = "red";
//				cxt.rotate((Math.PI/180) * (deg * 6));
//				cxt.fillRect(130,-4,-160,6);
//				cxt.closePath();
//	
				cxt.restore();
			}
			draw();
			
			// 画表针
			function drawZhen() {
				// 获取当前系统时间
				var time = new Date();
				var h = time.getHours(); // 时
				var m = time.getMinutes(); // 分
				var s = time.getSeconds(); // 秒
				
				//画时针
				cxt.save();
				cxt.translate(300,300);
				cxt.rotate(Math.PI/180 * h * 30 + Math.PI/180 * m/60*30 + Math.PI/180 * s/3600*30);
				cxt.fillRect(-4,-110,8,130);
				cxt.restore();
				
				//画分针
				cxt.save();
				cxt.translate(300,300);
				cxt.rotate(Math.PI/180 * m * 6 + Math.PI/180 * s/60*6);
				cxt.fillRect(-2,-130,6,150);
				cxt.restore();
				
				//画秒针
				cxt.save();
				cxt.translate(300,300);
				cxt.rotate(Math.PI/180 * s * 6);
				cxt.fillStyle = "crimson";
				cxt.fillRect(-2,-130,4,150);
				cxt.restore();
			}
			
			function move(){
				cxt.clearRect(0,0,canvas.width,canvas.height);
				draw();
				drawZhen();
				window.requestAnimationFrame(move);
			}
			move();
			setInterval(move,1000);

		</script>
	</body>
</html>
```

#### 视频马赛克原理

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>视频马赛克</title>
		<style type="text/css">
			#canvas {
				border: 2px solid red;
				display: block;
				margin: 0 auto;
			}
			
			video {
				display: none;
			}
			
			.btns {
				text-align: center;
				margin-top: 20px;
			}
			
			button {
				height: 30px;
				padding: 0 10px;
				line-height: 30px;
				cursor: pointer;
			}
		</style>
	</head>
	<body>
		<canvas id="canvas" width="600" height="400">
			你的浏览器不支持canvas!
		</canvas>
		<video id="vplay" width="600" height="400">
			<source src="./video/1.mp4" type="video/mp4"></source>
		</video>
		<div class="btns">
			<button id="play">播放</button>
			<button id="wuma">高清无码</button>
			<button id="fma">方形马赛克</button>
			<button id="yma">圆形马赛克</button>
			<button id="stop">暂停</button>
		</div>
		<script type="text/javascript">
			var canvas = getId("canvas");
			var cxt = canvas.getContext("2d");
			
			var video = getId("vplay");
			
			// 获取 按钮
			var play = getId("play");
			var wuma = getId("wuma");
			var fma = getId("fma");
			var yma = getId("yma");
			var stop = getId("stop");
			
			var isMosaic = false;
			var shape = "";
			
			// 点击播放按钮
			play.onclick = function(){
				vplay.play();
				draw();
			}
			
			// 点击暂停按钮
			stop.onclick = function(){
				vplay.pause();
			}
			
			// 点击高清无码
			wuma.onclick = function(){
				isMosaic = false;
			}
			
			// 方形马赛克
			fma.onclick = function(){
				isMosaic = true;
				shape = 'square';
			}
			
			// 圆形马赛克
			yma.onclick = function(){
				isMosaic = true;
				shape = 'circle';
			}
			
			// 绘制方法
			function draw(){
				cxt.clearRect(0,0,600,400);
				cxt.drawImage(vplay,0,0,600,400);
				
				// 判断是否有马赛克
				if(isMosaic){
					// 马赛克的原理就是把播放的图片分成一块一块的小图,并给这些小图,并给这些小图设置统一的颜色
					var imageData = cxt.getImageData(0,0,600,400);
					
					// 清除原来的图片
					cxt.clearRect(0,0,600,400);
					// 设置马赛克小格子的宽和高
					var height = 5;
					var width = 5;
					
					// 获取宽高为5px 的行和列 h:80 w:120
					var row = Math.floor(canvas.height / height);
					var col = Math.floor(canvas.width / width);
					
					// 遍历每个小格
					for (var i = 0 ; i< row;i++) {
						for (var j = 0; j < col; j++) {
							// 找最中间的点
							var x = j * width + Math.floor(width/2);
							var y = i * height + Math.floor(height/2);
							
							// 找该点的位置在像素数组中的下标
							var pos = (y-1) * canvas.width * 4 + x * 4;
							var colors = imageData.data;
							
							// 获取这个点的 rgb
							var r = colors[pos];
							var g = colors[pos + 1];
							var b = colors[pos + 2];
							
							// 设置填充颜色
							cxt.fillStyle = "rgb("+ r +","+ g +","+ b +")";
							
							// 判断马赛克的类型
							if(shape == 'square'){
								// 方形马赛克
								cxt.beginPath();
								cxt.fillRect(x - Math.floor(width/2),y - Math.floor(height/2),width,height);
								cxt.closePath();
							} else {
								// 圆形马赛克
								cxt.beginPath();
								cxt.arc(x,y,Math.floor(width/2),0,2*Math.PI,false);
								cxt.fill();
								cxt.closePath();
							}
						}
					}
				}
					
				// 设置循环
				window.requestAnimationFrame(draw);
			}
			
			// 获取id
			function getId(id) {
				return document.getElementById(id);
			};
		</script>
	</body>
</html>
```

#### 悟空棒

```php

```

### 9. canvas滤镜  getImageData() 获取像素信息

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>canvas滤镜</title>
		<style type="text/css">
			#canvas {
				border:  2px solid red;
				display: block;
				margin: 0 auto;
			}
			
			#btn {
				text-align: center;
			}
			
			button {
				cursor: pointer;
				height: 30px;
				line-height: 30px;
				text-align: center;
			}
		</style>
	</head>
	<body>
		<canvas id="canvas" width="600" height="900">
			您的浏览器不支持 canvas!
		</canvas>
		<div id="btn">
			<button>原图</button>
			<button>取反</button>
			<button>灰度</button>
			<button>黑白</button>
		</div>
		<script src="js/jquery-2.0.3.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			var canvas = $("#canvas");
			var cxt = canvas.get(0).getContext("2d");
			
			//判断是否加载完毕
			var dol = false;
			
			//绘制
			$("<img/>").prop("src","img/bg4.jpg").load(function(){
				cxt.drawImage(this,0,0);
				dol = true;
			});
			
			// 获取所有按钮
			var btns = $("button");
			
			// 点击原图
			btns.eq(0).click(function(){
				if (dol) {
					cxt.clearRect(0,0,canvas.width(),canvas.height());
					
					// 绘制
					var img = $("<img/>").prop("src","img/bg4.jpg");
					cxt.drawImage(img.get(0),0,0);
				}
			});
			
			// 取反:把图上所有点的 rgb 值转化为和255的差(255-当前值);
			btns.eqa(1).click(function(){
				if(dol){
					var imageData = cxt.getImageData(0,0,canvas.width(),canvas.height());
					var colors = imageData.data;
					
					for(var i = 0; i < colors.length;i+=4){
						colors[i] = 255 - colors[i];
						colors[i+1] = 255 - colors[i+1];
						colors[i+2] = 255 - colors[i+2];
					}
					
					// 更新数据 使用 cxt.putImageData(数据对象,开始第一个像素的 x, 开始第一个像素的y)
					cxt.putImageData(imageData,0,0);
				}
			});
			
			// 灰度: 其实就是求 rgb 的平均值
			btns.eq(2).click(function(){
				if(dol){
					var imageData = cxt.getImageData(0,0,canvas.width(),canvas.height());
					var colors = imageData.data;
					
					for(var i = 0; i < colors.length;i+=4){
						var mul = (colors[i] + colors[i+1] + colors[i+2]) / 3;
						colors[i] = mul;
						colors[i+1] = mul;
						colors[i+2] = mul;
					}
					cxt.putImageData(imageData,0,0);
				}
			});
			
			// 黑白: rgb的 平均值大于128改为255,小于的改为0
			btns.eq(3).click(function(){
				if(dol){
					var imageData = cxt.getImageData(0,0,canvas.width(),canvas.height());
					var colors = imageData.data;
					
					for(var i = 0; i < colors.length;i+=4){
						var mul = (colors[i] + colors[i+1] + colors[i+2]) / 3;
						mul = mul > 128 ? 255 : 0;
						colors[i] = mul;
						colors[i+1] = mul; 
						colors[i+2] = mul; 
					}
					cxt.putImageData(imageData,0,0);
				}
			});
		</script>
	</body>
</html>
```



