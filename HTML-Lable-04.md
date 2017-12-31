## HTML5 新增特性/智能表单

[TOC]

### 1.什么是HTML5

- HTML5是HTML的超集，不仅仅是HTML，更多的是JavaScript API和CSS的提升。
- 万维网的核心语言、标准通用标记语言下的一个应用超文本标记语言（HTML）的第五次重大修改。

### 2.什么是HTML

- 超文本：文本 图片 视频 音频
- 国际通用置标语言的子集 
- XHTML也是国际通用置标语言的子集 

### 3.HTML5包含什么？

- HTML
- 音频流和视频流的解析
- 语义化的标签(对搜索引擎友好)
- 地址定位

### 4.设计目的

- HTML5的设计目的是为了在移动设备上支持多媒体。新的语法特征被引进以支持这一点，如video、audio和canvas 标记。HTML5还引进了新的功能，可以真正改变用户与文档的交互方式。


### 5.发展趋势

- HTML5规范开发完成时，将成为主流。
- 据统计2013年全球将有10亿手机浏览器支持HTML5，同时HTML Web开发者数量将达到200万。毫无疑问，HTML5将成为未来5-10年内，移动互联网领域的主宰者。

### 6.应用场景

- 网页应用程序
  - PC端：iCloud、百度脑图、Office 365···
  - APP端：淘宝、京东、美团···
  - WeChat端：淘宝、京东、美团··· 
- 本地应用
  - PC端：网易云音乐、有道词典···
  - APP端：淘宝、京东、美团···
- 简单的游戏
  - html5版切水果、五子棋、太空战争游戏

### 7.智能表单

#### form表单

```html
	<!-- novalidate控制是否进行数据校验，默认是开启的 -->
    <!-- autocomplete决定了 是否开启自动完成的功能  -->
    <form action="#" method="get" autocomplete="off">
      正则表达式校验:<input id="text" type="text" pattern="\d"> <br><br>
      <!-- pattern是正则表达式，可以用于进行校验  -->
      email: <input type="email" name="email" placeholder="请输入邮箱" list="emails"><br>

      <!-- datalist用于给input提供预定义的选项
        list的属性值必须为datalist的id
     -->
      <datalist id="emails">
        <option >xxx@yyy.com</option>
        <option >yyy@zzz.com</option>
        <option >zzz@aaa.com</option>
      </datalist>
      <br>
      <!-- required 属于bool 属性 直接写名字就行 -->
      url: <input type="url" name="url" required="true"> <br> <br>

      number: <input type="number" name="number" min="20" max="100" step="2"> <br> <br>

      range: <input type="range" name="range" value="0" min="0" max="100" step="10"> <br> <br>

      <!-- autofocus 自动获得焦点 -->
      search: <input type="search" name="search" autofocus required> <br><br>

      <!-- 日期具有兼容性问题，尽量少用  -->
      date: <input type="date"> <br><br>
      month: <input type="month"> <br> <br>
      week: <input type="week"> <br> <br>
      time: <input type="time"> <br> <br>

      <!-- multiple 是文件多选 -->
      <input type="file" name="files" multiple> <br><br>

      <!-- 提交按钮 -->
      <input type="submit" name="" value="提交">
    </form>
```

#### 文本相关标签

```html
<header> ... </header>
<section> 
  <nav> ... </nav>
  <section>
    <article>...</article>
  </section>
</section>
<footer> ... </footer>
```

#### 多媒体标签

##### audio 音频

- controls 控制面板
- loop 循环播放
- autoplay 自动播放

```html
<!--
      controls 控制面板
      loop 循环播放
      autoplay 自动播放
    -->
    <audio controls loop autoplay>
      <source src="./video/music1.ogg" >
      <source src="./video/12306.wav" >
      <source src="./video/music1.mp3">
    </audio>
```

##### video 视频

- controls 控制面板
- loop 循环播放
- autoplay 自动播放
- poster 指定视频封面

```html
<!--
      poster 属性用于给视频指定封面
     -->
     <video id="video-1" width="600" height="300" controls poster="./video/mi.jpg">
        <source src="./video/chrome.ogv">
        <source src="./video/fun.mp4">
     </video>

     <script type="text/javascript">
       var v = document.getElementById("video-1");
       console.log(v.duration);  //NaN

       //loadedmetadata, 事件在元信息加载完毕之后触发
       v.addEventListener('loadedmetadata', function(){
         console.log("视频元信息加载完毕！");
         console.log("视频总长为 %ds！", v.duration);  // 视频总长为...s

       },false);
     </script>
```

### 8.自定义属性

```html
<div id="item" name="name" data-name="lisi" data-age="23" data-gender="male" data-score="90" data-abc-ef="abc-ef"></div>
    <script type="text/javascript">
      var Obox = document.querySelector("#item");
      var box = document.getElementById("item");

      box.setAttribute("name","huahua");
      box.setAttribute("title","titles");

      console.log(box.getAttribute("title"));
      console.log(box.getAttribute("name"));

      console.log(Obox.dataset);
      console.log(Obox.dataset.name);
      console.log(Obox.dataset.age);
      console.log(Obox.dataset.gender);
      console.log(Obox.dataset.score);
      console.log(Obox.dataset.abcEf);

      Obox.dataset.name = "ssy";
      Obox.dataset.ade = "21";
    </script>
```

### 9.JS新增选择器

- querySelector

```javascript
var f = document.querySelector("input[type=file]");
```

### 10.文件列表

```html
<input type="file" multiple>
    <table id="show">
      <caption><h2>文件信息</h2></caption>
      <thead>
        <tr>
          <th>文件名称</th>
          <th>文件大小</th>
          <th>文件最后修改时间</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>

    <script type="text/javascript">
      var f = document.querySelector("input[type=file]");
      var tb = document.querySelector('#show tbody');

      f.addEventListener('change',function() {
        console.log(f.files);

        for (let i = 0; i < f.files.length; i++) {
          console.log(f.files[i].name);

          var tr = document.createElement('tr');
          tr.innerHTML = "<td>" + f.files[i].name + "</td><td>"
          + (f.files[i].size/1024).toFixed(2) + " KB</td><td>"
          + f.files[i].lastModifiedDate.toLocaleString()
          + "</td>";
          tb.appendChild(tr);
        }
      },false)
    </script>
```

### 11. 全屏API

```javascript
<video id="video" poster="./video/mi.jpg" controls>
      <source src="./video/fun.mp4" >
    </video>
    <br>
    <button id="btn" type="button" name="button">视频全屏</button>

    <div id="box">我要全屏</div>

    <script src="./code.js" charset="utf-8"></script>
    <script type="text/javascript">
      var box = document.getElementById('box');
      var v =document.getElementById('video');
      var btn = document.getElementById('btn');
      var flag = 0; // 默认正常

	  //全屏方法
      function fullScreen(elem){
        if (elem.requestFullscreen){
          elem.requestFullscreen();
        } else if (elem.mozRequestFullScreen){
          elem.mozRequestFullScreen();
        } else if (elem.webkitRequestFullscreen){
          elem.webkitRequestFullscreen();
          // elem.style.width = "100%";
          // elem.style.height = "100%";
        }

      }

      //取消全屏
      function cancelFullScreen(){
        if (document.cancelFullScreen){
          document.cancelFullScreen();
        } else if (document.mozCancelFullScreen){
          document.mozCancelFullScreen();
        } else if (document.webkitCancelFullScreen){
        document.webkitCancelFullScreen();
        }
      }

      btn.onclick = function() {
        fullScreen(v);
      }

      box.ondblclick = function() {
        if (flag == 0) {
          fullScreen(box); //
          flag = 1;
        }
        else {
          cancelFullScreen(box);
          flag = 0;
        }
      }
</script>
```



























