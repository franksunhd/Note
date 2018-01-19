## SVG

[TOC]

### 1. 什么是 SVG?

- SVG 是可伸缩的矢量图形,通过 XML方式来绘制图形,并且放大或者缩小,或者改变尺寸都不会影响图片的质量
- SVG 是 万维网联盟的标准.

### 2. SVG 和 Canvas 的区别

- SVG 是基于 XML 绘制的2d 图形 , canvas 是通过 JavaScript 绘制的2d 图形
- canvas 可以以 .png 和 .jpg 格式进行图片保存 , 而 SVG 格式的图片不可以保存

### 3.起步

```xml
<?xml version="1.0" standalone="no"?>
<!-- 这是对XML的声明
  version 表示版本号
  standalone 表示是否是独立的 包含是否对外部文件的引用
  这里是 DTD 文件
-->
<!--
  引用了外部的 SVG DTD 文件 这个文件是位于 W3C,包含所有的 SVG 元素
 -->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<!--
    1. 什么是 SVG ?
      SVG 是可伸缩矢量图形,使用 XML 格式定义图形,放大缩小或改变尺寸不会影响图像的质量
      SVG 是万维网联盟的标准

    2.SVG 和 canvas 的区别在于:
      1). SVG 是基于 XML 绘制的2D图形,canvas 是通过 JavaScript 绘制的2D 图形
      2). canvas 是可以以 .png 或 .jpg 格式进行保存的,而 SVG 不可以保存
 -->

<!-- svg 标签是根元素,xmlns定义了 svg 命名空间 width 和 height 定义了文档的宽高 -->
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <!-- circle 定义了圆形 cx cy 圆心位置 , r半径-->
  <circle cx="50" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />

  <!-- rect 定义了矩形 x,y 左上角位置  style 定义样式-->
  <rect x="100" y="100" width="150" height="150" style="fill:blue;stroke:pink;stroke-width:5;fill-opacity:0.5;
  stroke-opacity:1"/>

  <!-- 圆角矩形 rx,ry 定义圆角水平半径和垂直半径 -->
  <rect x="300" y="300" rx="20" ry="20" width="150" height="150" style="fill:blue;stroke:pink;stroke-width:5;fill-opacity:0.5;
  stroke-opacity:1"/>

  <!-- 椭圆 ellipse cx cy 定义了椭圆圆心的位置-->
  <ellipse cx="200" cy="500" rx="100" ry="50" style="fill:blue;stroke-width:5;stroke:yellow;opacity:0.5;" />

  <!-- 直线 line x1,y1 起点位置  x2,y2终点位置-->
  <line x1="300" y1="0" x2="500" y2="200" style="stroke-width:2;stroke:red;"/>

  <!--
    多边形 polygon poly有 many 的含义 gon 有 angle的含义
    points: 指定了多边形每个点的坐标位置 x 值和 y 值之间用逗号分隔
  -->
  <polygon points="200,270 30,280 110,450" style="fill:lime;stroke:purple;stroke-width:1"/>

  <!--绘制五星 -->
  <polygon points="100,10 40,180 190,60 10,60 160,180" transform="translate(10,600)"
  style="fill:red;stroke:orange;stroke-width:5;fill-rule:nonzero;" />
  <!--
     fill-rule 属性判断 绘制的点是否都在路径的内部
        默认:nonzero 非零 发出射线 左至右加一 右至左减一 和为非零在内部
            evenodd 奇偶 发出射线 路径交叉  奇数内部  偶数外部
  -->
  <polygon points="100,10 40,180 190,60 10,60 160,180" transform="translate(250,600)"
  style="fill:red;stroke:orange;stroke-width:5;fill-rule:evenodd;" />

  <!-- 曲线 -->
  <polyline points="20,20 45,30 60,90 20,200" transform="translate(500,50)" style="fill:none;stroke-width:2;stroke:purple;" />

  <polyline points="10,10 10,50 50,50 50,90 90,90 90,130" transform="translate(600,100)" style="fill:none;stroke-width:4;stroke:red;"/>

  <!--
    path 路径
    M:moveTo , L:LineTo , H:横划线 , V垂直划线 , C:曲线 , S: 光滑曲线 , Q: 二次贝塞尔曲线 , T:光滑二次贝塞尔曲线 , A:椭圆的弧 , Z:closePath
  -->

  <path transform="translate(700,100)" d="M150 0 L75 200 L225 200 Z" />

  <g transform="translate(500,300)">
    <!-- AB 线 -->
    <path  id="lineAB" d="M 100 350 l 150 -300" stroke="red"
    stroke-width="3" fill="none" />
    <!-- BC 线 -->
    <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
    stroke-width="3" fill="none" />
    <!-- 切线 l 和 L 的区别在于 大写代表绝对坐标 小写代表相对坐标 -->
    <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
    fill="none" />
    <!-- 二次贝塞尔曲线 -->
    <path d="M 100 350 q 150 -300 300 0" stroke="blue"
    stroke-width="5" fill="none" />
    <!-- 标记点 -->
    <g stroke="black" stroke-width="3" fill="black">
      <circle id="pointA" cx="100" cy="350" r="3" />
      <circle id="pointB" cx="250" cy="50" r="3" />
      <circle id="pointC" cx="400" cy="350" r="3" />
    </g>
    <!-- 标记文本 -->
    <g font-size="30" font="sans-serif" fill="black" stroke="none"
    text-anchor="middle">
      <text x="100" y="350" dx="-30">A</text>
      <text x="250" y="50" dy="-10">B</text>
      <text x="400" y="350" dx="30">C</text>
    </g>
  </g>

  <!-- 文本 -->
  <text x="0" y="15" fill="red" transform="translate(400,30),rotate(30 20,40)">我是 SVG </text>
 </svg>
```

```xml
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="100%" height="100%" viewBox="0 0 640 690">

  <title>DOM Level 3 Events: Event Flow</title>
  <desc>Alternate description</desc>
    
  
  <defs id="defs-1">
    <path id="arrowhead" d="M-9,-4 L0,0 -9,4 Z" stroke-linejoin="round" stroke-linecap="round"/>
    <marker id="blackArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="black" fill="black"  />
    </marker>
    <marker id="redArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="red" fill="red"  />
    </marker>
    <marker id="greenArrow" viewBox="-13 -5 14 10" refX="-4" markerWidth="10" markerHeight="20" orient="auto">
      <use xlink:href="#arrowhead" stroke="green" fill="green"  />
    </marker>

    <filter x="-5%" y="-5%" width="120%" height="120%" id="dropShadow">
      <feGaussianBlur stdDeviation="2 2" in="SourceAlpha"/> 
      <feOffset dx="4" dy="4"/>
      <feComponentTransfer result="shadow">
        <feFuncA type="linear" slope=".55" intercept="0"/>
      </feComponentTransfer>
      <feMerge>
        <feMergeNode/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>

  </defs>
  
  <g id="nodes" font-family="Verdana, sans-serif" font-size="18" fill="black" text-anchor="middle" stroke="none" stroke-width="2">
    <g id="Window-node" transform="translate(310, 10)">
      <a xlink:href="../DOM3-Events.html#glossary-window" target="_parent">
        <rect x="-70" y="0" width="140" height="40" fill="gainsboro" stroke="black" filter="url(#dropShadow)" />
        <text x="0" y="26">Window</text>
      </a>
    </g>

    <g id="document-node" transform="translate(310, 80)">
      <a xlink:href="../DOM3-Events.html#glossary-document" target="_parent">
        <rect x="-60" y="0" width="120" height="40" fill="gainsboro" stroke="black" filter="url(#dropShadow)" />
        <text x="0" y="26">Document</text>
      </a>
    </g>

    <g id="html-node" transform="translate(310, 150)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;html&gt;</text>
    </g>

    <g id="body-node" transform="translate(310, 220)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;body&gt;</text>
    </g>

    <g id="table-node" transform="translate(310, 290)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;table&gt;</text>
    </g>

    <g id="tbody-node" transform="translate(310, 360)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tbody&gt;</text>
    </g>

    <g id="tr_1-node" transform="translate(140, 450)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tr&gt;</text>
    </g>

    <g id="tr_2-node" transform="translate(500, 450)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;tr&gt;</text>
    </g>


    <g id="tr_1_td_1-node" transform="translate(70, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_1_td_1_text-node" transform="translate(70, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Shady Grove</text>
    </g>

    <g id="tr_1_td_2-node" transform="translate(210, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_1_td_2_text-node" transform="translate(210, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Aeolian</text>
    </g>

    <g id="tr_2_td_1-node" transform="translate(430, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="blue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26" fill="white">&lt;td&gt;</text>
    </g>

    <g id="tr_2_td_1_text-node" transform="translate(430, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">
        <tspan x="0" y="34">Over the River,</tspan> <tspan x="0" y="54">Charlie</tspan>
      </text>
    </g>

    <g id="tr_2_td_2-node" transform="translate(570, 540)">
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="lightskyblue" stroke="black" filter="url(#dropShadow)" />
      <text x="0" y="26">&lt;td&gt;</text>
    </g>

    <g id="tr_2_td_2_text-node" transform="translate(570, 610)">
      <ellipse cx="0" cy="35" rx="64" ry="35" fill="steelblue" stroke="black" filter="url(#dropShadow)"/>
      <text x="0" y="40" font-size="15" fill="white" text-anchor="middle">Dorian</text>
    </g>
  </g>
  
  <g id="edges">
    <line id="window-document" x1="310" y1="50" x2="310" y2="73" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="document-html" x1="310" y1="120" x2="310" y2="143" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="html-body" x1="310" y1="190" x2="310" y2="213" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="body-table" x1="310" y1="260" x2="310" y2="283" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>     
    <line id="table-tbody" x1="310" y1="330" x2="310" y2="353" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <path id="tbody-tr_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M310,400 Q310,420 260,420 H160 Q140,420 140,443"/>
    <path id="tbody-tr_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M310,400 Q310,420 380,420 H480 Q500,420 500,443"/>
    <path id="tr_1-tr_2_td_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M140,490 Q140,510 120,510 H90 Q70,510 70,533"/>
    <path id="tr_1-tr_2_td_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M140,490 Q140,510 160,510 H190 Q210,510 210,533"/>
    <path id="tr_2-tr_2_td_1" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M500,490 Q500,510 480,510 H450 Q430,510 430,533"/>
    <path id="tr_2-tr_2_td_2" fill="none" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"
          d="M500,490 Q500,510 540,510 H550 Q570,510 570,533"/>
    <line id="tr_1_td_1-text" x1="70" y1="580" x2="70" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_1_td_2-text" x1="210" y1="580" x2="210" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_2_td_1-text" x1="430" y1="580" x2="430" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
    <line id="tr_2_td_2-text" x1="570" y1="580" x2="570" y2="603" stroke="black" stroke-width="2" marker-end="url(#blackArrow)"/>
  </g>
  
  <g id="event-flow" stroke-dasharray="10,5">
    <g id="capture_phase">
      <a xlink:href="../DOM3-Events.html#glossary-capture-phase" target="_parent"><text fill="red" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="150" y="220">Capture</tspan> <tspan x="150" y="240">Phase</tspan> <tspan x="150" y="260">(1)</tspan></text></a>

      <path id="capture_phase_arrow" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            d="M235,28 C195,25 195,75 238,85 "/>
      <use xlink:href="#capture_phase_arrow" x="5" y="70" />
      <use xlink:href="#capture_phase_arrow" x="10" y="140" />
      <use xlink:href="#capture_phase_arrow" x="10" y="210" />
      <use xlink:href="#capture_phase_arrow" x="10" y="280" />
      <path id="capture_phase_arrow2" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            d="M245,378 C205,375 205,473 428,458 "/>
      <path id="capture_phase_arrow3" fill="none" stroke="red" stroke-width="3" marker-end="url(#redArrow)" stroke-linecap="round"
            stroke-dasharray="none" d="M428,473 C330,470 330,533 363,548 "/>

    </g>
    
    <g id="target_phase">
      <a xlink:href="../DOM3-Events.html#glossary-target-phase" target="_parent"><text fill="blue" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="337" y="580">Target</tspan> <tspan x="337" y="600">Phase</tspan> <tspan x="337" y="620">(2)</tspan></text></a>
      
      <rect x="-50" y="0" width="100" height="40" rx="5" ry="5" fill="none" stroke="black" stroke-width="5" stroke-dasharray="none" 
            transform="translate(430, 540)"/>
    </g>
    
    <g id="bubble_phase">
      <a xlink:href="../DOM3-Events.html#glossary-bubbling-phase" target="_parent"><text fill="green" font-family="Verdana, sans-serif" font-size="20" font-weight="bold" text-anchor="middle"><tspan x="490" y="320">Bubbling</tspan> <tspan x="490" y="340">Phase</tspan> <tspan x="490" y="360">(3)</tspan></text></a>

      <path id="bubble_phase_arrow3" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            stroke-dasharray="none" d="M492,548 C630,483 630,470 562,473"/>
      <path id="bubble_phase_arrow2" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M565,457 C605,447 605,398 377,388"/>
      <path id="bubble_phase_arrow" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M375,375 C415,372 415,332 375,322"/>
      <use xlink:href="#bubble_phase_arrow" x="0" y="-70" />
      <use xlink:href="#bubble_phase_arrow" x="0" y="-140" />
      <path id="bubble_phase_arrow4" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M375,165 C425,162 425,122 385,112"/>
      <path id="bubble_phase_arrow" fill="none" stroke="green" stroke-width="3" marker-end="url(#greenArrow)" stroke-linecap="round"
            d="M385,95 C435,92 435,52 395,42"/>
    </g>
  </g>
  
</svg>
```

