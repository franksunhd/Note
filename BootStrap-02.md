## BootStrap组件/字体图标

[TOC]

### 1.Glyphicons 字体图标(bootStrap内置)

#### 所有可用的图标

- 包括250多个来自 Glyphicon Halflings 的字体图标。[Glyphicons](http://glyphicons.com/) Halflings 一般是收费的，但是他们的作者允许 Bootstrap 免费使用。为了表示感谢，希望你在使用时尽量为 [Glyphicons](http://glyphicons.com/) 添加一个友情链接。
- [图标列表](http://v3.bootcss.com/components/#glyphicons)

#### 如何使用

- 出于性能的考虑，所有图标都需要一个基类和对应每个图标的类。把下面的代码放在任何地方都可以正常使用。注意，为了设置正确的内补（padding），务必在图标和文本之间添加一个空格。



```html
<!-- 
	Bootstrap
	引用外部样式表
-->
<link href="bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">

<!--bootstrap内置字体图标  -->
  <span class="glyphicon glyphicon-apple"></span>
  <div class="glyphicon glyphicon-education"></div>
```

### 2.font awesome图标字体库

[font awesome 官网链接](http://fontawesome.dashgame.com/)

#### 如何使用

##### 方法一

- 将以下代码粘贴到网页HTML代码的 `<head>` 部分.

```html
<link href="//netdna.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">
```

##### 方法二

- 官网下载`font-awesome`文件夹
- 复制整个 `font-awesome` 文件夹到您的项目中。
- 在HTML的 `<head>` 中引用font-awesome.min.css。                

```html
<link rel="stylesheet" href="path/to/font-awesome/css/font-awesome.min.css">
```

#### 基本图标

- 可以将Font Awesome图标使用在几乎任何地方，只需要使用CSS前缀 `fa` ，再加上图标名称。Font Awesome是为使用内联元素而设计的。我们通常更喜欢使用 `<i>` ，因为它更简洁。但实际上使用 `<span>` 才能更加语义化。            

```html
<i class="fa fa-camera-retro"></i> fa-camera-retro
```

- 如果您修改了图标容器的字体大小，图标大小会随之改变。同样的变化也会发生在颜色、阴影等其它任何CSS支持的效果上。

#### 大图标

- 使用 `fa-lg` (33%递增)、`fa-2x`、 `fa-3x`、`fa-4x`，或者 `fa-5x` 类 来放大图标。

```html
<i class="fa fa-camera-retro fa-lg"></i> fa-lg
<i class="fa fa-camera-retro fa-2x"></i> fa-2x
<i class="fa fa-camera-retro fa-3x"></i> fa-3x
<i class="fa fa-camera-retro fa-4x"></i> fa-4x
<i class="fa fa-camera-retro fa-5x"></i> fa-5x
```

- 如果图标的底部和顶部被截断了，您需要增加行高来解决此问题。

### 3.iconfont阿里图标库

[iconfont 官网链接](http://www.iconfont.cn/)

#### 如何使用

##### font-class引用

> font-class是unicode使用方式的一种变种，主要是解决unicode书写不直观，语意不明确的问题。

> 与unicode使用方式相比，具有如下特点：

- 兼容性良好，支持ie8+，及所有现代浏览器。

- 相比于unicode语意明确，书写更直观。可以很容易分辨这个icon是什么。
- 因为使用class来定义图标，所以当要替换图标时，只需要修改class里面的unicode引用。
- 不过因为本质上还是使用的字体，所以多色图标还是不支持的。

**使用步骤如下：**

第一步：引入项目下面生成的fontclass代码：

```html
<link rel="stylesheet" type="text/css" href="./iconfont.css">
```

第二步：挑选相应图标并获取类名，应用于页面：

```html
<i class="iconfont icon-xxx"></i>
```

> "iconfont"是你项目下的font-family。可以通过编辑项目查看，默认是"iconfont"。

##### symbol引用

> 这是一种全新的使用方式，应该说这才是未来的主流，也是平台目前推荐的用法.这种用法其实是做了一个svg的集合，与另两种相比具有如下特点：

- 支持**多色图标**了，不再受单色限制。
- 通过一些技巧，支持像字体那样，通过`font-size`,`color`来调整样式。
- 兼容性较差，支持 ie9+,及现代浏览器。
- 浏览器渲染svg的性能一般，还不如png。

**使用步骤如下：**

第一步：引入项目下面生成的symbol代码：

```html
<script src="./iconfont.js"></script>
```

第二步：加入通用css代码（引入一次就行）：

```html
<style type="text/css">
.icon {
   width: 1em; height: 1em;
   vertical-align: -0.15em;
   fill: currentColor;
   overflow: hidden;
}
</style>
```

第三步：挑选相应图标并获取类名，应用于页面：

```html
<svg class="icon" aria-hidden="true">
  <use xlink:href="#icon-xxx"></use>
</svg>
```

##### unicode引用

> unicode是字体在网页端最原始的应用方式，特点是：

- 兼容性最好，支持ie6+，及所有现代浏览器。
- 支持按字体的方式去动态调整图标大小，颜色等等。
- 但是因为是字体，所以不支持多色。只能使用平台里单色的图标，就算项目里有多色图标也会自动去色。

> 注意：新版iconfont支持多色图标，这些多色图标在unicode模式下将不能使用，如果有需求建议使用symbol的引用方式

**unicode使用步骤如下：**

第一步：拷贝项目下面生成的font-face

```
@font-face {
  font-family: 'iconfont';
  src: url('iconfont.eot');
  src: url('iconfont.eot?#iefix') format('embedded-opentype'),
  url('iconfont.woff') format('woff'),
  url('iconfont.ttf') format('truetype'),
  url('iconfont.svg#iconfont') format('svg');
}

```

第二步：定义使用iconfont的样式

```
.iconfont{
  font-family:"iconfont" !important;
  font-size:16px;font-style:normal;
  -webkit-font-smoothing: antialiased;
  -webkit-text-stroke-width: 0.2px;
  -moz-osx-font-smoothing: grayscale;
}

```

第三步：挑选相应图标并获取字体编码，应用于页面

```
<i class="iconfont">&#x33;</i>
```

> "iconfont"是你项目下的font-family。可以通过编辑项目查看，默认是"iconfont"。

#### 缺点

- 它只能根据具体需求下载图标
- 当需要的图标没有下载时，需要重新下载，并且新的库文件需要覆盖原文件







