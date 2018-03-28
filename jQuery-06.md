## jQuery中的效果

[TOC]

### 1.显示和隐藏

#### .hide()方法

- 隐藏匹配的元素

```javascript
$("#box button").eq(1).click(function() {
    $("#box1").hide(2000,"linear",function() {
        // 回调函数,执行完隐藏之后回调
        $(this).text("隐藏完成");
    });
});
```

#### .show()方法

- 显示匹配的元素
- 适合于display=none;的显示  不适用于visibility=hidden;的显示,

```javascript
$("#box button").eq(0).click(function() {
    $("#box1").show("slow",function() {
        $(this).text("显示完成");
    });
});
```

#### .toggle()方法

- 显示或隐藏匹配的元素，如果元素是最初显示，它会被隐藏，如果隐藏的，它会显示出来。

```javascript
$("#box button").eq(2).click(function() {
    $("#box1").toggle("slow");
});
```

### 2.渐变(淡入/淡出)

#### .fadeIn()方法

- 通过淡入的方式显示匹配元素.

```javascript
$("#box button").eq(6).click(function() {
    $("#box1").fadeIn();
});
```

#### fadeOut()方法

- 通过淡出的方式隐藏匹配元素。

```javascript
$(".ig").eq(i).fadeIn(600).siblings().fadeOut(600);
//0.6秒的淡入和淡出

$("#box button").eq(7).click(function() {
    $("#box1").fadeOut();
});
```

#### fadeTo() 第二个参数是透明度 

```javascript
$("#box button").eq(8).click(function() {
    $("#box1").fadeTo("slow",0.5);
});
```

#### fadeToggle()

```javascript
$("#box button").eq(9).click(function() {
    $("#box1").fadeToggle();
});
```

### 3.滑动

#### .slideDown()方法

- 用滑动动画显示一个匹配元素。

```javascript
$("#box button").eq(3).click(function() {
    $("#box1").slideDown();
});
```

#### .slideUp()方法

- 用滑动动画隐藏一个匹配元素。

```javascript
//上拉隐藏
 $(".search-lists").slideUp(100);

$("#box button").eq(4).click(function() {
    $("#box1").slideUp();
});
```

#### .slideToggle()方法

- 用滑动动画显示或隐藏一个匹配元素。如果元素是最初显示，它会被隐藏，如果隐藏的，它会显示出来。

```javascript
$("p").slideToggle("slow");

$("#box button").eq(5).click(function() {
    $("#box1").slideToggle();
});
```

### 4.自定义

#### animate()

```javascript
$("#box button").eq(10).click(function() {
    $("#box1").animate({
        width: "+=250",
        height: "200px",
        fontSize: "30px",
        // css3的设置,不支持
        transform:"translateY(50px)",
        // 背景色不支持
        backgroundColor: "yellow"
    },2000,"linear",function() {
        $(this).text("动画完成");
    });
});
```

#### stop()

```javascript
$("#box button").eq(12).click(function() {
    // 不传参:停止正在执行的动画
    // 参数1: 清空动画队列,停止的当前运行位置
    // 参数2: 和 finish 道理一样
    $("#box1").stop(true);
});
```

#### finish()

```javascript
$("#box button").eq(13).click(function() {
    // 停止动画,回到队列中的最后在一个位置
    $("#box1").finish();
});
```

#### delay()

```javascript
$("#box button").eq(14).click(function() {
    $("#box1").hide().delay(800).slideDown(300).delay(1000).fadeOut(400);
    $("#box1").text("延时1s");
});
```

### 5.设置 (jQuery.fx.off)

```javascript
// 关闭文件中的所有动画
jQuery.fx.off = true;
```

