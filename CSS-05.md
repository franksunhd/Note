## CSS预处理器

[TOC]

### 1.概念/种类

- **CSS预处理器**用一种**专门的编程语言**，进行Web页面样式设计，然后再编译成正常的CSS文件，以供项目使用。CSS预处理器为CSS增加一些编程的特性。
- **优点：**可以在CSS中使用**变量、简单的逻辑程序、函数**等等在编程语言中的一些基本特性，可以让CSS更加简洁、适应性更强、可读性更佳，更易于代码的维护.
- **CSS预处理器种类繁多，主要有Sass、Less、Stylus .**

### 2.Sass是什么

- **Sass 是一个 CSS 的扩展**，它在 CSS 语法的基础上，允许您使用**变量** (variables), **嵌套规则** (nested rules), **混合** (mixins), **导入** (inline imports) 等功能，令 CSS 更加强大与优雅。

### 3.Sass的安装使用

#### 1).window版本

- Ruby官网下载ruby的软件包

#### 2).Linux版本

- sudo apt-get update
- sudo apt-get install ruby
- sudo gem install sass (如果失败，执行下一步)
- sudo apt-get install ruby-sass
- sass --version(检测版本)


#### 3).Sass的使用方法

##### 1.首先需要编译运行生成css文件(sass input.scss   output.css)

- 缺点：没修改一次就需要编译一次

##### 2.监视单个文件改动并自动编译更新css文件(sass --watch input.scss:output.css)

- 缺点：只能监听单个文件，多个文件改动监视运行不方便

##### 3.监视整个目录，并自动更新css文件(sass  --watch   ./scss:./css)

- 优点：一次编译，不能停，每保存一次，自动更新css文件。

##### 注意：监听目录的绝对路径中不能包含中文

##### 注意：文件的注释中不能出现中文

### 4.Sass基础语法

#### 1).文件后缀名	

- sass有两种后缀名文件：一种后缀名为sass，**不使用大括号和分号**；另一种就是我们这里使用的scss文件，这种和我们平时写的css文件格式差不多，**使用大括号和分号**。而本教程中所说的所有sass文件都指后缀名为scss的文件。在此也建议使用后缀名为scss的文件，以避免sass后缀名的严格格式要求报错。

```scss
//文件后缀名为sass的语法
body
  background: #eee
  font-size:12px
p
  background: #0982c1

//文件后缀名为scss的语法  
body {
  background: #eee;
  font-size:12px;
}
p{
  background: #0982c1;
} 
```

#### 2).导入

- 导入.scss 文件的规则和导入.css文件的规则有所不同，编译时会将@import的scss文件合并进来只生成一个CSS文件。但是如果你在sass文件中导入css文件如@import "reset.css"，那效果跟普通CSS导入样式文件一样，导入的css文件不会合并到编译后的文件中，而是以@import方式存在。
- 所有的sass导入文件都可以忽略后缀名.scss。一般来说基础的文件命名方法以_开头，如_a.scss。这种文件在导入的时候可以不写下划线，可写成@import “a”。

```scss
/*a.scss*/
body {
  background: #eee;
}


/*需要导入样式的sass文件b.scss*/
@import "reset.css";	/*已经存在的css文件，在这里被导入*/
@import "a";			/*已经存在的.scss文件，在这里被导入*/

p{
  background: #0982c1;	/*这是b.scss文件中的本身内容*/
} 

/*转译出来的b.css样式*/

@import "reset.css";	/*引入外部css文件的格式不变*/
body {
  background: #eee;		/*a.scss的内容被整合在b.scss中*/
}
p{
  background: #0982c1;	/*自身*/
}
根据上面的代码可以看出，b.scss编译后，reset.css继续保持import的方式，而a.scss则被整合进来了。
```

#### 3).注释

- sass的注释方式有两种，一种是标准的css注释方式/**/,另一种为//双斜线形式的单行注释，不过，这种单行注释不会被转译出来。

```scss
标准的注释
/*
	我是css 的标准注释
	设置body的内边距
*/

body{
    padding：5px;
}

/*
	双斜杠的单行注释
	单行注释跟JavaScript的语言的注释方式 一样，但单行注释不会输入到css文件中。
*/

//我是双斜杠的的单行注释
//设置背景颜色
body {
    background:red;
}
```

#### 4).变量

- sass的变量必须是**$**开头，后面紧跟变量名，而变量值和变量名之间就需要使用冒号(:)分隔开（就像CSS属性设置一样），如果值后面加上!default则表示默认值。

##### 普通变量

- 定义之后可以在全局范围内使用。

```scss
//sass style
//-------------------------------
$fontSize: 12px;
body{
    font-size:$fontSize;
}

//css style
//-------------------------------
body{
    font-size:12px;
}
```

##### 默认变量

sass的默认变量仅需要在值后面加上!default即可。

```scss
//sass style
//-------------------------------
$baseLineHeight:        1.5 !default;
body{
    line-height: $baseLineHeight; 
}

//css style
//-------------------------------
body{
    line-height:1.5;
}

//sass的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可

//sass style
//-------------------------------
$baseLineHeight:        2;
$baseLineHeight:        1.5 !default;
body{
    line-height: $baseLineHeight; 
}

//css style
//-------------------------------
body{
    line-height:2;
}
```

- 可以看出现在编译后的line-height为2，而不是我们默认的1.5。默认变量的价值在进行组件化开发的时候会非常有用。

##### 特殊变量

- 一般我们定义的变量都为属性值，可直接使用，但是如果变量作为属性或在某些特殊情况下等则必须要以#{$variables}形式使用。

```scss
//sass style
//定义变量-------------------------------
$borderDirection:       top !default; 	//默认值
$baseFontSize:          12px !default;
$baseLineHeight:        1.5 !default;

//应用于class和属性
.border-#{$borderDirection}{
  border-#{$borderDirection}:1px solid #ccc;
}
//应用于复杂的属性值
body{
    font:#{$baseFontSize}/#{$baseLineHeight};
}

//css style
//-------------------------------
.border-top{
  border-top:1px solid #ccc;
}
body {
  font: 12px/1.5;	//实际为18px;
}
```

##### 多值变量

- 多值变量分为list类型和map类型，简单来说list类型有点像js中的数组，而map类型有点像js中的对象。
- list数据可通过空格，逗号或小括号分隔多个值，可用nth($var,$index)取值。

###### list

```scss
//一维数据
$px: 5px 10px 20px 30px;

//二维数据，相当于js中的二维数组
$px1: 5px 10px, 20px 30px;
$px2: (5px 10px) (20px 30px);

使用
//sass style
//-------------------------------
		//第一个 为默认，第二个:hover
$linkColor: #08c #333 !default;
a{
  color:nth($linkColor,1);
  font-size:nth(nth($px2,1),2);		//10px
  &:hover{
    color:nth($linkColor,2);
  }
}

//css style
//-------------------------------
a{
  color:#08c;
}
a:hover{
  color:#333;
}
```

###### map(键值对)

- map数据以key和value成对出现，其中value又可以是list。格式为：\$map: (key1: value1, key2: value2, key3: value3);。可通过map-get(\$map,\$key)取值。

```scss
$sizes:( h1:50px, h2:40px, h3:30px, h4:20px, h5:10px);

.one {
    font-size:map-get($sizes,"h1");
}
```

```scss
$heading: (h1: 2em, h2: 1.5em, h3: 1.2em);
使用
//sass style
//-------------------------------
$headings: (h1: 2em, h2: 1.5em, h3: 1.2em);

// $header 和 $size 都是参数 
@each $header, $size in $headings {
  #{$header} {
    font-size: $size;
  }
}

//css style
//-------------------------------
h1 {
  font-size: 2em; 
}
h2 {
  font-size: 1.5em; 
}
h3 {
  font-size: 1.2em; 
}
```

##### 嵌套(Nesting)

- sass的嵌套包括两种：一种是**选择器的嵌套**；另一种是**属性的嵌套**。我们一般说起或用到的都是选择器的嵌套。

###### 选择器嵌套

- 所谓选择器嵌套指的是在一个选择器中嵌套另一个选择器来实现继承，从而增强了sass文件的结构性和可读性。
  在选择器嵌套中，可以使用&表示父元素选择器

```scss
//sass style
//-------------------------------
#top_nav{
  background-color:#333;
  li{
    float:left;
  }
  a{
    color: #fff;
    
    &:hover{
      color:#ddd;
    }
  }
}

//css style
//-------------------------------
#top_nav{
  background-color:#333;
}  
#top_nav li{
  float:left;
}
#top_nav a{
  color: #fff;
}
#top_nav a:hover{
  color:#ddd;
}
```

###### 属性嵌套

- 所谓属性嵌套指的是有些属性拥有同一个开始单词，如border-width，border-color都是以border开头

```scss
//sass style
//-------------------------------
.fakeshadow {
  border: {
    style: solid;
    left: {
      color: #888;
    }
    right: {
      color: #ccc;
    }
  }
}

//css style
//-------------------------------
.fakeshadow {
  border-style: solid;
  border-left-color: #888;
  border-right-color: #ccc; 
}
```

##### @at-root

- sass3.3.0中**新增**的功能，用来跳出选择器嵌套的。默认所有的嵌套，继承所有上级选择器，但有了这个就可以跳出所有上级选择器。

###### 普通跳出嵌套

```scss
//sass style
//-------------------------------
//没有跳出
.parent-1 {
  color:#f00;
  .child {
    width:100px;
  }
}

//单个选择器跳出
.parent-2 {
  color:#f00;
  @at-root .child {
    width:200px;
  }
}

//css style
//-------------------------------
.parent-1 {
  color: #f00;
}
.parent-1 .child {
  width: 100px;
}

.parent-2 {
  color: #f00;
}
.child {
  width: 200px;
}//sass style
//-------------------------------
//没有跳出
.parent-1 {
  color:#f00;
  .child {
    width:100px;
  }
}

//单个选择器跳出
.parent-2 {
  color:#f00;
  @at-root .child {
    width:200px;
  }
}

//多个选择器跳出
.parent-3 {
  background:#f00;
  @at-root {
    .child1 {
      width:300px;
    }
    .child2 {
      width:400px;
    }
  }
}

//css style
//-------------------------------
.parent-1 {
  color: #f00;
}
.parent-1 .child {
  width: 100px;
}

.parent-2 {
  color: #f00;
}
.child {
  width: 200px;
}

.parent-3 {
  background: #f00;
}
.child1 {
  width: 300px;
}
.child2 {
  width: 400px;
}
```

##### 混合(mixin)

- sass中使用@mixin声明混合，可以传递参数，参数名以$符号开始，多个参数以逗号分开，也可以给参数设置默认值。声明的@mixin通过@include来调用。

###### 无参数mixin

```scss
//sass style
//-------------------------------
@mixin center-block {
    margin-left:auto;
    margin-right:auto;
}
.demo{
  //@include调用
    @include center-block;
}

//css style
//-------------------------------
.demo{
    margin-left:auto;
    margin-right:auto;
}
```

###### 有参数mixin

```scss
//sass style
//-------------------------------   
@mixin opacity($opacity:50) {
  opacity: $opacity / 100;
}

//css style
//-------------------------------
.opacity{
  @include opacity; 	//不传参数使用默认值 50
}
.opacity-80{
  @include opacity(80); //传递参数
}
```

###### 多个参数mixin

- 调用时可直接传入值，如@include传入参数的个数小于@mixin定义参数的个数，则按照顺序表示，后面不足的使用默认值，**如不足的没有默认值则报错**。除此之外还可以选择性的传入参数，使用参数名与值同时传入。

```scss
//sass style
//-------------------------------   
@mixin horizontal-line($border:1px dashed #ccc, $padding:10px){
    border-bottom:$border;
    padding-bottom:$padding;  
}
.imgtext-h li{
    @include horizontal-line(1px solid #ccc);
}
.imgtext-h--product li{
    @include horizontal-line($padding:15px);
}

//css style
//-------------------------------
.imgtext-h li {
    border-bottom: 1px solid #ccc;
    padding-top: 10px;
    padding-bottom: 10px;
}
.imgtext-h--product li {
    border-bottom: 1px dashed #ccc;
    padding-bottom: 15px;
}
```

###### 多组值参数mixin

- 如果一个参数可以有多组值，如box-shadow、transition等，那么参数则需要在变量后加三个点表示，如$variables…。

```scss
//sass style
//-------------------------------   
//box-shadow可以有多组值，所以在变量参数后面添加...
@mixin box-shadow($shadow...) {
  box-shadow:$shadow;
}

.box{
  border:1px solid #ccc;
  @include box-shadow(0 2px 2px red,0 3px 3px blue,0 4px 4px green);
}

//css style
//-------------------------------
.box{
  border:1px solid #ccc;
  box-shadow:0 2px 2px red,0 3px 3px blue,0 4px 4px green;
}
```

###### @content(解决@media等带来的问题)

```scss
//sass style
//-------------------------------   
@mixin max-screen($size){
  @media screen and (max-width: $size){
    @content;
  }
}

@include max-screen(980px){
  // content
  .one {
    color: yellow;
    font-size: 30px;
  }
}

@include max-screen(500px){
  .two {
    color: red;
    font-size: 20px;
  }
}
//css style
//-------------------------------
@media screen and (max-width: 980px) {
  .one {
    color: yellow;
    font-size: 30px;
  }
}

@media screen and (max-width: 500px) {
  .two {
    color: red;
    font-size: 20px;
  }
}
```

##### 继承

- sass中，选择器继承可以让选择器继承另一个选择器的所有样式，并联合声明。使用选择器的继承，要使用关键词@extend，后面紧跟需要继承的选择器。

```scss
//sass style
//------------------------------- 
//@extend
.one{
  width: 100px;
  height: 100px;
  line-height: 100px;
  text-align: center;
}

.two {
  @extend .one;
  background: yellow;
}

h1 {
  font-size: 50px;
}

.three {
  @extend .two;
  @extend h1;
}
//css style
//-------------------------------
.one, .two, .three {
  width: 100px;
  height: 100px;
  line-height: 100px;
  text-align: center;
}

.two, .three {
  background: yellow;
}

h1, .three {
  font-size: 50px;
}
```

##### 占位选择器%

- 从sass 3.2.0以后就可以定义占位选择器%。这种选择器的优势在于：如果不调用则不会有任何多余的css文件，避免了以前在一些基础的文件中预定义了很多基础的样式，然后实际应用中不管是否使用了@extend去继承相应的样式，都会解析出来所有的样式。占位选择器以%标识定义，通过@extend调用。

```scss
//sass style
//-------------------------------
// %
%hehe{
  letter-spacing: 20px;
}

%a{
  letter-spacing: 20px;
}

.one {
  width: 100px;
  height: 100px;
  @extend %hehe;
}

.two {
  @extend %hehe;
}
//css style
//-------------------------------
.one, .two {
  letter-spacing: 20px;
}

.one {
  width: 100px;
  height: 100px;
}

//结果a没有被调用
```

##### 函数

```scss
//sass style
//-------------------------------
//function
//define
@function toPx($value){
  @return $value * 10px;
}


@function opacity($value){
  @return $value / 100;
}

.one {
  font-size: toPx(10);
  opacity: opacity(30);
  color: lighten(red, 0%);	//lighten默认函数
}

//css style
//-------------------------------
.one {
  font-size: 100px;
  opacity: 0.3;
  color: red;
}
```

##### 条件判断

###### @if判断

- @if可一个条件单独使用，也可以和@else结合多条件使用

```scss
//sass style
//-------------------------------
//@if
$type: 3;

.one {
  @if $type == 1 {
    color: yellow;
    font-size: 20px;
  } @else if $type == 2 {
    color: blue;
    background: yellow;
  } @else if $type == 3 {
    color: green;
  } @else {
    color: #000;
  }
}
//css style
//-------------------------------
.one {
	color: green;
}
```

###### 三目判断

```scss
语法为：if($condition, $if_true, $if_false) 。三个参数分别表示：条件，条件为真的值，条件为假的值。
if(true, 1px, 2px) => 1px
if(false, 1px, 2px) => 2px
```

##### 循环

###### for循环

```scss
//sass style
//-------------------------------
//第一种through 包含3
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
//第二种to 不包含3
@for $i from 1 to 3 {
  .class-#{$i} { width: 2em * $i; }
}

//css style
//-------------------------------
.item-1 {
  width: 2em; 
}
.item-2 {
  width: 4em; 
}
.item-3 {
  width: 6em; 
}

.class-1 {
  width: 2em; 
}
.class-2 {
  width: 4em; 
}
```

###### each循环

```scss
//sass style
//-------------------------------
//list
$px: top 10px solid, bottom 20px dotted , left 30px  dashed,right 40px double;

@each $dir, $size, $style in $px {
  .border-#{$dir}{
    border-#{$dir}: $size $style red;
  }
}
//map
$h: (h1: 50px, h2: 40px, h3: 30px, h4: 20px);
@each $key, $value in $h {
  .item-#{$key} {
    font-size: $value;
  }
}

//css style
//-------------------------------
.border-top {
  border-top: 10px solid red;
}

.border-bottom {
  border-bottom: 20px dotted red;
}

.border-left {
  border-left: 30px dashed red;
}

.border-right {
  border-right: 40px double red;
}

.item-h1 {
  font-size: 50px;
}

.item-h2 {
  font-size: 40px;
}

.item-h3 {
  font-size: 30px;
}

.item-h4 {
  font-size: 20px;
}
```


























