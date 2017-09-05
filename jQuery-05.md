## jQuery中的遍历

[TOC]

### 1.树遍历

#### .parent() 获取每个元素的父元素

- 取得匹配元素集合中，每个元素的父元素，可以提供一个可选的选择器。

```javascript
$(this).parent().remove();
```

#### .children() 获得匹配元素集合中每个元素的子元素

```html
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

#### .prev() 获取集合中每个匹配元素紧邻的前一个兄弟元素。 

- 如果提供了一种选择器，它将只检索匹配该选择器的紧邻的前一个兄弟元素。

```html
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

### 2.各种遍历

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

