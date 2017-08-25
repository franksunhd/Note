## jQuery中的CSS操作(CSS/尺寸/位置/数据)

[TOC]

### 1.CSS

#### .addClass()	添加样式

- 为每个匹配的元素添加指定的样式类名

#### .removeClass()     移除样式

- 移除集合中每个匹配元素上一个，多个或全部样式。

#### .toggleClass()       有类就添加,没有就删除

- 为匹配的元素集合中的每个元素上添加或删除一个或多个样式类（class）
- 取决于这个样式类（class）是否存在或state参数的值。
- 有类就删除，没有就添加

#### .css()    设置属性 或 获取属性值

- **获取**匹配元素集合中的**第一个**元素的样式属性的计算值	或	**设置**每个匹配元素的一个或多个CSS属性

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>css操作</title>
    <style>
      .back{
        width: 500px;
        height: 500px;
        background: pink;
      }

      .color_red {
        color: red;
      }
    </style>
  </head>
  <body>

    <div class="one">hjjhdjhkjhk</div>
    <div class="one">hjjhdjhkjhk</div>
    <div class="one">hjjhdjhkjhk</div>

    <script src="../jquery.min.js" charset="utf-8"></script>
    <script type="text/javascript">
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
    </script>

  </body>
</html>
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

### 属性

#### 1. .val() 获取表单元素的值

- 获取匹配的元素集合中第一个元素的当前值或设置匹配的元素集合中每个元素的值。


- val()　获取值
- .val(value)设置值

```html
// 从复选框获取选中值
$( "input[type=checkbox][name=bar]:checked" ).val();
```

```html
//设置文本框的值
$("input").val(text);
```

### 