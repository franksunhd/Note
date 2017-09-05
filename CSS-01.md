## CSS层叠样式表/选择器/样式类型/三大特性

[TOC]

### 1. 初识CSS

－	CSS通常称为CSS样式表或层叠样式表（级联样式表），主要用于设置HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及版面的布局等外观显示样式。
－	CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。

### 2. CSS的作用

- CSS 主要目的： 控制网页中元素的样式
- CSS 可以让我们从HTML结构和样式分离出来。
- CSS 可以让我们专注结构。代码更少，语义更好，搜索更容易。

### 3. CSS规则

－	使用HTML时，需要遵从一定的规范。CSS亦如此，要想熟练地使用CSS对网页进行修饰，首先需要了解CSS样式规则，具体格式如下:

```html
选择器{
	属性1:属性值1; 
	属性2:属性值2; 
	属性3:属性值3;
}
```

－	在上面的样式规则中，选择器用于指定CSS样式作用的HTML对象，花括号内是对该对象设置的具体样式。其中，属性和属性值以“键值对”的形式出现，属性是对指定的对象设置的样式属性，例如字体大小、文本颜色等。属性和属性值之间用英文“:”连接，多个“键值对”之间用英文“;”进行区分。

比如：

```html
h1 {
  color:red;
  font-size:50px;
}
```

### 4. CSS选择器	[jQuery](./jQuery-01.md)

－	要想将CSS样式应用于特定的HTML元素，首先需要找到该目标元素。在CSS中，执行这一任务的样式规则部分被称为选择器，CSS基础(还有很多)选择器有四种。

- 标签选择器
- 类选择器
- id选择器
- 通配选择器

#### 标签选择器

```html
标签名　{
  	属性1:属性值1; 
	属性2:属性值2; 
	属性3:属性值3; 
}
```

例如：

```html
<head>
<title>标签选择器</title>
<style>
h1 {
  	color:red;
}
p {
  	color:green;
}
</style>
</head>
<body>
  <h1>大标题</h1>
  <p>p标签</p>
</body>
```

#### 类选择器

```html
.ClassName {
  	属性1:属性值1; 
	属性2:属性值2; 
	属性3:属性值3;
}
```

例如：

```html
<head>
<title>类选择器</title>
<style>
  /*
  	类名的命名要规范;尽量见名知意
  	定义类名
  */
.color-red {
  	color:red:
}
</style>
</head>
<body>
  <!--使用类-->
  <p　class="color-red">段落</p>
</body>
```

#### Id选择器

```html
#IdName {
  	属性1:属性值1; 
	属性2:属性值2; 
	属性3:属性值3;
}
```

例如：

```html
<head>
<title>ID选择器</title>
<style>
  /*定义ＩＤ选择器*/
 ＃div-01 {
 	color:red;     
  }
</style>
</head>
<body>
  <div　id="div-01">
    div标签
  </div>
</body>

```

#### 通配选择器

```html
* {
  	属性1:属性值1; 
	属性2:属性值2; 
	属性3:属性值3;
}
```

例如：

```html
<head>
<title>通配选择器</title>
<style>
  * {
    /*取下所有外边距*/
     margin:0;
  }
</style>
</head>
```

#### 后代选择器

```html
<head>
<title>后代选择器</title>
<style>
/*
	后代选择器以　“空格”　为间隔符
	子辈和孙辈都可以受到影响
*/
/* 标签选择器 */
      div p span {
        color:red;
      }
      div span {
        color: blue;
      }
      /*类选择器*/
      .first-01 p {
        color:pink;
      }
      /*Id 选择器*/
      #div-01 p {
        color: green;
      }
    </style>
</head>
<body>
	<!-- 标签选择器 -->
    <div class="">
      <p><span>文本１</span></p>
    </div>
    <div class="">
      <p>文本2</p>
    </div>
    <div class="">
      <span>文本3</span>
    </div>
    <!-- 类选择器 -->
    <div class="first-01">
      <p>类选择器</p>
    </div>
    <!-- ID选择器 -->
    <div id="div-01">
      <p>Id选择器</p>
    </div>
</body>
```

#### 交集选择器

－	选择两个集合中的公共部分

```HTML
div.p {
  color:red;
}
```

```html
<head>
<title>交集选择器</title>
    <style media="screen">
    /* 既满足是p, 又满足包含color_red的类
       交集选择器中间是连续写，没有空格
    */
    　/*　标签/类*/
      div p.color_red.one {
        color: red;
      }
      /*标签/ID*/
      h1 p#p1 span {
        color: yellow;
      }
    </style>
</head>
<body>
      <!--
      添加了2个类
      既要满足color_red类 ,也要满足one类，否则不可以
    -->
    <div>
      <p class="color_red one">111</p>
      <p>222</p>
      <p>333</p>
    </div>

    <!-- 类不再p标签中 -->
    <div>
      <h1 class="color_red">sjgkjkjhk</h1>
    </div>
    
    <!-- 不显示红色 -->
    <p class="color_red">pppppp</p>
    
    <!-- 标签/ID -->
    <h1>
      <p id="p1"><span>ksjgkdjhkjhkhj</span></p>
    </h1>
  </body>
```

#### 并集选择器

－	对多个集合中的所有内容合并在一起进行设置．

```html
<head>
    <title>并集选择器</title>
    <style media="screen">
    /*
    并集以“,”作为分隔符
    */
    p,div{
      color: red;
    }

    h3 span , h2 span {
      color: green;
    }
    </style>
  </head>
  <body>
    <!-- p标签和div标签都为红色 -->
    <p>p标签</p>
    <div>div标签</div>

    <!-- 下面两个都为绿色 -->
    <h3><span>h3>span</span></h3>
    <h2><span>h2>span</span></h2>
  </body>
```

#### 伪类选择符

##### E:link

##### E:visited

##### E:hover

##### E:active

```html
<!--
    所有的元素都有link(初始),visited(访问过),hover(悬停),active(按下)伪类.
    但是只有a,才都可以设置。其他元素hover(悬停),active(按下)有效。

    考虑到浏览器的兼容性问题：
    这四个伪类在a元素要想都有效果，需要按照顺序：link  visited hover active
-->
a:link {
  
}
a:visited {
  
}
a:hover {
  
}
a:active {
  
}
```

例如：

```html
<head>
    <meta charset="utf-8">
    <title>伪类</title>
    <style>
    a {
      font-size: 50px;
    }

    /*伪类，link初始样式*/
    a:link{
      color: black;
    }

    /* 鼠标悬停的效果*/
    a:hover {
      color: yellow;
    }

    /*激活状态，鼠标按下*/
    a:active {
      color: green;
    }

    /*访问过的链接*/
    a:visited {
      color: pink;
    }

    .one:hover {
      color: purple;
    }

    .one:active {
      color: black;
    }

  </style>
  </head>
  <body>
    <a href="https:/www.tmall.com" target="_blank">跳转</a>
	<!--只有hover(悬停)，和active(按下)显示，其余两个没有效果-->
    <div class="one">div的颜色变化</div>
  </body>
```

##### E:checked(只适用于radio和checked类型)

```html
<style>
      input {
        width: 50px;
        height: 50px;
      }

      input:checked + span {
        background: pink;
      }

      input:checked + span::before {
        content: "我被选中了";
      }
</style>
<input type="checkbox">
<span></span>
<!--input复选框被选中之后,span标签内部的最前面添加文本-->
```

##### E:target 被锚点中之后 的样式

```html
<style>
      /*被锚点中之后，的样式*/
      p:target {
        font-size: 50px;
        color: red;
      }
</style>
<a href="#p1">锚点</a>
<p id="p1">闪光灯看见到很快就会</p>
<!--结果为点击锚点链接,p标签的字体变大,颜色变红-->
```

##### E:empty 内容为空的元素被选中

```html
<style>
/* 内容为空的元素会被 选中 empty*/
      .one:empty::before {
        content: "我是空的";
      }

</style>
<div class="one">空间商客户开始角度好看见好看</div>
    <div class="one"></div>
    <div class="one"></div>
<!--结果为下面的两个div中添加了"我是空的"-->
```

##### E:enabled 匹配可用状态的元素

##### E:disabled 匹配不可用状态的元素 

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
<meta charset="utf-8" />
<title>用户界面(UI)元素状态伪类选择符 E:enabled_CSS参考手册_web前端开发参考手册系列</title>
<meta name="author" content="Joy Du(飘零雾雨), dooyoe@gmail.com, www.doyoe.com" />
<style>
li {
	padding: 3px;
}
input[type="text"]:enabled {
	border: 1px solid #090;
	background: #fff;
	color: #000;
}
input[type="text"]:disabled {
	border: 1px solid #ccc;
	background: #eee;
	color: #ccc;
}
</style>
</head>
<body>
<form method="post" action="#">
<fieldset>
	<legend>E:enabled与E:disabled</legend>
	<ul>
		<li><input type="text" value="可用状态" /></li>
		<li><input type="text" value="可用状态" /></li>
		<li><input type="text" value="禁用状态" disabled="disabled" /></li>
		<li><input type="text" value="禁用状态" disabled="disabled" /></li>
	</ul>
</fieldset>
</form>
</body>
</html>
```

#### 伪对象选择符

##### E:first-letter/E::first-letter 设置对象内第一个字符的样式

```html
<style>
      .one::first-letter {
       font-size: 50px;
       font-weight: bolder;
     }
</style>
<p class="one">
      我爱你 中国  <br>
      I love you China <br>
</p>
<!--结果为"我"变大变粗-->
```

##### E:first-line/E::first-line 设置对象内第一行字符的样式

```html
<style>
      .one::first-letter {
       font-size: 50px;
       font-weight: bolder;
     }
</style>
<p class="one">
      我爱你 中国  <br>
      I love you China <br>
</p>
<!--结果为"我爱你 中国"变大变粗-->
```

##### E:before/E::before  选中元素内部的头部 ,必须和content配合使用

##### E:after/E::after  选中元素内部的尾部 ,必须和content配合使用

```html
<style>
/* 内容为空的元素会被 选中 empty*/
      .one:empty::before {
        content: "我是空的before";
      }
  .one:empty::after {
        content: "我是空的after";
      }

</style>
<div class="one">空间商客户开始角度好看见好看</div>
    <div class="one"></div>
    <div class="one"></div>
<!--结果为下面的两个div中添加了"我是空的before 我是空的after"-->
```

##### E:placeholder 设置对象文字占位符的样式。

```html
<style>
/*
     浏览器的兼容性问题
*/
     .two::-webkit-input-placeholder{
       color: blue;
     }

     .two::-ms-input-placeholder {
       color: blue;
     }

     .two::-moz-placeholder {		/*Firefox 的兼容性写的时候,不写"-input"*/
       color: blue;
     }
</style>
<input class="two" type="text" placeholder="邮箱/用户名/手机号">
<!--input文本框颜色变为蓝色,不要考虑浏览器的兼容性问题-->
```

##### E:selection  设置对象被选择时的样式

- 需要注意的是，::selection只能定义被选择时的[background-color](http://css.doyoe.com/properties/background/background-color.htm)，[color](http://css.doyoe.com/properties/color/color.htm)及[text-shadow](http://css.doyoe.com/properties/text-decoration/text-shadow.htm)(IE11尚不支持定义该属性)。

```html
<style>
.two::selection {
       color: red;
       background: blue;
     }
</style>
<!--当对象选择时,可以设置选中字体的颜色和背景颜色-->
```

### 5. CSS三种样式类型

#### 行内样式

－　所有的样式都是在写标签的内部，只能作用在这个标签上面。（一般情况下不建议使用，我们单独学习css的目的就是页面的结构和样式的分离,我们不能反其道而行之）。

#### 嵌套样式

－	写在head中，并且用style标签包含。这也是我们比较常用的一种。

#### 外部样式

－	将CSS编写为单独的文件,需要在head中引入。

```html
<head>
<link rel="stylesheet" href="CSS文件路径" type="text/css">
</head>
```

例如：

```html
<head>
    <meta charset="utf-8">
    <title>样式的使用方式</title>
    <!-- 引入外部样式表,共有的部分 -->
    <link rel="stylesheet" href="./css/master.css">

    <!--  -->
    <style media="screen">
      /* 嵌套样式*/
      div {
        color:green;
      }
    </style>
  </head>
  <body>
    <!--
    行内样式
    #注意:style后边是英文双引号,且每个属性值以"分号"结尾
   -->
    <p style="color:red; font-size:50px; ">p标签</p>
    <h1>h1标签</h1>
  </body>
```

**注意：**

1. 如果通过开发人员工具来看拥有外部样式的页面的时候，那么我们会发现请求至少有两条：其中一条页面主体内容的请求，另一条应该就是外部样式的请求。
2. 如果页面上有外部样式的请求，会跟主页面的解析同时进行。

#### 三种样式类型对比

![](https://nts.newbieol.com/static/k111/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/class-003/image/css.jpg)



### 6. CSS的三大特性

#### 继承	[CSS可以和不可以继承的属性](./CSS-04.md)

-　就是页面中的一些标签的属性可以继承给子标签,但是继承还是限制的,比如a的颜色，块级元素的高度等等。
-　一般情况下，所有的与文字图片的大小样式相当的属性都可以继承:font-x,line-x,一些标签的宽高也可以继承。

```html
<!--
继承有局限性：不是所有的样式都能继承
文本相关的基本都可以继承，其他例外
-->
比如：div中的a标签的颜色无法继承；div中的div的高无法继承
```

比如：

```html
<head>
    <meta charset="utf-8">
    <title>继承(本质就是少写代码)</title>
    <style media="screen">
    .one {
      color:red;
    }

    .one p {
      color: green;
    }

    .two {
      color: yellow;
    }

    .three {
      height: 200px;
    }
    </style>
  </head>
  <body>
    <!--
    继承有局限性：不是所有的样式都能继承
    文本相关的基本都可以继承，其他例外
   -->
    <div class="one">
      div元素
      <!-- div中的p继承了div的red属性 -->
      <p>div中的p</p>
    </div>

    <div class="two">
      <!--a的颜色无法继承  -->
      <a href="#">a超链接</a>
    </div>

    <!--块级元素的宽度可以继承，但是高度不可以继承-->
    <div class="three">
      <div>three的子元素</div>
    </div>
  </body>
```

#### 层叠

- 页面的样式是多项属性设置进行叠加的结果。

```html
<head>
    <meta charset="utf-8">
    <title>层叠(效果叠加)</title>
    <style media="screen">
    /*
    对一个元素不同样式的多次设置会进行效果叠加，
    同一样式会覆盖
    */
    .one {
      font-size: 50px;
    }
    .one , .two {
      color: red;
    }
    </style>
  </head>
  <body>
    <!-- p-1标签50px;red -->
    <p class="one">p-1标签</p>
    <!-- p-2标签red; -->
    <p class="two">p-2标签</p>
  </body>
```

#### 优先级

- 当设置发生冲突时，需要考虑优先级，优先级最高的设置有效。
- 基本公式： !important > 行内style > id > class > 标签 > 继承 > 浏览器的默认
- 但是运行公式需要条件：针对同一个标签的设置。

```html
    css的选择器规则，是按照从右到左寻找的！！！！！

    优先级的计算公式(在元素本身上)：
    !important > 行内style > id > class > 标签 > 继承 > 浏览器的默认
<!--
    计算公式：在同一个css的规则中,默认优先级为0
     出现一次 标签，优先级加 1
     出现一次 class，优先级加 10
     出现一次 id ,优先级加 100
    优先级相同，最后的设置有效
-->
```

例如：

```html
  <head>
    <meta charset="utf-8">
    <title>CSS的优先级问题　重点！！！</title>
    <style media="screen">
    #oneId {
      color: green;
    }

    .one {
      color:red;
    }

    p {
      /*
      !important 用于确定最高优先级
      */
      color: yellow !important;
    }

    .two {
      color: purple;
    }

    #twoId {
      color: pink;
    }
    /**/
    .three-1 {
      color: red;
    }
    /* 交集选择器*/
    div.three-1 {
      color: yellow;
    }
    /*后代选择器*/
    div .three-2 {
      color:green;
    }
    </style>
  </head>
  <body>
    <div class="one" id="oneId">
        <!-- id > class 文本１为 #oneId的颜色-->
      文本１
      <!--
          虽然有继承，但是它小于下面的其他类，故不考虑
      -->
      <p class="two" id="twoId"  style="color:brown;">请问p元素是什么颜色？？？</p>
    </div>
    <!--
        three-1:出现一次类选择器+10;交集选择器出现一次div标签+1;所以是１１；
        three-2:位于后代选择器，前边的div是标签+1;后边是类选择器+10;
        两个优先级相同，最后设置有效;
    -->
    <div><!--div .three-2 中的div 指的是这一行的div-->
      <div class="three-1 three-2">div的颜色？？？</div>
    </div>
    <div>
      <h1 class="three-2">pppp</h1>
    </div>
  </body>
```

## 补充内容

### 伪类和伪对象(元素)的区别

- 伪类本质上是为了弥补常规CSS选择器的不足，以便获取到更多信息；
- 伪元素本质上是创建了一个有内容的**虚拟容器**,它本身只是基于元素的抽象，并不存在于文档中；
- CSS3中伪类和伪元素的语法不同；
- 可以同时使用多个伪类，而只能同时使用一个伪元素；
- 一个选择器**只能使用一个伪元素**，并且**伪元素必须处于选择器语句的最后**。

