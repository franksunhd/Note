## CSS Hack

[TOC]

### 1.什么是CSS Hack

- CSS hack是通过在CSS样式中加入一些特殊的符号，让不同的浏览器识别不同的符号（什么样的浏览器识别什么样的符号是有标准的，CSS hack就是让你记住这个标准），以达到应用不同的CSS样式的目的。
- 这里只列举一些使用比率较高的常用CSS Hack，且不考虑IE6以下的版本
- CSS Hack一般都是利用各浏览器的支持CSS的能力和BUG来进行的。所以对浏览器的选择大致可以分为能力选择和怪癖选择(BUG)。能力通常是指浏览器对CSS特性的支持程度，而怪癖是指浏览器特有的一些BUG。

### 2.CSS hack的原理

- 由于不同的浏览器和浏览器各版本对CSS的支持及解析结果不一样，以及CSS优先级对浏览器展现效果的影响，我们可以据此针对不同的浏览器情景来应用不同的CSS。

### 3.CSS hack分类

> CSS Hack大致有3种表现形式，IE条件Hack、选择符Hack以及属性级Hack，实际项目中CSS Hack大部分是针对**IE浏览器**不同版本之间的表现差异而引入的。

**条件Hack(即HTML条件注释Hack)**

- 针对所有IE(注：IE10+已经不再支持条件注释)： IE浏览器显示的内容 ，针对IE6及以下版本： 。这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效。

**属性级Hack(即类内部Hack)**

- 例如 IE6能识别下划线"\_"和星号" * "，IE7能识别星号" * "，但不能识别下划线C"\_"，IE6~IE10都认识"\9"，但firefox前述三个都不能认识。 

**选择符级Hack(即选择器Hack)**

- 例如 IE6能识别\*html .class{}，IE7能识别\*+html .class{}或者*:first-child+html .class{}。 

### 4.CSS Hack书写顺序

- CSS hack书写顺序，一般是将适用范围广、被识别能力强的CSS定义在前面。

### 5.条件Hack

**语法**

```css
<!--[if <keywords>? IE <version>?]> 
HTML代码块 
<![endif]-->
```

```css
<!--[if lt IE 8 ]>
    <style>
    .one {
      color: red;
    }
    </style>
<![endif]-->
```

**取值**

\<keywords>

if条件共包含6种选择方式：是否、大于、大于或等于、小于、小于或等于、非指定版本

- 是否：

  指定是否IE或IE某个版本。关键字：*空*

- 大于：

  选择大于指定版本的IE版本。关键字：*gt*（greater than）

- 大于或等于：

  选择大于或等于指定版本的IE版本。关键字：*gte*（greater than or equal）

- 小于：

  选择小于指定版本的IE版本。关键字：*lt*（less than）

- 小于或等于：

  选择小于或等于指定版本的IE版本。关键字：*lte*（less than or equal）

- 非指定版本：

  选择除指定版本外的所有IE版本。关键字：*!*

\<version>

目前的常用IE版本为6.0及以上，推荐酌情忽略低版本，把精力花在为使用高级浏览器的用户提供更好的体验上

IE10及以上版本已将条件注释特性移除，使用时需注意。

**说明**

用于选择IE浏览器及IE的不同版本

- if条件Hack是HTML级别的（包含但不仅是CSS的Hack，可以选择任何HTML代码块）

**如不想在非IE中看到某区域，可这样写：**

> ```html
> <!--[if IE]>
> <p>你在非IE中将看不到我的身影</p>
> <![endif]-->
> ```

上述p代码块，将只在IE中可见。

- if条件6种选择方式的使用示例（下述代码中被条件注释包含的HTML代码块也可以是link标记）：

**是否，示例代码：**

> ```html
> <!--[if IE]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，只有IE浏览，才能看到应用了test类的元素是红色文本。

**大于，示例代码：**

> ```html
> <!--[if gt IE 6]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，只有IE6以上，才能看到应用了test类的元素是红色文本。

**大于或等于，示例代码：**

> ```html
> <!--[if gte IE 6]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，只有IE6以上（含IE6），才能看到应用了test类的元素是红色文本。

**小于，示例代码：**

> ```html
> <!--[if lt IE 7]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，只有IE7以下，才能看到应用了test类的元素是红色文本。

**小于或等于，示例代码：**

> ```html
> <!--[if lte IE 7]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，只有IE7以下（含IE7），才能看到应用了test类的元素是红色文本。

**非指定版本，示例代码：**

> ```html
> <!--[if ! IE 7]>
> <style>
> .test{color:red;}
> </style>
> <![endif]-->
> ```

在上述代码中，除IE7以外的IE版本，都能看到应用了test类的元素是红色文本。

**实例**

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">

<head>
  <meta charset="utf-8" />
  <title>if条件Hack_CSS参考手册_web前端开发参考手册系列</title>

  <style>
    h1 {
      margin: 10px 0;
      font-size: 16px;
    }

    span {
      display: none;
    }

    .not-ie {
      display: inline;
    }
  </style>
	<!--[if IE]>
		<style>
			.ie{display:inline;}
			.not-ie{display:none;}
		</style>
  	<![endif]-->

  	<!--[if IE 5]>
		<style>
			.ie5{display:inline;}
		</style>
	<![endif]-->

 	<!--[if IE 6]>
		<style>
			.ie6{display:inline;}
		</style>
	<![endif]-->

  	<!--[if IE 7]>
		<style>
			.ie7{display:inline;}
		</style>
	<![endif]-->

  	<!--[if IE 8]>
		<style>
			.ie8{display:inline;}
		</style>
	<![endif]-->

  	<!--[if IE 9]>
		<style>
			.ie9{display:inline;}
		</style>
	<![endif]-->
</head>
<body>
  <div>
    您正在使用
    <span class="not-ie">非IE</span>
    <span class="ie">IE</span>
    <span class="ie5">5</span>
    <span class="ie6">6</span>
    <span class="ie7">7</span>
    <span class="ie8">8</span>
    <span class="ie9">9</span> 浏览器
  </div>
</body>
</html>

<!--结果在浏览器中看到文字  “您正在使用 非IE 浏览器 ”-->
```

### 6.属性级Hack

**语法**

```html
selector{
	<hack>?property:value<hack>?;
}
```

**取值**

-  \_：选择IE6及以下。*连接线（中划线）（-）亦可使用，为了避免与某些带中划线的属性混淆，所以使用下划线（_）更为合适。
-  \*：选择IE7及以下。诸如：（+）与（#）之类的均可使用，不过业界对（\*）的认知度更高。
-  \9：选择IE6+
-  \0：选择IE8+和Opera15以下的浏览器

**说明**

选择不同的浏览器及版本

- 尽可能减少对CSS Hack的使用。*Hack有风险，使用需谨慎*
- 通常 如未作特别说明，本文档所有的代码和示例的默认运行环境都为标准模式。
- 一些CSS Hack由于浏览器存在交叉认识，所以需要通过层层覆盖的方式来实现对不同浏览器进行Hack的。

**如想同一段文字在IE6,7,8显示为不同颜色，可这样写：**

> ```css
> .test {
> 	color: red\9; /* For IE6+ */
> 	*color: #f00;  /* For IE7 and earlier */
> 	_color: #ff0;  /* For IE6 and earlier */
> }
> ```

\* 上述Hack均需运行在标准模式下，若在怪异模式下运行，这些Hack将会被不同版本的IE相互识别，导致失效。

**实例**

```html
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
<meta charset="utf-8" />
<title>属性级Hack_CSS参考手册_web前端开发参考手册系列</title>
<style>
h1 {
	margin: 10px 0;
	font-size: 16px;
}
.test {
	color: #c30;          /* For latest Firefox, chrome, Safari */
	color: #090\0;        /* For Opera15- */
	color: #00f\9;        /* For IE8+ */
	*color: #f00;         /* For IE7 */
	_color: #ff0;         /* For IE6 */
}
</style>
</head>
<body>
<div class="test">在不同浏览器下看看我的颜色吧</div>
</body>
</html>
```

### 7.选择符级Hack

**语法**

```html
<hack> selector{ sRules }
```

**说明**

选择不同的浏览器及版本

- **简单列举几个：**

  > ```css
  > * html .test { color: #090; }       /* For IE6 and earlier */
  > * + html .test { color: #ff0; }     /* For IE7 */
  > .test:lang(zh-cmn-Hans) { color: #f00; }  /* For IE8+ and not IE */
  > .test:nth-child(1) { color: #0ff; } /* For IE9+ and not IE */
  > ```

  \* 上述代码中的3,4两行就是典型的利用伪类来进行选择的CSS Hack。

