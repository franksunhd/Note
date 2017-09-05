## jQuery中的效果

### 1.显示和隐藏

#### .hide()方法

- 隐藏匹配的元素

```javascript
$('.target').hide();
```

### .show()方法

- 显示匹配的元素
- 适合于display=none;的显示  不适用于visibility=hidden;的显示,

```javascript
$('.target').show();
```

### .toggle()方法

- 显示或隐藏匹配的元素，如果元素是最初显示，它会被隐藏，如果隐藏的，它会显示出来。

```javascript
$('.target').toggle();
```

### 2.渐变

#### .fadeIn()方法

- 通过淡入的方式显示匹配元素。

#### fadeOut()方法

- 通过淡出的方式隐藏匹配元素。

```javascript
$(".ig").eq(i).fadeIn(600).siblings().fadeOut(600);
//0.6秒的淡入和淡出
```

### 3.滑动

#### .slideDown()方法

- 用滑动动画显示一个匹配元素。

```javascript
//下拉显示
 $(".search-lists").slideDown(100);
```

#### .slideUp()方法

- 用滑动动画隐藏一个匹配元素。

```javascript
//上拉隐藏
 $(".search-lists").slideUp(100);
```

#### .slideToggle()方法

- 用滑动动画显示或隐藏一个匹配元素。如果元素是最初显示，它会被隐藏，如果隐藏的，它会显示出来。

```javascript
$("p").slideToggle("slow");
```

