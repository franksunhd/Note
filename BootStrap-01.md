## BootStrap/栅格系统/全局CSS样式

[TOC]

###### 

## 起步

### 1.什么是BootStrap?

- BootStrap是一个**基于HTML, CSS, JavaScript技术**的快速开发响应式布局，移动设备优先的前端框架.
- BootStrap简洁、直观、强悍的前端开发框架，让web开发更迅速、简单。
- BootStrap是由Twitter的Mark Otto和Jacob Thomton开发的. BootStrap是2011年八月在GitHub上发布的开源产品.

### 2.为什么使用BootStrap

- 移动设备优先的响应式网格, 从BootStrap3.0开始, 框架将包含了移动终端设备的优先的样式.
- 浏览器支持IE, Firefox, opera, chrome, safari.
- 基于WEB字体的图标, 适用于移动及高密度屏幕(高清屏).
- 使用更简单, 让开发者更容易上手, 只要你具备HTML和CSS的基础知识.
- 响应式设计, 这也是BootStrap最大的特色, 它能够自适应于台式机, 平板电脑和手机.
- 标记和样式更加简洁高效.
- 包含了功能强大的内置组件, 易于定制.
- 它是开源的, 可以根据需求任何更改源码.

### 3.BootStrap包的内容

- 基本结构: BootStarp提供了一个带着网络系统, 链接样式, 背景的基本结构.
- css: 自带, 全局的css设置, 定义基本的HTML元素样式, 可扩展的class, 以及一个先进的网格系统.
- 组件: 包含了十几个可重用的组件, 用于创建图像, 下拉菜单, 导航, 警告, 弹出框等等.
- JavaScript插件: 包含了十几个自定义的jQuery插件.
- 定制: 我们可以根据实际的需求定制BootStrap的组件等.


### 4.下载BootStrap源码

[官网下载](http://v3.bootcss.com/)

- 获得所有 CSS 和 JavaScript 原始文件，另外还包含一个说明文档的本地版本，可以直接在 GitHub 中下载最新的版本。

### 5.包含的内容

> ​	Bootstrap 提供了两种形式的压缩包，在下载下来的压缩包内可以看到以下目录和文件，这些文件按照类别放到了不同的目录内，并且提供了压缩与未压缩两种版本。

>#### Bootstrap 插件全部依赖 jQuery
>
>请注意，**Bootstrap 的所有 JavaScript 插件都依赖 jQuery，**因此 jQuery 必须在 Bootstrap 之前引入，就像在基本模版中所展示的一样。在[ `bower.json` 文件中](https://github.com/twbs/bootstrap/blob/v3.3.7/bower.json) 列出了 Bootstra p 所支持的 jQuery 版本。

#### 文档结构

```html
bootstrap/
├── less/
├── js/
├── fonts/
├── dist/
│   ├── css/
│   ├── js/
│   └── fonts/
└── docs/
    └── examples/
```

### 6.基本模板

- 拷贝并粘贴下面给出的 HTML 代码，这就是一个最简单的 Bootstrap 页面了。

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->

    <!--
    IE中独有的条件hack
    -->
    <!--[if lt IE 9]>
      <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>

    <div class="container">
      <h1>你好，世界！</h1>
    </div>

    <div class="container-fluid">
      <h1>HELLO WORLD!</h1>
    </div>
    
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="./js/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="bootstrap/dist/js/bootstrap.min.js"></script>
  </body>
</html>
```

### 7.IE 兼容模式

> ​	Bootstrap 不支持 IE 古老的兼容模式。为了让 IE 浏览器运行最新的渲染模式下，建议将此  `<meta>`  标签加入到你的页面中：

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<!--也就是不支持IE 11以下版本-->
```

### 8.国产浏览器高速模式

> ​	国内浏览器厂商一般都支持兼容模式（即 IE 内核）和高速模式（即 webkit 内核），不幸的是，所有国产浏览器都是默认使用兼容模式，这就造成由于低版本 IE （IE8 及以下）内核让基于 Bootstrap 构建的网站展现效果很糟糕的情况。

- 将下面的 `<meta>` 标签加入到页面中，可以让部分国产浏览器默认采用高速模式渲染页面：

```html
<meta name="renderer" content="webkit">
```



###### 

## 全局CSS样式

### 1.移动设备优先

- 为了确保适当的绘制和触屏缩放，需要在 `<head>` 之中**添加 viewport 元数据标签**。

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### 2.Normalize.css

- 为了增强跨浏览器表现的一致性，我们使用了 [Normalize.css](http://necolas.github.io/normalize.css/)，这是由 [Nicolas Gallagher](https://twitter.com/necolas) 和 [Jonathan Neal](https://twitter.com/jon_neal) 维护的一个CSS 重置样式库。
- 使用标签对样式进行重置
- 使用方式：下载Normalize.css文件，使用link引入外部样式文件

```css
<link rel="stylesheet" href="./css/normalize.css">
```

### 3.布局容器

- Bootstrap 需要为页面内容和栅格系统包裹一个 `.container` 容器。我们提供了两个作此用处的类。注意，由于 `padding` 等属性的原因，这两种 容器类不能互相嵌套。
- `.container` 类用于固定宽度并支持响应式布局的容器。

```html
<div class="container">
  ...
</div>
```

- `.container-fluid` 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<div class="container-fluid">
  ...
</div>
```

### 4.栅格系统

> ​	Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。它包含了易于使用的[预定义类](http://v3.bootcss.com/css/#grid-example-basic)，还有强大的[mixin 用于生成更具语义的布局](http://v3.bootcss.com/css/#grid-less)。

#### 简介

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。下面就介绍一下 Bootstrap 栅格系统的工作原理：

- “行（row）”必须包含在 `.container` （固定宽度）或 `.container-fluid` （100% 宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。
- 通过“行（row）”在水平方向创建一组“列（column）”。
- 你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为行（row）”的直接子元素。
- 类似 `.row` 和 `.col-xs-4` 这种预定义的类，可以用来快速创建栅格布局。Bootstrap 源码中定义的 mixin 也可以用来创建语义化的布局。
- 通过为“列（column）”设置 `padding` 属性，从而创建列与列之间的间隔（gutter）。通过为 `.row` 元素设置负值 `margin` 从而抵消掉为 `.container` 元素设置的 `padding`，也就间接为“行（row）”所包含的“列（column）”抵消掉了`padding`。
- 负值的 margin就是下面的示例为什么是向外突出的原因。在栅格列中的内容排成一行。
- 栅格系统中的列是通过指定1到12的值来表示其跨越的范围。例如，三个等宽的列可以使用三个  `.col-xs-4` 来创建。
- 如果一“行（row）”中包含了的“列（column）”大于 12，多余的“列（column）”所在的元素将被作为一个整体另起一行排列。
- 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何 `.col-md-*` 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何 `.col-lg-*` 不存在， 也影响大屏幕设备。

#### 栅格参数

|                   |  超小屏幕手机 (<768px)   |      小屏幕平板 (≥768px)       |    中等屏幕桌面显示器 (≥992px)     |    大屏幕大桌面显示器 (≥1200px)    |
| :---------------: | :----------------: | :-----------------------: | :-----------------------: | :-----------------------: |
|      栅格系统行为       |       总是水平排列       | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列 | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列 | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列 |
| `.container` 最大宽度 |     None （自动）      |           750px           |           970px           |          1170px           |
|        类前缀        |     `.col-xs-`     |        `.col-sm-`         |        `.col-md-`         |        `.col-lg-`         |
|        列数         |         12         |            12             |            12             |            12             |
|       最大列宽        |         自动         |           ~62px           |           ~81px           |           ~97px           |
|        槽宽         | 30px （每列左右均有 15px） |    30px （每列左右均有 15px）     |    30px （每列左右均有 15px）     |    30px （每列左右均有 15px）     |
|        可嵌套        |         是          |             是             |             是             |             是             |
|        偏移         |         是          |             是             |             是             |             是             |
|        列排序        |         是          |             是             |             是             |             是             |




















