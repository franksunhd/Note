## jQuery中的DOM操作

[TOC]

```html
<!--
    DOM操作 === 节点操作  === 标签操作  === 元素操作
-->
```

### 1.内部插入

#### .append()

- 在每个匹配元素**里面的末尾处**插入参数内容。

```html
<div class="one">
      <h2>我是第一个one</h2>
</div>
//在选中元素的里边的最后边！！！！！
    $("body").append("<h1>通过append方法追加到了body的尾部</h1>");
    $(".one").append("<p>追加的内容</p>");
	$(".one").append("<h2></h2>");	//h2内容为空
```

#### .appendTo()

- 将匹配的元素**内部插入**到目标元素的最后面。

```html
<div class="two"></div>
//将前边的<h2>标签的内容插入到 .two 的内部的末尾
$("<h2>appendTo追加</h2>").appendTo(".two");

//$("<p></p>") 叫做创建一个jQuery对象，可以理解为创建一个元素。
//(其实就是在原有标签的基础上做了一些改造)
    var newElement = $("<a href='https://www.baidu.com'>链接</a>");
    newElement.appendTo(".two");
```

#### .prepend ()

- 将参数内容插入到每个匹配**元素内部的前面**。

```html
<div class="three">
      <h2>three元素</h2>
</div>
//字符串类型		本来没有，在这创建了一个新的
$(".three").prepend("<p>hello three!!</p>");

// jQuery对象类型	是移除原来的，不是复制，移除之后原来的位置上没有了
$(".three").prepend($("<p>three hello</p>"));
```

#### .prependTo()

- 将所有元素插入到目标前面（元素内插到前）。

```html
<div class="three">
      <h2>three元素</h2>
</div>
//字符串类型		本来没有，在这创建了一个新的
$("<p>hello three!!</p>").prependTo(".three");

// jQuery对象类型	是移除原来的，不是复制，移除之后原来的位置上没有了
$("<p>hello three!!</p>").prependTo($(".three"));
```

#### .html()

- **获取**集合中第一个匹配元素的HTML内容 或 **设置**每一个匹配元素的html内容。

```html
//修改标签内容(设置)
$(".four > h2").html("<span>我是h2</span>");
$(".four > h2").html("xxxxx");

//获取内容
$('div.demo-container').html();
```

#### .text()

- 得到匹配元素集合中每个元素的文本内容结合，包括他们的后代，或设置匹配元素集合中每个元素的文本内容为指定的文本内容。

```html
<div class="demo-container">
      <div class="demo-box">Demonstration Box</div>
  <ul>
  <li>list item 1</li>
  <li>list <strong>item</strong> 2</li>
  </ul>
</div>
$('div.demo-container').text();	
//结果为：Demonstration Box list item 1 list item 2
```

### 2.外部插入

#### .before()

- 根据参数设定，在匹配元素的前面插入内容

```html
<div class="one">one</div>
    <div class="one">one</div>

    <ul class="two">
      <li>1</li>
      <li>2</li>
      <li>3</li>
</ul>

<script type="text/javascript">
$(".one").before("<h2>兄弟！</h2>");
$(".two li:eq(1)"). before("<li>临时添加</li>")		//指定在第二个li前添加
</script>
```

#### .insertBefore()

- 在目标元素前面插入集合中每个匹配的作为目标元素的兄弟元素。(翻转，外部插兄弟)

```html
<div class="three">
      <h2>three</h2>
</div>

<script type="text/javascript">
$("<h3>three!!!!</h3>").insertBefore(".three > h2");
</script>
```

#### .after()

- 在匹配元素集合中的每个元素后面插入参数所指定的内容，作为其兄弟节点。

```html
<div class="one">one</div>
    <div class="one">one</div>

    <ul class="two">
      <li>1</li>
      <li>2</li>
      <li>3</li>
</ul>

$(".one").after("<h2>兄弟！</h2>");
$(".two li:eq(1)").after("<li>临时添加</li>");	//指定在第二个li后添加
```

#### .insertAfter()

- 在目标元素后面插入集合中每个匹配的作为目标元素的兄弟元素	(翻转,外部插兄弟)

```html
<div class="three">
      <h2>three</h2>
</div>

<script type="text/javascript">
$("<h3>three!!!!</h3>").insertAfter(".three > h2");
</script>
```

### 3.移除元素

#### .remove()

- 将匹配元素集合从DOM中删除(子元素及其本身全部丢失)

```html
<div class="one">
      <div class="one_s">xxx</div>
      <div class="one_s">xxx</div>
      <div class="one_s color_red">yyyy</div>
      <p class="color_red">yyyy</p>
</div>
//两种方法
$(".one_s.color_red").remove();			//一次选择
// $(".color_red").remove(".one_s");	//选择两次
```

#### .empty()

- 从DOM中移除集合中匹配元素的所有子节点。(删除所有子，自己还在)

```html
<ul class="two">
      <li>1</li>
      <li>2</li>
      <li>3</li>
</ul>
//删除所有子节点，但是自己的节点仍然存在
$(".two").empty();
```

#### .detach()

- 从DOM中去掉所有匹配的元素。(保存删除，并没有真正删除，还可以找回)

```html
<div class="three">
      <h2>three</h2>
</div>
//保存一下已经删除的元素，便于将来继续使用！！！！
    var temp = $(".three:eq(0)").detach();
    console.log(temp);//已经删除的元素
   
    $("body").prepent(temp);	//找回并添加到body标签内部的开头
```

#### .unwrap()

- 将匹配元素集合的**父级元素删除**，保留自身（和兄弟元素，如果存在）在原来的位置。

```html
<div>
  <button type="button" name="button">点我</button>
  <button type="button" name="button">点我</button>
</div>
<button type="button" name="button">点我</button>

//选择button标签，删除父级的div标签
$("button").unwrap();
```

### 4.包裹

#### .wrap()

- 在集合中匹配的每个元素周围包裹一个HTML结构。(每个包裹一层)
- .wrap()函数可以接受任何字符串或对象，可以传递给$()工厂函数来指定一个DOM结构。

```html
 <h2 class="one">one</h2>
 <h2 class="one">one</h2>

<script src="../jquery.min.js" charset="utf-8"></script>
<script type="text/javascript">
  //给符合条件的元素都包裹,在元素的外部包裹
    $(".one").wrap("<div></div>");
  
  $('p').wrap(document.createElement('div'));
</script>>  
```

#### .wrapAll()

- 在集合中所有匹配元素的外面包裹一个HTML结构。(集体包裹一层)
- .wrapAll()函数可以接受任何字符串或对象，可以传递给$()工厂函数来指定一个DOM结构.

```html
	<li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
//整体包裹	给li标签包裹一层ul标签
    $("li").wrapAll("<ul class='lists'></ul>");
```

#### .wrapInner()

- 在匹配元素里的**内容**外包一层结构。	(给匹配元素的内容做包裹)

```html
<div class="two">文本</div>
<div class="two">文本</div>

<script src="../jquery.min.js" charset="utf-8"></script>
<script type="text/javascript">
  //给符合条件的元素都包裹,在元素的内部包裹
    $(".two").wrapInner("<h2></h2>");		//给文本加包裹
</script>
```

### 5.替换

#### .replaceWith()

- 用提供的内容替换集合中所有匹配的元素并且返回被删除元素的集合。

```html
<div class="four">
      <h2>1</h2>
      <h2>2</h2>
      <h2>3</h2>
    </div>
//
$(".four>h2").replaceAll("<div>son</div>");
```

#### .replaceAll()

- 用集合的匹配元素替换每个目标元素。	(翻转，替换所有)

```html
<div class="four">
      <h2>1</h2>
      <h2>2</h2>
      <h2>3</h2>
    </div>
//翻转
$("<div>son</div>").replaceAll(".four>h2");
```

### 6.克隆

#### .clone()

- 创建一个匹配的元素集合的深度拷贝副本。	(只是复制，原来的没有移除)

```html
<div class="container">
  <div class="hello">Hello</div>
  <div class="goodbye">Goodbye</div>
</div>
//克隆Hello，添加到.goodbye的内部末尾
$("hello").clone().appendTo(".goodbye");
```

























