## canvas

[TOC]

### 1.什么是 canvas?

- canvas 是 HTML5提供的一个新标签,可通过javascript脚本绘制2D 图形.
- canvas 最早在 Apple 引入,后来又在 Safari 和 Google Chrome中实现

### 2.canvas 的特点

- canvas 是一个矩形区域的画布,可以用 JavaScript 在上面绘画,控制其每一个像素.
- canvas 标签使用 JavaScript 在网页绘制图像,本身不具备绘图功能.

### 3.canvas 的应用领域

- 游戏:
- 可视化数据:数据图表化 比如:百度的 echart
- banner广告
- 未来模拟器
- 未来远程计算机控制
- 未来图形编辑器

### 4.canvas 语法

- 不要使用 CSS 控制它的宽和高,会让图片进行拉伸
- 重新设置 canvas标签的宽高属性会让画布擦除所有的内容
- 可以给 canvas画布通过 style 属性设置其它属性
- canvas 默认宽高300px 和 150px

### 5.常用操作方法

#### a. getContext("2d");

- 用于获得画布上下文对象,然后才可以对画布进行操作,参数2d 表示当前画布支持2D 绘图,如果希望将当前画布支持3d ,则传入" webgl"

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext();
```

#### b. ctx.beginPath() 设置绘制的开始

#### c. ctx.closePath() 设置绘制的结束

#### d. ctx.moveTo() 设置绘制的起点

#### e. ctx.lineTo() 

#### f. ctx.stroke() 对绘制路径进行描边填充

#### g. ctx.fill() 对绘制路径进行内部填充

#### h. ctx.rect( x,y,width,height) 绘制矩形路径

- x ,y 代表左上角位置坐标
- width 和 height 代表矩形的宽和高

#### i. ctx.fillRect(x,y,width,height) 绘制填充矩形

#### j. ctx.strokeRect(x,y,width,height) 绘制描边矩形

#### k. ctx.clearRect(x,y,width,height) 擦除矩形

#### l. ctx.arc(x,y,r,sAngle,eAngle,counterclockwise) 绘制圆弧

- x,y 圆心的位置坐标
- sAngle, 和 eAngle 是开始弧度和结束弧度
- counterclockwise 是 bool 值,决定是否逆时针 默认 false

### 6. 常用属性

#### a. ctx.strokeStyle 设置描边颜色样式

```javascript
ctx.strokeStyle = "red";
ctx.strokeStyle = "#efe";
ctx.strokeStyle = "rgba(0,0,0,0.5)";
```

#### b. ctx.fillStyle 设置填充颜色样式

#### c. ctx.lineWidth 设置线条宽度

```javascript
ctx.lineWidth= 3px;
```

### 7.应用实例

#### 绘制点线

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

#### 绘制矩形

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

#### 绘制文本

```javascript
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

#### 绘制弧形

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

#### 绘制图片

```javascript
<img id="img" src="./monkey.jpg" alt="无法显示图片">
    <canvas id="canvas" width="300" height="300">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");

      canvas.style.border = "1px solid red";
      // 获得画布
      var ctx = canvas.getContext("2d");

      var img = document.getElementById("img");

      //等待图片加载完毕
      img.onload = function() {
        //绘制图片时，一定要保证图片加载完毕

        // img x y
        ctx.drawImage(img,100,100);

        // img x y width height
        ctx.drawImage(img, 0, 0, 100, 100);

        // img sx sy swidth sheight x y width height
        cxt.drawImage(img, 57, 96, 97, 97, 350, 350, 45, 45);
      }
    </script>
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

#### 径向渐变

```javascript
<canvas id="canvas" width="500" height="500">您的浏览器不支持canvas</canvas>
    <script type="text/javascript">
      var canvas = document.getElementById("canvas");
      var ctx = canvas.getContext("2d");
	  // 创建渐变对象 x0,y0,r0 (渐变开始圆的横纵坐标,半径) x1,y1,r1 (渐变结束时的圆的横纵坐标,半径) 
      var circle = ctx.createRadialGradient(300,300,50,300,300,200);
      circle.addColorStop(0, 'red');
	  //添加一个渐变颜色，第一个参数介于 0.0 与 1.0 之间的值，表示渐变中开始与结束之间的位置。
      circle.addColorStop(0.5, 'blue');
      circle.addColorStop(1, 'yellow');
	  //关键点，把渐变设置到 填充的样式
      ctx.fillStyle = circle ;
      ctx.arc(300,300,200, 0, 2 * Math.PI);
      ctx.fill();
    </script>
```

#### 画布缩放

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

#### 画布原点的移动

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

#### 画布旋转

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

#### 画布状态保存

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

#### 画布保存为图片

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

#### 画布透明

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

#### 画布裁剪

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





















