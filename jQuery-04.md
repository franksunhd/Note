## jQuery中的事件操作

[TOC]

### 鼠标事件

#### 1.click()	鼠标单击事件

- 为 JavaScript 的"click" 事件绑定一个处理器，或者触发元素上的 "click" 事件。
- click是添加单击事件的方法
- 匿名函数就是没有名字

```javascript
function handlerClick(){
      console.log("单击。。。。");
    }

    //函数作为参数时，通常称该函数为回调函数(在将来的某个时刻会被执行)
    
	/*
    click内部的函数作为回调函数使用，又称为事件处理函数
    此处只是注册了一个事件处理函数，并没有执行该函数。
    */
	
    /*
    事件可以添加多个处理函数。
    当触发事件的时候，处理函数的执行顺序是按照注册顺序来的
    */
    $(".one").click(function(){
      $(".one").css("background-color", "red");
    });

    $(".one").click(handlerClick);		//执行事件处理函数

    console.log("事件处理");
```

```javascript
<div class="btn">
      <button>添加</button>
      <button>删除</button>
</div>

<ul id="lists"></ul>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">

    var add = $(".btn button").eq(0);
    var del = $(".btn button").eq(1);
	
	//点击一次添加按钮，无序列表添加一行
    add.click(function(){
      $("<li>li元素</li>").appendTo("#lists");
    });
	
	//点击一次删除按钮，无序列表从尾部删除一行
    del.click(function(){
      $("#lists li:last").remove();
    });
    </script>
```

#### 2. dblclick() 鼠标双击事件

- 为JavaScript 的 "dblclick" 事件绑定一个处理函数，或者触发元素上的 "dblclick" 事件。
- 双击时会先触发单击！！！！！

```JavaScript
<div class="one"></div>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">

    $(".one").click(function(){
      console.log("单击。。。");
    });

    /*
    双击时会先触发单击！！！！！
    */
	//鼠标双击更改div的大小，背景颜色
    $(".one").dblclick(function(){
      console.log("双击。。。");
      $(".one").css({
        "width":"500px",
        "height": "500px",
        "background-color":"yellow"
      });
    });
</script>
```

#### 4.contextmenu() 鼠标右击事件

- 为 JavaScript 的"contextmenu" 事件绑定一个处理器，或者触发元素上的 "contextmenu" 事件。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">

    //doucment是整个页面
    $(document).contextmenu(function(){
      console.log("鼠标右键单击。。。。");
    });
    </script>
  </body>
</html>
```

#### 5.鼠标悬停事件mouseover()/鼠标离开事件mouseout()

```javascript
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <style>
    .one {
      width: 100px;
      height: 100px;
      background: red;
    }
    </style>
  </head>
  <body>
    <div class="one"></div>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">

    /*
    //鼠标悬停的事件
    $(".one").mouseover(function(){
      $(".one").css("background-color", "blue");
    });

    //鼠标离开的事件
    $(".one").mouseout(function(){
      $(".one").css("background-color", "red");
    });
    */
      
	//链式调用
    $(".one").mouseover(function(){
      $(".one").css("background-color", "blue");
    }).mouseout(function(){
      $(".one").css("background-color", "red");
    });

    </script>
  </body>
</html>
```

#### 6.hover()

- 将二个事件函数绑定到匹配元素上，分别当鼠标指针进入和离开元素时被执行。

```javascript
	<div class="one"></div>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">
	
    /*
    hover相当于 mouseout mouseover合体
    根据实际需求传入处理函数,可以使用null代替空函数
    */
    $(".one").hover(function(){
      $(".one").css("background-color", "blue");
    }, function(){
      $(".one").css("background-color", "red");
    });


    </script>
```

### 键盘事件

#### 1.按下事件keydown()

- keysdown()识别所有按键

#### 2.按下事件keypress()

- keypress() 识别字母数字键

#### 3.抬起事件keyup()

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">

    // keydown识别所有的
    $(document).keydown(function(){
      console.log("按下了");
    });

    /*
    keypress识别 字母数字键
    */
    /*
    $(document).keypress(function(){
      console.log("按下了");
    });
    */

    $(document).keyup(function(e){
      console.log("弹起了： "  + e.which);
    });
    </script>

  </body>
</html>
```

### 事件绑定 on()方法

#### on()方法

- 使用on方法进行事件绑定,通用的事件绑定方法
- on方法可以自定义事件
- on方法也可以绑定多个事件处理函数

#### trigger()方法～触发自定义的事件

- trigger触发自定义的事件
- 根据绑定到匹配元素的给定的事件类型执行所有的处理程序和行为。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>使用on方法进行事件绑定,通用的事件绑定方法</title>
      <style>
      #divId {
        width: 200px;
        height: 100px;
        background: blue;
      }
    </style>
  </head>
  <body>

    <button id="btn">按钮</button>
    <button id="btn2">单击改变div的背景色</button>
    
    <div id="divId"></div>

    <script src="../jquery.min.js"></script>
    <script type="text/javascript">
      
    /*
     $("#btn").click(function(){....});
    */
      
    //on方法也可以绑定多个事件处理函数
    $("#btn").on('click', function () {
      console.log("click 1....");
    }).on('click', function(){
      console.log("click 2....");
    });

    $("#btn").on('dblclick', function () {
      console.log("dbclick 1....");
    });

    /***************自定义事件的注册和触发*******************/

    //注册自定义的事件		改变div背景颜色
    $("#divId").on("changeColor", function(){
      $("#divId").css("background-color", "red");
    });			
    //这里只是注册，没有使用

    //btn2单击时，trigger触发changeColor事件
    $("#btn2").on('click', function(){
    //trigger触发自定义的事件
      $("#divId").trigger("changeColor");
    });
      
    </script>
  </body>
</html>
```

### 解除事件绑定 off()方法

#### off()方法

- 移除一个事件处理函数。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>off解除事件绑定</title>
  </head>
  <body>

    <button id="btn">按钮</button>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">
	
    //定义事件处理函数
    function handlerOne(){
      console.log("触发单击 1...");
    }
	
    //绑定定义的事件处理函数
    $("#btn").on('click', handlerOne);
	
    //绑定匿名函数
    $("#btn").on('click', function(){
      console.log("触发单击 2 ...");

    //使用off解除绑定的事件处理函数
    //只填写 事件名称，会将该事件上的所有处理函数全都解除绑定了
    // $("#btn").off('click');
    //移除指定处理函数
    $("#btn").off('click', handlerOne);
    });

   $("#btn").dblclick(function(){
     console.log("触发双击。。。。。");
     //off没有参数，那么移除该元素上的所有事件的所有函数
     $("#btn").off();
   });
    </script>
  </body>
</html>
```

### 表单事件

#### .focus() 获得焦点

``` javascript
$(".message input").focus(function(){
     $(".message p").css("visibility", "hidden");
   });
```

### 事件对象

#### e.pageX

- 鼠标相对于文档的左边缘的位置（左边）。 

#### e.pageY

- 鼠标相对于文档的顶部边缘的位置（顶部）

#### e.preventDafault()

- 如果调用这个方法，默认事件行为将不再触发。

#### e.stopPropagetion()

- 不触发任何前辈元素上的事件处理函数。

```javascript
$(document).contextmenu(function(e){
      //获得鼠标坐标
      var x = e.pageX;
      var y = e.pageY;

      //去掉浏览器的默认右键
      e.preventDefault();
      e.stopPropagation();

     //显示菜单
     /*
     菜单的边界问题，需要解决？？？？？
     */
     $("#menu").css({
       "display":"block",
       "top": y + "px",
       "left": x + "px"
     });
```

#### e.which()

- 针对键盘和鼠标事件，这个属性能确定你到底按的是哪个键。 

```javascript
//控制台打印抬起的是哪个键
$(document).keyup(function(e){
      console.log("弹起了："  + e.which);
    });
```

