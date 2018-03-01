## jQuery中的查找/过滤/工具/核心

[TOC]

### 1.查找

```html
<div id="box">
    <ul>
        <li class="l1">li1</li>
        <li>li2</li>
        <li class="l3">li3</li>
        <li>li4</li>
    </ul>
</div>
```

#### .parent() 获取每个匹配元素的父元素

```javascript
console.log($(".l1").parent());  // ul
```

#### .parents([选择器]) 获取匹配元素的所有祖先元素

```javascript
console.log($(".l1").parents()); // ul div#box body html
console.log($(".l1").parents("#box")); // div#box
```

#### .parentsUntil(选择器) 找的元素不包含参数

```javascript
console.log($(".l1").parentsUntil("body")); // ul div#box
```

#### .offsetParent() 和原生的一样,查找具有定位关系的父元素

```javascript
console.log($("#box").offsetParent());  // html
```

#### .children() 获得匹配元素集合中每个元素的子元素

```javascript
<ul class="level-1">
  <li class="item-i">I</li>
  <li class="item-ii">II
    <ul class="level-2">
      <li class="item-a">A</li>
      <li class="item-b">B
        <ul class="level-3">
          <li class="item-1">1</li>
          <li class="item-2">2</li>
          <li class="item-3">3</li>
        </ul>
      </li>
      <li class="item-c">C</li>
    </ul>
  </li>
  <li class="item-iii">III</li>
</ul>
<script>
 $('ul.level-2').children().css('background-color', 'red');
</script>
<!--结果为A,B,C有红色背景-->
/**************************************************/

// children 找第一代
console.log($("#box ul").children()); // li.l1  li   li.l3   li
```

#### .find(选择器|JQ对象|原生对象) 参数必传 

```javascript
console.log($("#box").find("ul")); // ul
```

#### .siblings() 获取匹配元素中每个元素的兄弟元素

```html
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
</ul>
<script>
 var i=0;
  if(i<=6){
      $("li").eq(i).addClass("active").siblings().removeClass("active");
  }
</script>
<!--结果依次为li元素添加和删除类-->
```

#### .next() 取得匹配的元素集合中每一个元素紧邻的后面同辈元素的元素集合。 

- 如果提供一个选择器，那么只有紧跟着的兄弟元素满足选择器时，才会返回此元素。

```html
  <div>
    <button disabled="disabled">First</button> - <span></span>
  </div>
  <div>
    <button>Second</button> - <span></span>
  </div>
  <div>
    <button disabled="disabled">Third</button> - <span></span>
  </div>
<script>
  $("button[disabled]").next().text("this button is disabled");
</script>
<!--结果为first和third按钮后有文本-->
```

#### .nextAll() 获得每个匹配元素集合中所有下面的同辈元素。

```html
<ul>
   <li>1</li>
   <li>2</li>
   <li>3</li>
   <li class="third-item">4</li>
   <li>5</li>
   <li>6</li>
   <li>7</li>
</ul>
<script>
$('li.third-item').nextAll().css('color', 'red');
</script>
<!--结果为5,6,7变为红色-->
```

#### .nextUntil() 查找当前元素之后所有的同辈元素，直到遇到匹配的那个元素为止。

```javascript
console.log($("#box .l3").nextUntil("#box"));  // li
```

#### .prev() 获取集合中每个匹配元素紧邻的前一个兄弟元素。 

```javascript
<ul>
   <li>list item 1</li>
   <li>list item 2</li>
   <li class="third-item">list item 3</li>
   <li>list item 4</li>
   <li>list item 5</li>
</ul>
<script>
$('li.third-item').prev().css('color', 'red');
</script>
<!--结果为2变为红色-->
/**************************/

console.log($("#box .l3").prev());  // li
```

#### .prevAll() 获得集合中每个匹配元素的所有前面的兄弟元素。

```html
<ul>
   <li>list item 1</li>
   <li>list item 2</li>
   <li class="third-item">list item 3</li>
   <li>list item 4</li>
   <li>list item 5</li>
</ul>
<script>
$('li.third-item').prevAll().css('color', 'red');
</script>
<!--结果为1,2变为红色-->
```

#### .prevUntil()  查找当前元素之前所有的同辈元素，直到遇到匹配的那个元素为止。

```javascript
console.log($("#box .l3").prevUntil("#box"));  // li  li.l1
```

### 2.过滤

```html
<div id="box">
    <ul>
        <li class="l1">li1</li>
        <li class="l1">li2</li>
        <li class="l3">li3</li>
        <li>li4</li>
    </ul>
</div>
```

#### hasClass(类名)  判断是否有某个类名

```javascript
// hasClass(类名)   结合 addClass 和 removeClass
console.log($("#box li").hasClass("l1")); // true
```

#### filter(选择器)  筛选符合条件的元素 

```javascript
console.log($("#box li").filter(".l1"));  // li.l1  li.l1
console.log($("#box li").filter(".l1:first"));  // li.l1
```

#### is(选择器) 判断匹配元素是否与选择元素相同 --Boolean值 

```javascript
console.log($("#box li").parent().is("ul")); // true
```

#### map()

```javascript
$("#box li").map(function (index,value) {
    index += 10;
    console.log(index,value);
});
```

#### has() 判断匹配元素是否含有选择的 DOM元素

```javascript
console.log($("#box ul").has(".l1"));
```

#### not()

```javascript
console.log($("#box ul").not(".l1"));
```

#### slice(start,[end])

### 3.工具  — 数组和对象操作

#### $.each(fn)

```javascript
$("ul li").each(function(index,value) {
    console.log(index,value);
});

// $.each() 遍历对象或数组
$.each([1,2,3,[4,5,6]],function(index,value) {
    console.log(index,value);
});

var person =  {name:"lisi",age:18};
$.each(person,function(key,value) {
    console.log(key,value);
});
```

#### $.extend() 扩展对象,返回值是扩展的对象

```javascript
var temp = {};
var person1 = {
    name:"lisi",
    hobby:["抽烟","喝酒","烫头"]
};
var person2 = {
    name:"ssy",
    age:18
};
// 把 person1和 person2扩展到 temp中
// 参数1给 true, 深拷贝,重新开辟内存空间
var extendObj = $.extend(temp,person1,person2);
console.log(temp,extendObj); 
// {name: "ssy", hobby: Array(3), age: 18} {name: "ssy", hobby: Array(3), age: 18}
// 返回值和 第一个对象 是相等的
console.log(temp == extendObj);  // true
```

##### extend可以扩展公用的函数

```javascript
$.extend({
    request:function() {
        console.log("公用请求函数");
        console.log(this.url);
        console.log(this === $);
    },
    url:"http://www.baodu.com"
});

$.request();  // 公用请求函数  http://www.baodu.com  true
console.log($.url); // http://www.baodu.com

/***************************扩展方式*****************************/
console.log($.prototype);  
// Object [jquery: "3.1.1", constructor: ƒ, toArray: ƒ, get: ƒ, pushStack: ƒ, …]

// 1.
jQuery.prototype.run = function() {
    console.log(this);
    console.log("跑步");
}

$("ul li").run();
$("#box").run();

// 2.$.fn JQ对象的原型
console.log($.fn);
// Object [jquery: "3.1.1", constructor: ƒ, toArray: ƒ, get: ƒ, pushStack: ƒ, …]

console.log($.fn === $.prototype);  // true
$.fn.eat = function() {
    console.log("eat----");
}
$("#box").eat();

// 3.
$.fn.extend({
    move:function() {
        console.log("开始移动");
    },
    speed:20
});
$("#box").move();  // 开始移动
console.log($.fn.speed);  // 20
```

### 4.核心

#### .each() 遍历一个jQuery对象，为每个匹配元素执行一个函数。

- 为每个选中的元素执行一次函数

```html
<div class="nav-item">
        <a href="#" class="item">小米手机</a>
        <a href="#" class="item">红米</a>
        <a href="#" class="item">平板 · 笔记本</a>
        <a href="#" class="item">电视</a>
        <a href="#" class="item">盒子 · 影音</a>
        <a href="#" class="item">路由器</a>
        <a href="#" class="item">智能硬件</a>
        <a href="#">服务</a>
        <a href="#">社区</a>
</div>
<script>
//此处的index为 从0开始的计数。。。。console.log(index);的结果为0~6
$(".nav-item a.item").each(function(index){
  		//此时用eq(index)选中0~6对应的标号
      	$(".nav-item a.item").eq(index).mouseover(function(){
        //显示nav-bottom
        $(".nav .nav-bottom").show();
      	//显示nav-bottom 中对应的li
        $(".logobox-bottom .items").eq(index).addClass("active").siblings().removeClass("active");
          });    
    });
</script>
<!--
	结果是为每个item的ａ标签执行一个函数
	每移动到一个a标签都会使对应的隐藏导航显示
-->
```

#### context 上下文

```javascript
// $():参数2,context 上下文
// 找 #box 下的 p
$("p","#box").css("backgroundColor","lightblue");

console.log($("p",box));  // r.fn.init(2)
console.log($("p","#box"));  // r.fn.init(2)
```

#### Jquery 文档加载完成回调

```javascript
// jQuery(callback);
$(function() {
    // 文档就绪
});

$(document).ready(function() {
    // 文档就绪
});
```

#### get() 获取原生对象

```javascript
// jq转换为原生
$("#box p").get(1).style.fontSize = "30px";
// 不给参数,返回数组,获取选中的元素数组
console.log($("#box p").get());
$("#box p").get().reverse()[0].style.color = "pink";
```

#### index() 获取匹配元素的索引值 从0开始

```javascript
<ul>
  <li id="foo">foo</li>
  <li id="bar">bar</li>
  <li id="baz">baz</li>
</ul>
$('li').index(document.getElementById('bar')); //1，传递一个DOM对象，返回这个对象在原先集合中的索引位置
$('li').index($('#bar')); //1，传递一个jQuery对象
$('li').index($('li:gt(0)')); //1，传递一组jQuery对象，返回这个对象中第一个元素在原先集合中的索引位置
$('#bar').index('li'); //1，传递一个选择器，返回#bar在所有li中的索引位置
$('#bar').index(); //1，不传递参数，返回这个元素在同辈中的索引位置。
```

