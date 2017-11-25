## 元素的嵌套原则

[TOC]

### HTML 标签包括 块级元素(block)、内嵌元素（inline）

#### 块级元素

- 一般用来搭建网站架构、布局、承载内容……它包括以下这些标签：

```html
address、blockquote、center、dir、div、dl、dt、dd、fieldset、form、h1~h6、hr、isindex、menu、noframes、noscript、ol、p、pre、table、ul 
```

#### 内嵌元素

- 一般用在网站内容之中的某些细节或部位，用以“强调、区分样式、上标、下标、锚点”等等，下面这些标签都属于内嵌元素：

```html
a、abbr、acronym、b、bdo、big、br、cite、code、dfn、em、font、i、img、input、kbd、label、q、s、samp、select、small、span、strike、strong、sub、sup、textarea、tt、u、var 
```

### HTML 标签的嵌套规则

#### 块元素可以包含内联元素或某些块元素，但内联元素却不能包含块元素，它只能包含其它的内联元素：

```html
<div><h1></h1><p></p></div> 		—— 对	(div可以嵌套某些块元素)
<a href=”#”><span></span></a>		—— 对	(a标签可以嵌套span标签)
<span><div></div></span> 			—— 错 	(span标签是行元素，不可以嵌套div这个块元素)
```

#### 块级元素不能放在\<p>里面

```html
<p> <ol><li></li></ol> </p> 	—— 错	(有序列表是块元素)
<p><div></div></p>			    —— 错 	(div是块元素)
```

#### 有几个特殊的块级元素只能包含内嵌元素，不能再包含块级元素。

```html
h1、h2、h3、h4、h5、h6、p、dt 
```

#### li 内可以包含 div 标签

li 和 div 标 签都是装载内容的容器，地位平等，没有级别之分，li 标签可以容纳它的父级 ul 或者是 o。

#### 块级元素与块级元素并列、内嵌元素与内嵌元素并列

```html
<div><h2></h2><p></p></div> 				—— 对
<div><a href=”#”></a><span></span></div> 	—— 对
<div><h2></h2><span></span></div> 			—— 错 
```









