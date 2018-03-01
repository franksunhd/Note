## jQuery中的CSS操作(CSS/尺寸/位置/数据)

[TOC]

### 1.CSS

#### .addClass()  添加样式

- 为每个匹配的元素添加指定的样式类名
- 参数:类名/匿名函数

```javascript
$("#box1 p").eq(0).addClass("s1");
$("#box p").eq(0).addClass("s1 s2 s4")
// 参数是匿名函数
$("#box1 p").addClass(function(index,className) {
    // console.log(1);
    console.log(index,className);
    if (index === 0) return "s1";
    if (index === 1) return "s2";
    if (index === 2) return "s3";
});
```

#### .removeClass()     移除样式

- 移除集合中每个匹配元素上一个，多个或全部样式。

#### .toggleClass()       有类就添加,没有就删除

- 为匹配的元素集合中的每个元素上添加或删除一个或多个样式类（class）
- 取决于这个样式类（class）是否存在或state参数的值。
- 有类就删除，没有就添加

```javascript
//  参数2:控制删除(false) 或者 添加(true) Class
$("#box p:last-child").toggleClass("s1 s2",true);
```

#### .css()    设置属性 或 获取属性值

- **获取**匹配元素集合中的**第一个**元素的样式属性的计算值	或	**设置**每个匹配元素的一个或多个CSS属性

```javascript
	/*
     $(".one").css("width", "500px");
     $(".one").css("height", "500px");
     $(".one").css("background", "pink");
	*/
    /*
    //一次性设置多个
    $(".one").css({
      "width": "500px",
      "height": "500px",
      "background": "pink"
    });
    */

    //使用addClass来添加样式最方便
    $(".one").addClass("back color_red");

    //使用removeClass来移除样式
    $(".one").removeClass("color_red back");

    //有类就删除，没有就添加
    $(".one").toggleClass("back");

    //获取样式
    console.log($(".one").css("width"));//获取width
    console.log($(".one").css("height"));//获取height
    console.log($(".one").css("background-color"));

    //返回一个包含指定属性的对象
    console.log($(".one").css(["width", "height", "background-color"]));

/**************************/
<div id="box">
    <p>p1</p>
    <p>p2</p>
</div>
<script src="./js/jquery.min.js" charset="utf-8"></script>
<script type="text/javascript">
    $("#box p").css("color","red").css("font-size","30px");

    // 获取
    var value = $("#box p").css("width");  // 包含单位

    // html() 内容相关 可以包含 html 标签
    $("#box p").eq(0).html("w:" + value);

    // 参数对象
    $("#box p:eq(1)").css({
        // 注意驼峰命名,数字单位可以省略
        textDecoration:"line-through",
        color:"pink"
    });

    // 回调函数
    $("#box p").css("background-color",function(index) {

        if(index === 0) return "yellow";
        if(index === 1) return "blue";
    });

    $("#box p").css({
        width:function(index,value) {
            return parseFloat(value) - 100;
        },
        height:function(index,value) {
            return parseFloat(value) + 100;
        }
    });

    // text() 内容相关 不包含 html 标签

    // val() 表单内容相关
```

### 2.jQuery的链式调用 ! ! !

- 链式调用实现：jQuery中的方法每次都返回选择的符合条件的jQuery对象本身。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>jQuery的链式调用！！！！！</title>
    <style>
      .back {
        width: 200px;
        height: 200px;
        background: pink;
      }
    </style>
  </head>
  <body>

    <div class="one">111</div>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">
/*
	console.log($(".one"));
    console.log($(".one").addClass("back"));
    console.log($(".one").css("color", "red"));
    console.log($(".one").css(["width", "height", "background-color"]));
*/
    //等价于以上代码	链式调用
  console.log($(".one").addClass("back").css("color","red").css(["width", "height", "background-color"]));
    </script>
  </body>
</html>
```

### 3.属性

#### 1. val() 获取表单元素的值/ 设置表单元素的值

- 获取匹配的元素集合中第一个元素的当前值或设置匹配的元素集合中每个元素的值。
- val()　获取值
- val(value)设置值


```javascript
// 从复选框获取选中值
$("input[type=checkbox][name=bar]:checked" ).val();
```

```javascript
//设置文本框的值
$("input").val(text);
```

#### 2.attr() 获取行间属性 / 设置行间属性

- 参数1:属性名
- 参数2:属性值/匿名函数的返回值作为属性值

```javascript
// 获取属性
var ar = $("#box").attr("id");
console.log(ar);

// 设置
$("#box").attr("age","18");

// 参数对象,设置多个属性
$("#box").attr({
    name:"lisi",
    sex:"nv",
    src:"地址",
    alt:"提示"
});

// 回调函数
$("#box").attr("src","地址");
$("#box").attr("src",function(index,oldValue) {
    console.log(index,oldValue);  // 0 "地址"
    return "新的地址";
});
```

#### 3.removeAttr()  移除行间属性

```javascript
// 移除 一个或者多个
$("#box").removeAttr("age sex");
```

```javascript
$("#box").test = "测试";
console.log($("#box").test);  // undefined

var obj = $("#box");
obj.test = "测试1";
console.log(obj.test);  // 测试1
// 验证: $("#box") 每次执行都会 new 一个新的一模一样的对象返回
console.log($("#box") === $("#box"));  // false
```

#### 4.prop()  类似原生点语法自定属性,行间不可见

```javascript
// 设置
$("#box2").prop("age","18");

// 获取
var age = $("#box2").prop("age");
console.log(age,box2.age);  // 18 18

// 原生对象只有一份,多个 JQ 对象共享一个原生对象
// 两个 $("#box2") JQ 对象不同,但是原生对象只有一份
$("#box2")[0].test = "测试3";
console.log($("#box2")[0].test);  // 测试3
```

### 4.尺寸

#### height() 

#### width() 宽高没有单位

```javascript
<div id="box">
    <p>p1</p>
    <p>p2</p>
    <p>p3</p>
</div>
$("#box p").height(100).width(100).css("background-color","pink");
```

#### innerHeight()

#### innerWidth()  内尺寸,不包含边框

```javascript
<div id="box">
    <p>p1</p>
    <p>p2</p>
    <p>p3</p>
</div>
var value1 = $("#box p").eq(0).innerHeight();
console.log(value1);
$("#box p").eq(0).text("innerHeight(contain+padding):" + value1 + "px");
```

#### outerWidth()

#### outerHeight()  外尺寸 ,包含边框,默认不包含 margin,参数1给 true 包含 margin

```javascript
var outerW = $("#box p").outerWidth();
console.log("外尺寸:" + outerW);  // 160  // border + padding

var outerW1 = $("#box p").outerWidth(true);
console.log("外尺寸:" + outerW1);  // 190  // border + padding + margin
```

### 5.位置

#### offset()

```javascript
<style media="screen">
    #box {
        position: relative;
    }

    #box a {
        position: absolute;
        left: 10px;
        top: 10px;
    }
</style>
<div id="box">
    <a href="#">子元素</a>
</div>
$("#box").css({
    border:"5px solid red",
    height:"200px",
    width:"200px"
});

// offset:获取到页面顶部(左)的距离
var offsetBox = $("#box").offset();
console.log(offsetBox);  // object对象 包含 left = 8和 top = 8
console.log(offsetBox.top,offsetBox.left);  // 8 8

var offsetA = $("#box a").offset();
// offset 与父元素的定位没有关系,永远都是相对于文档的距离
console.log(offsetA);  // object对象 包含 left = 23 和 top = 23
console.log(offsetA.top,offsetA.left); // 23 23
```

#### position()

```javascript
// position() 获取相对于父元素的偏移,只能获取,不能设置
var pos = $("#box a").position();
console.log(pos);  // object 对象
console.log(pos.left,pos.top); // 10 10
```

#### scrollTop()

#### scrollLeft()

```javascript
// 获取
var sTop = $(document.body).scrollTop();
console.log(sTop);
var sTop1 = $(document.documentElement).scrollTop();
console.log(sTop);


// 设置
$("body,html").scrollTop(0);

// 动画方式设置 回到顶部
$("body,html").animate({
    scrollTop:0
},1000);
```

## 补充内容

### 全选和反选

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>全选和反选</title>
</head>
<body>
	<div id="box">
		<input id="btn1" type="button" name="btn1" value="全选">
		<input id="btn2" type="button" name="btn2" value="反选">
	</div>

	<ul id="list">
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
		<li><input type="checkbox"></li>
	</ul>
	<script src="./js/jquery.min.js" charset="utf-8"></script>
	<script type="text/javascript">
		// 全选
		$("#btn1").click(function() {
			$("#list > li > input").prop("checked",true);
		});

		// 反选
		$("#btn2").click(function() {
			// $("#list li input").get().forEach()
			$("#list li input").each(function(index,value) {
				this.checked = !this.checked;
			});
		});
	</script>
</body>
</html>
```

```javascript
// 全选
$("#btn1").click(function() {
    $("#list > li > input").prop("checked",true);
});

// 反选
$("#btn2").click(function() {
    $("#list > li > input").prop("checked",function(index,old) {
        return !old;
    });
});
```

