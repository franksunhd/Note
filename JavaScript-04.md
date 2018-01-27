## JS 对象/HTML DOM对象/Browser 对象

[TOC]

### JS Functions(全局对象)

- 全局属性和函数可用于所有内建的 JavaScript 对象。

#### (顶层函数)全局函数--数值转换

##### isNaN() 检查某个值是不是数字

- isNaN(x) x是必须值,是为要检测的值,如果转换是NaN,则直接输出true.否则输出false.

##### parseInt() 函数可解析一个字符串，并返回一个整数。

- parseInt(string);返回解析后的整数。

```javascript
console.log(parseInt(""));				//NaN
console.log(parseInt("1234abc"));		//1234
console.log(parseInt("abc"));			//NaN
console.log(parseInt("10.123"));		//10
console.log(parseInt("0x12"));			//18

console.log(parseInt("070"));			//70, 并没有解析为８进制
console.log(parseInt("010", 8));		//8
console.log(parseInt("10", 2));			//2
console.log(parseInt("20",2));			//超过范围时，转换为NaN
console.log(parseInt("17", 8));			//15
console.log(parseInt("10", 10));		//10
console.log(parseInt("10", 16));		//16

console.log(parseInt("010"));			//10
```

##### parseFloat() 函数可解析一个字符串，并返回一个浮点数。

- parseFloat(string);返回解析后的浮点数字。

```javascript
document.write(parseFloat("10")); 		//返回 10
document.write(parseFloat("10.00")); 	//返回 10.00
document.write(parseFloat("10.33")); 	//返回 10.33
document.write(parseFloat("34 45 66")); //返回 34
document.write(parseFloat(" 60 ")); 	//返回 60
document.write(parseFloat("40 years"));	//返回 40
document.write(parseFloat("He was 40"));//返回 NaN

<!--结果都为 3.14-->
document.write(parseFloat("3.14")) 
document.write(parseFloat("314e-2")) 
document.write(parseFloat("0.0314E+2")) 
document.write(parseFloat("3.14more non-digit characters")) 
```

##### String() 函数  把对象的值转换为字符串。

```javascript
var a=123;
var b=true;
var c;
var d=null;

console.log(String(a));	//123
console.log(String(b));	//true
console.log(String(c));	//undefined
console.log(String(d));	//null
```

##### String() 和 toString()的区别

- 首先,两者都是把其他类型的变量转换为字符串的方法
- 其次,toString()无法转换null类型和undefined类型

```javascript
var a=123;
var b=true;
var c;
var d=null;
console.log(a.toString());    //123
console.log(b.toString());    //true
// console.log(c.toString()); //会报错
// console.log(d.toString()); //会报错

console.log(String(a));        //123
console.log(String(b));        //true
console.log(String(c));        //undefined
console.log(String(d));        //null
```

##### Number()  把对象的值转换为数字。

```javascript
var test1= new Boolean(true);
var test2= new Boolean(false);
var test3= new Date();
var test4= new String("999");
var test5= new String("999 888");

//javascript Date对象
document.write(Number(test1)+ "<br />"); 	//1
document.write(Number(test2)+ "<br />");    //0
document.write(String(test3)+ "<br />");    
//Sun Sep 03 2017 20:53:22 GMT+0800 (CST)

document.write(Number(test3)+ "<br />");    //1504443202548
document.write(Number(test4)+ "<br />");    //999
document.write(Number(test5)+ "<br />");    //NAN
```
#### 数值转换实例

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>number转换</title>
  </head>
  <body>

    输入： <input id="one" type="text" >
    <button id="btn">点击转换为数字</button>
    <h1>Number转换结果：<span id="show1"></span></h1>
    <h1>parseInt转换结果：<span id="show2"></span></h1>
    <h1>parseFloat转换结果：<span id="show3"></span></h1>


    <script type="text/javascript">
    var input = document.getElementById('one');
    var btn = document.getElementById('btn');
    var show1 = document.getElementById('show1');
    var show2 = document.getElementById('show2');
    var show3 = document.getElementById('show3');

    btn.onclick = function() {
      // input输入框中的内容都是字符串形式，
      // 使用Number转成数字
      var result = Number(input.value);
      console.log(result);
      show1.innerHTML = result;

      // input输入框中的内容都是字符串形式，
      // 使用parseInt转成数字(整数),还可以指定进制去转换
      result = parseInt(input.value);
      // result = parseInt(input.value, 2);
      // result = parseInt(input.value, 8);
      // result = parseInt(input.value, 16);
      console.log(result);
      show2.innerHTML = result;

      // input输入框中的内容都是字符串形式，
      // 使用parseFloat转成 小数点
      result = parseFloat(input.value);
      console.log(result);
      show3.innerHTML = result;
    }
    </script>
  </body>
</html>
```

### JS Date对象

- Date 对象用于处理日期和时间

```javascript
var myDate=new Date();
//注释：Date 对象会自动把当前日期和时间保存为其初始值。

//javascript Date对象
document.write(Date("1504443202548")+ "<br />");
//输出结果为: Sun Sep 03 2017 20:53:22 GMT+0800 (CST)

//转换格式为:=TEXT((B1/1000+8*3600)/86400+70*365+19,"yyyy-mm-dd hh:mm:ss")
- (2017年)转换Excel将时间戳转换为日期格式的算法
- 从 1970-01-01 08:00:00开始,使用 10位/13位的数进行表示,每增加 1或者 1000,时间增加 1秒.(格林威治时间)
```

```javascript
var mDate = new Date();
// 输出本机当前的 时间
console.log(mDate);
// 输出当前 年代
console.log(mDate.getFullYear() + "年");
// 输出当前 月份
console.log(mDate.getMonth()+1 + "月");
// 输出当前 日期
console.log(mDate.getDate() + "日");
// 输出当期 小时
console.log(mDate.getHours() + "时");
// 输出当前 分钟
console.log(mDate.getMinutes() + "分");
// 输出当前 秒
console.log(mDate.getSeconds() + "秒");
```

未完....

### JS Array对象

- Array 对象用于在单个的变量中存储多个值。

```javascript
var aArray = new Array();
var aArray = new Array(size);
var aArray = new Array(element0, element1, ..., elementn);
```

- **参数**
  - 参数 *size* 是期望的数组元素个数。返回的数组，length 字段将被设为 *size* 的值。
  - 参数 *element* ..., *elementn* 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。


- **返回值**
  - 返回新创建并被初始化了的数组。
  - 如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。
  - 当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为 undefined 的数组。
  - 当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。
  - 当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。

未完....

### JS Boolean对象

- Boolean 对象表示两个值："true" 或 "false"。

```javascript
new Boolean(value);	//构造函数
Boolean(value);		//转换函数

var boo = new Boolean(true)
document.write(boo.toString())
```

未完....

### JS Math对象

- Math 对象用于执行数学任务。

```javascript
var pi_value=Math.PI;
var sqrt_value=Math.sqrt(15);

//不能直接传递数组
console.log(Math.max([1,2,3,5,10,-1,88]));

//使用apply对Math.max进行改造，然后可以传数组
console.log(Math.max.apply(null, [1,2,3,4,4,88]));
```

```javascript
// 输出PI的值
console.log(Math.PI);
// 输出三个数中的最小数
console.log(Math.min(12,22,32));
// 输出三个数中的最大数
console.log(Math.max(12,22,32));
// 四舍五入
console.log(Math.round(12.49));
console.log(Math.round(12.50));
// 向上取整
console.log(Math.ceil(12.1));
// 向下取整
console.log(Math.floor(12.9));
// 0~1之间的随机数(不包括0和1)
console.log(Math.random());
// 1~100之间的随机数(包括1和100)
console.log(Math.floor(Math.random()*100+1));
```

```javascript
// 产生 6 个 0 - 10之间的不重复的 随机数
// 方法一 :  封装函数
// 1. 封装查找数组中有没有指定元素
		function find(arr, obj) {  
	        var i = arr.length;  
	        while (i--) {  
	            if (arr[i] === obj) {  
	                return true;  
	            }  
	        }  
	        return false;  
	    }

	    btn1.onclick = function () {
	    	var count1 = 0;
	    	var arr1 = [];  // 存放6个元素的数组
	    	while(1){
	    		var Randomnum = Math.floor(Math.random() * 10 + 1);
	    		var m = find(arr1,Randomnum);
	    		if(m === false){
	    			arr1.push(Randomnum);
	    			count1++;
	    			if (count1 === 6) {
	    				break;
	    			}
	    		}
	    	}

	    	item1.innerHTML = arr1;
	    }
 // 方法二 :  $.inArray(value,array)
        btn2.onclick = function () {
	    	var count2 = 0;
	    	var arr2 = [];  // 存放6个元素的数组
	    	while(1){
	    		var Randomnum = Math.floor(Math.random() * 10 + 1);
	    		
	    		// 2.jQuery inArray(value,array);  返回值 没有为 -1
	    		var m1 = $.inArray(Randomnum,arr2);
	    		console.log(m1);
	    		if(m1 === -1){
	    			arr2.push(Randomnum);
	    			count2++;
	    			if (count2 === 6) {
	    				break;
	    			}
	    		}
	    	}

	    	item2.innerHTML = arr2;
	    }
  // 方法三:
function Random(len, min, max) {
var arr = [];
var json = {};
while (arr.length < len) {
//产生单个随机数
var num = Math.floor(Math.random() * (max - min + 1)) + min;
//通过判断json对象的索引值是否存在 来标记 是否重复
if (!json[num]) {
	json[num] = 1;
	arr.push(num);
	}
}
return arr;
}
console.log(Random(6, 0, 10)); //生成6个从0-10之间不重复的随机数

// 方法四:
var arr = [];
while(arr.length <= 6){
		var num = Math.floor(Math.random() * 11);
		if(arr.indexOf(num) == -1){
			arr.push(num)
		}
	}
alert(arr);
```

未完...

### JS Number对象

- Number 对象是原始数值的包装对象。

```javascript
var myNum=new Number(value);
var myNum=Number(value);

var num1 = Number("Hello world!"); 	//NaN
var num2 = Number("");				//0
var num3 = Number("000011");		//11
var num4 = Number(true);			//1
```

未完...

### JS String对象

- String 对象用于处理文本（字符串）。

```javascript
var sString = new String(s);
var sString = String(s);
```

未完...

### JS RegExp对象

- RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具。

```javascript

```

未完....

## HTML DOM对象

DOM(文档对象模型)是指针对HTML和XML文档的一个API(应用程序编程接口).DOM脱胎于网景公司和微软创始的DHTML(动态HTML).

### 文档对象模型

```javascript
// DOM:文档对象模型
// document: 文档对象
// DOM 属性结构: document -> html-> 各节点组成

// 常用的节点:
/*
	1.元素节点 <div></div> 	nodeType=1
    2.属性节点  id  class 	nodeType=2
    3.文本节点				nodeType=3
    4.注释节点				nodeType=8
    5.根节点 document 		 document.nodeType=9
    6.<!DOCTYPE html>       document.doctype.nodeType=10
*/

// 1.document
console.log(document);  // 文档对象

// 2.documentElement html对象
console.log(document.documentElement);  
// 没有<!DOCTYPE html> html对象

console.log(document.html);  // undefined 未定义,不这么写
// 3.head
console.log(document.head);		// head 对象
// 4.body
console.log(document.body);		// body 对象

var box = document.getElementById('box');
// nodeName 标签名
// nodeType 节点类型
// nodeValue 节点值
// 每个节点都具有这三个属性
console.log(box.nodeName,box.nodeType,box.nodeValue);  // DIV 1 null
// 5.node.childNodes 元素所有子节点
console.log(box.childNodes);

// 6.Node.parentNode 获取节点的父节点
console.log(document.body.parentNode);		// html 对象

// document 对象 是这个文档的根节点吗,没有父节点,输出为空
console.log(document.parentNode);  // null

var nodeT = box.childNodes[0];
// #text 代表文本节点  3代表节点类型为文本节点
console.log(nodeT.nodeName,nodeT.nodeType,nodeT.nodeValue);  // #text 3
var nodeC = box.childNodes[1];
console.log(nodeC.nodeName,nodeC.nodeType,nodeC.nodeValue);  // #comment 8 注释1
// 根节点: document
console.log(document.nodeName,document.nodeType,document.nodeValue);  // #document 9 null
// <!DOCTYPE html> 声明节点  html 10 null
console.log(document.doctype.nodeName,document.doctype.nodeType,document.doctype.nodeValue);  // html 10 null

// 7.属性节点
// attributes 获取所有的属性节点
console.log(box.attributes);

console.log(box.attributes[0].nodeName);  // id
console.log(box.attributes[0].nodeType);  // 2
```

### 节点访问(父/兄/子)

```javascript
// 1.获得父节点
document.parentNode  // 输出为空 document对象是根节点,没有父节点
one.parentNode

// 2.兄弟节点
one.nextSibling  // 将文本节点也识别为兄弟
one.nextElementSibling  // 只识别标签作为自己的兄弟

one.previousSibling  // 访问元素的上一个节点,包括文本节点
one.previousElementSlibing  // 访问元素的上一个元素节点

// 3.firstChild 选择的是第一个子节点,其中可包括文本节点
// 所有浏览器都支持,标准浏览器下返回第一个节点(可以是文本节点或者注释节点)
// IE 6,7,8下返回第一个 元素节点(不包括文本节点等)
console.log(box.firstChild);  // 文本节点

// 4.firstElementChild() 选择第一个元素子节点
// 只有标准浏览器支持, IE 下的为 undefined
// 返回的是第一个 元素节点
box.firstElementChild.style.fontSize = "30px";
console.log(box.firstElementChild);

// 获取第一个子元素的兼容写法
function firstEle(ele) {
    return ele.firstElementChild || ele.firstChild;
}

one.lastChild  // 访问元素的最后一个子节点,包括文本节点
one.lastElementChild  // 访问元素的最后一个 子元素节点

// last:特点同上
function lastEle(ele) {
    return ele.lastElementChild || ele.lastChild;
}

// 5.直接子元素集合
// children属性,获取所有的子代元素
// 不是标准写法,但是所有浏览器都支持
console.log(box.children);

one.children[2]  // 不包含文本节点
one.children[4]
```

### 获得节点( ID/ClassName/TagName/querySelector)

```javascript
document.getElementById("id");
document.getElementsByTagName("div");
document.getElementsByClassName("test");

// JS 新增的选择器,只有标准浏览器支持
// 1. querySelector()
// 参数 : 选择器
// 返回 : 元素,及时有多个元素也只是返回第一个元素
var box1 = document.querySelector("div#box");
console.log(box1);

// 2. querySelectorAll() 返回的是一个集合
// 参数 : 选择器
// 返回 : 元素集合  [元素对象]
var p1 = document.querySelectorAll("#box > p");
console.log(p1);
p1[0].style.fontSize = "30px";
```

### 创建节点(createElement/createTextNode/createComment)

```javascript
// 1.创建元素节点
var test = document.createElement("div");
// 2.创建文本节点
var textNode = document.createTextNode("百度一下,你就知道!");
console.log(textNode, typeof(textNode));  // 文本  "Object"
// 3.创建节点注释
var com = document.createComment("这是注释");
// 调用两次,只有后边的设置有效
ele.appendChild(com);
box.appendChild(com);
```

### 操作节点(appendChild/insertBefore/replaceChild/removeChild)

```javascript
// 插入操作
// 1. 把元素绘制到 dom 中
box.appendChild(ele);

var sEle = document.createElement("strong");
var sEle1 = document.createElement("strong");
sEle.innerText = "strong标签";
sEle1.innerText = "strong标签";
box.appendChild(sEle);
box.appendChild(sEle1);

// 2. box.insertBefore()
// 参数1:新元素
// 参数2:参照元素
var Img = document.createElement("img");
Img.src = "./img/favicon.ico";
Img.style.width = "30px";
box.insertBefore(Img,sEle);

// 3. replaceChild(新元素,旧元素);
// 参数1:新元素
// 参数2:参照元素,要替换的旧元素
box.replaceChild(Img,sEle1);
//替换节点(被替换的节点还在文档中,但是在文档中已经没有了自己的位置)

// 4.删除子元素
box.removeChild(Img);
//移除节点(要移除的节点还在文档中,但是在文档中已经没有了自己的位置)

// 5.remove() 删除全部元素
box.remove();
```

### 节点属性相关(操作属性的方式/getAttribute/setAttribute)

```javascript
/*
 * 操作属性的方式:
 * 		元素对象自定义的属性,和行间自定义属性没有关联,不能渲染到文档
 * 1.点语法 可以获取或者设置行间系统的属性
 * 2.元素对象[""]  可以放置变量,不能去引号,去掉引号被认为是变量
 * 3.getAttribute() 获取文档中系统或者自定义的属性
 * 4.setAttribute() 设置文档中系统或者自定义属性都可以加载到文档中
 * 5.hasAttribute("") 判断元素有没有当前的属性
 * 6.hasAttributes() 判断元素有没有设置属性 
 */
<div id="box" class="BoxName" name="NameBox" age="123" style="background-color:red;">
    <!-- 注释1 --><!-- 注释2 -->
    文本节点
    <p>p标签</p>
</div>

var box = document.getElementById('box');

console.log(box);

// 1. 点语法
console.log("------点语法------");
console.log(box.id,box.className);
box.name = "box1";
console.log(box.id,box.name);

// 点语法无法获得自定义的属性
console.log(box.age);  // undefined

// ?!重点难理解!?
// 元素对象自定义的属性,和行间自定义属性没有关联,不能渲染到文档
box.age = "20";
box.sex = "男";
console.log(box.age);  // 20 能打印不能喧染到文档

console.log("------元素对象[]------");
// 2.元素对象[] 不能去引号,去掉引号被认为是变量
console.log(box["id"]);  // box

console.log("------getAttribute() 获取属性值------");
// 3.获取属性值
console.log(box.getAttribute("age"));   // (自定义属性) 123
console.log(box.getAttribute("style"));   // (系统属性) background-color:red;
console.log(box.getAttribute("sex"));   // null

// 获取 class 标准浏览器使用 class  IE 6,7,8 使用 className
console.log(box.getAttribute("class"));   // Boxname

// 4.设置: 系统或者自定义的属性都可以被加载到文档中
box.setAttribute("sex","男");

// 5.获取元素的所有属性节点
console.log(box.attributes);

// 6.判断有没有 某个属性 有返回 true
console.log(box.hasAttribute("age"));

// 7.判断元素有没有设置属性 设置返回 true
console.log(box.hasAttributes());
```

### 获取样式(style/getComputedStyle/currentStyle)

```javascript
/* 
	getAttribute 和 style 的区别
	1).getAttribute 是获取元素的属性, style是获取元素的 style中的行间样式
	2).getAttribute 可以获取元素的自定义属性,比如name,age等
	3).style 是获取的 style 中的 width,height 等属性.
*/

// 1.node.style 的方式只能够获取 元素的行间样式
console.log(box.style.height,typeof(box.style.height)); 
// 300px string

// 2.标准浏览器中的方法: getComputedStyle(元素对象,参数2)
//  返回该元素对象的所有样式
//  可以获取到  行间样式 ,也可以获取到  嵌套样式
//  参数2:伪类/伪元素的名字,一般省略或者给null
//  IE8 以下的浏览器  currentStyle

var a = window.getComputedStyle(box,null);
console.log(a);

console.log(a.height);  // 300px
console.log(a.backgroundColor);  // rgb(0,0,255)

var b = window.getComputedStyle(box,":before");
console.log(b,typeof b);  // object
console.log(b.content);	// 通过参数2获取
console.log(b.height);  // 100px

function getStyle(ele,attr) {
// 兼容性写法
return ele.currentStyle ? ele.currentStyle[attr]: getComputedStyle(ele)[attr];

// 2. 判断浏览器有没有这个方法,前边加 window 且不能省略
return window.getComputedStyle ? getComputedStyle(ele)[attr] : ele.currentStyle[attr];
}
```

### 克隆节点(cloneNode)

```javascript
var a = document.getElementById(“id”);
var clone = a.cloneNode(true);

// 只能克隆元素,无法克隆事件

/*
创建副本节点
  {
  true 深复制,复制节点及其整个子节点树
  flase 浅复制,只复制节点本身
  不复制添加到DOM节点中的js属性
  }
*/
```

### 处理文本节点(normalize)

```javascript
normalize() //处理文档树中的文本节点
// 调用该方法:后代节点遇到 空文本节点,就删除;遇到多个相邻的文本节点合并为一个文本节点.
```

### innerHTML 遗留问题/效率问题

```javascript
// innerHTML赋值,会覆盖掉 box 中子元素绑定的事件, box中的布局会被重新绘制
<div id="box">
	<p>文本</p>
	<button>按钮</button>
</div>
<hr>
<p>
	<button id="bCreate">开始创建1</button>
</p>
<script type="text/javascript">
  var box = document.querySelector("#box");
  var bCreate = document.querySelector("#bCreate");
  var btn = document.querySelector("#box button");

  var pEle = document.createElement("p");
  var textNode = document.createTextNode("百度一下,你就知道!");

  pEle.appendChild(textNode);

  btn.onclick = function() {
      alert("box内按钮");
  };

  bCreate.onclick = function() {
      // innerHTML赋值,会覆盖掉 box 中子元素绑定的事件, box中的布局会被重新绘制
      box.innerHTML += "<p>新的元素</p>";
      // 如果单独的 appendChild 点击按钮是只添加一次
      // 加上 innerHTML 相当于每次都会重新绘制元素在界面的显示, appendChild就是每次都追加
      box.appendChild(pEle);
  }
</script>
```

```javascript
<div id="box"></div>
<script type="text/javascript">
    console.time("浪哥")
    var content = "";
    for (var i = 0; i < 900; i++) {
        // 创建 cell
        // appendChild  2-3ms
        // var cell = document.createElement("div");
        // cell.className = "cell";
        // box.appendChild(cell);

        // 错误 : innerHTML  500-900ms
        // box.innerHTML += "<div class='cell'></div>";

        // 解决:文档碎片 1ms-3ms
        content += "<div class='cell'></div>";
    }
    box.innerHTML = content;
    console.timeEnd("浪哥");
</script>
```

