## JavaScript 变量声明/数据类型/语句/函数声明

[TOC]

[**Google JavaScript 编码规范指南**](http://s.sxt.cn/u/352/blog/7152)

###　1、浏览器内核

> 　Trident

- Trident(IE内核):该内核程序在1997年的IE4中首次被采用，并沿用到IE11，也就普遍称为“IE内核”。

> 　Gecko

- Gecko(Firefox内核):特点是代码完全开放，可开发程度很高，全世界的程序员都可以为其编写代码，增加功能。

> 　Presto(已废弃)

- Presto(Opera前内核):它的引擎渲染速度的优化达到极致，但却牺牲了网页的兼容性。

> 　Webkit

- Webkit(Safari内核，Chrome内核原型，开源):它是苹果公司自己的内核，也是苹果的Safari浏览器使用的内核。

> 　Blink

- Blink (Google内核) 源自 WebKit，是从它衍生出自己的 Blink 引擎

### 2、JavaScript的组成部分

> **ECMAScript**

- 描述该语言的语法和基本对象

> **浏览器对象模型(bom)**

- 描述与浏览器进行交互的接口和方法

> **文档对象模型(dom)**

- 描述处理网页内容的方法和接口

  ![](https://nts.newbieol.com/static/k111/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/class-005/image/js.jpg)

### 3、JavaScript的用途(作用)

- 嵌入动态文本于HTML页面中
- 对浏览器事件做出响应
- 读写HTML元素
- 在数据被提交到服务器之前验证数据
- 检测访客的浏览器信息
- 控制cookjes，包括创建和修改
- 基于Node.js技术进行服务器端编程

### 4、JavaScript语言的特点

>​	JavaScript一种**直译**式**脚本语言**，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的**解释**器被称为JavaScript引擎，为**浏览器**的一部分，广泛用于**客户端**的脚本语言，最早是在**HTML**（**标准通用标记语言**下的一个应用）网页上使用，用来给**HTML网页**增加动态功能。(百度百科)
>
>​	JavaScript是一种属于网络的脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各式各样的动态功能,为用户提供更流畅美观的浏览效果。通常JavaScript脚本是通过嵌入在HTML中来实现自身的功能的。



>>1.是一种解释性脚本语言（代码不进行预编译）。
>>2.主要用来向HTML（标准通用标记语言下的一个应用）页面添加交互行为。
>>3.可以**直接**嵌入HTML页面，但写成单独的js文件有利于结构和行为的**分离**。
>>4.跨平台特性，在绝大多数浏览器的支持下，可以在多种平台下运行（如Windows、Linux、Mac、Android、iOS等） 

名词解释：

- 直译：直接进行解析
- 脚本语言：解释执行，不需要编译
- 动态类型：可以在程序运行的期间动态的改变代码的结构和变量类型
- 基于原型的面向对象：JS的世界没有类，永远都是**对象创建对象**
- 弱类型：对象的声明没有类型，动态语言的体现

### 5、第一个简单的JS程序

- 创建一个web项目，填写对应的项目名称
- 创建一个HTML文件
- 声明一个JS代码块 (<script></script>)
- 开始书写JS代码

输出一个Hello world程序：

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>Hello world</title>
  <!-- script 代码块 -->
  <script type="text/javascript">
    //声明一个str变量
    var str = "Hello world";
    //声明一个sayhello()函数
    function sayhello() {
      //打印语句
      alert(str);
    };
  </script>
  <style media="screen">
    * {
      margin: 0;
      padding: 0;
    }
  </style>
</head>
<body>
  <h1>欢迎您进行JavaScript的学习</h1>
  <!--
      事件驱动  onclick 鼠标单击事件
              ondblclick 鼠标双击事件
  -->
  <input type="button" name="" value="测试事件驱动" onclick="sayhello();" />
  <!-- <input type="button" name="" value="测试事件驱动" ondblclick="sayhello();" /> -->
  <pre>
    JS代码从上到下解释执行
  </pre>
</body>
</html>
```

- 整体剖析代码
  - 代码块(script)
  - 变量 (str)
  - 函数(function)
  - 打印语句(alert)
  - 事件驱动(onclick)

### 6、JavaScript的代码注释

- JavaScript不会执行注释部分
- 注释可以提高代码的可读性
- 还可以提高代码的维护性
- 注释可以阻止代码的执行

  > **注释的分类**(**不要和其他的注释混淆**)
  >
  > html的注释<!-- -->
  >
  > css的注释		//	/**/
  >
  > JavaScript的注释 	//	/**/

#### 单行注释(//)

- 单行注释可以描述简单的问题

```javascript
<script type="text/javascript">
    //声明一个str变量
    var str = "Hello world";
    //声明一个sayhello()函数
    function sayhello() {
    //打印语句
      alert(str);
    };
  </script>
```

#### 多行注释(/*     */)

- 可以同时注释多行代码，也可以同时解除对多行代码的注释

```javascript
<script type="text/javascript">
    /*
    	声明一个str变量
    */
    var str = "Hello world";
    /*
    	声明一个sayhello()函数
    */
    function sayhello() {
     /*
      	打印语句
     */
      alert(str);
    };
  </script>
```

#### 函数注释

```javascript
<script type="text/javascript">
    var str = "Hello world";
    /**
    *	函数说明(功能)
    *	@param{String} id 参数说明
    *	@param{REgExp} reg 参数说明 
    *	返回值：默认没有返回，undefined
    */
    function sayhello(aaa,bbb) {
      alert(str);			
      console.log(str);			//控制台输出
    };
  </script>
```

### 7、JavaScript编写方式

#### 行内JavaScript

```html
<button onclick="alert('helloworld!');">点我</button>
```

#### 嵌套JavaScript

```html
<script>
      alert("我是提示框！！！！");
</script>
```

#### 引入外部js脚本

```html
<script type="text/javascript" src="外部js文件路径"></script>
```

例如：去掉字符串中的空格     "    ab      cd     "

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>引入JS文件</title>
  <script type="text/javascript" src="./js/uilt.js"></script> 
  <script type="text/javascript">
    //声明一个字符串，方便测试去空格功能
    var str = "  ab cd   ";
    //测试去空格的方法
    alert("[" + str.trim() + "]");
  </script>
</head>
  <body>
      <h1>学习如何引入一个JS文件</h1> 
  </body>
</html>
```

```javascript
//实现去掉字符串右空格
String.prototype.rtrim = function() {
  return this.replace(/\s+$/ig , "");
};

//实现去掉字符串的左空格
String.prototype.ltrim = function() {
  return this.replace(/^\s+/ig , "");
};
```

### 8、变量的声明方式

#### JavaScript的变量

- 变量是存储信息的容器
- ECMAScript 的变量是  **松散类型**  的,所谓松散类型就是可以用来保存**任何类型的数据**。换句话说,每个变量***仅仅是一个用于保存值的占位符***而已。定义变量时要使用 **var** 操作符。　　

```javascript
//变量需要定义后才能使用
var  a, b;   				//定义一个变量,var是关键字,a,b是变量名(标识符)
var  c = 10, d = "hello";
console.log(d);				//console.log();用于控制台的输出
a = 10; 					//a开始是数值类型

a = "world"; 				//重新赋值变为字符串类型，可以，但是不推荐这样做。
							//再次使用变量时不需要var

console.log(typeof a);		//typeof 测试数据类型
function test(){
  var value = 234;			//局部变量,函数调用完毕之后立刻销毁
  test = "string";			//定义全局变量
  ....
}
```

#### 变量的作用域

> 区分：全局变量 和 局部变量
>
> - **javascript只有函数是用于区分作用域的，并不是{ }**
> - 如果在任何函数之外声明了一个变量,则该变量为**全局变量**,且该变量的值在整个持续范围内都可以访问和修改.
> - 如果在函数定义内部声明了一个变量,则该变量为**局部变量**,且每次执行该程序时都会创建和破坏该变量,且不能被函数外部的任何事物所访问.
> - 局部变量一定要以var声明,否则是全局变量.
>   - **局部变量只能在指定的作用内访问****全局变量在任意位置都可以访问**
> - 局部函数，默认只在能当前作用域内调用

```javascript
//全局变量
var uname = "zhangsan"; 			

//借助window对象声明全局变量
window.pwd = "123456";

function test()
{
  //如果声明变量的时候不加var, 那么在第一次使用之后就会变成全局变量
  email = "zhangsan@qq.com";
  
  //局部变量
  var realname = "张三";
  var age = 10;
  alert(uname + "++" + realname + "--" + pwd)
}

function testEmail() {
	alert("age");			//错误，无法访问局部变量
}			
```

> > 全局变量的三种声明方式:	var	/ window  / 局部变量声明声明时不加var.

#### 标识符

> ​	所谓标识符,就是指变量、函数、属性的名字,或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符:

- 第一个字符必须是一个字母、下划线( _ )或一个美元符号( $ )其他字符可以是字母、下划线、美元符号或数字。
- 标识符中的字母也可以包含扩展的 ASCII 或 Unicode 字母字符(如 À 和 Æ),但我们不推荐这样做。
- 按照惯例,ECMAScript 标识符采用驼峰大小写格式,也就是第一个字母小写,剩下的每个单词的首字母大写,例如: firstChild getSelectionText
- 不要和关键字重名

#### JavaScript的命名规范

- 变量必须以**字母**开头
- 变量也可以以$ 和_ 符号开头(不过不推荐这么做)
- 变量名称对大小写敏感(**y和Y是不同的变量**)
- JavaScript语句和JavaScript变量都对大小写敏感
- JavaScript中创建变量通常称为”声明变量“
- 变量可以使用短名称，也可以使用描述性更好的名称

#### JavaScript如何声明变量

- JS是一门弱类型的语言,所以变量的声明统一使用var;
- 变量声明之后,该变量是空的(它没有值);
- 可以在声明变量的时候对其进行赋值
- 可以在一条语句中声明多个变量,以语句var开头,并使用逗号作为分隔符.
- 如果重新声明JavaScript变量,该变量的值不会被覆盖.(针对同级,变量可以声明多次)



### 9、JavaScript数据类型

> ECMAScript 中有 **5 种简单数据类型**(也称为**基本数据类型**): 
>
> - Undefined  未定义类型
> - Null          Null类型
> - Boolean  布尔类型
> - Number  数值类型
> - String     字符串类型

对一个值使用 **typeof** 操作符可能返回下列某个字符串: 

> - typeof  测试变量类型;		console.log(typeof str1);
> - typeof  测试什么变量都不会报错，typeof没有错误

|   数据类型    |   描述    |
| :-------: | :-----: |
| undefined |   未定义   |
|  boolean  |   布尔值   |
|  string   |   字符串   |
|  number   |   数值    |
|  object   | 对象或null |
| function  |   函数    |

比如：

```javascript
//变量需要定义后才能使用 
 var a = "string";
 alert(typeof a); 							//string

 var b = 123;
 alert(typeof b); 							//number

 var c = true;
 alert(typeof c);							//boolean

 var d;
 alert(typeof d);							//undefined

 var f = function(){alert("hello");};
 alert(typeof f);							//function

 var e = null;
 alert(typeof e);							//object    
```

#### 未定义类型

> ​	Undefined 类型只有一个值,即特殊的 undefined 。在使用 var 声明变量但未对其加以初始化时,这个变量的值就是 undefined, 或者显式的进行undefined赋值操作，比如: 

```javascript
var a ;						//变量没有赋值，那么默认值为 undefined
var b = undefined;			//定义了变量，但是变量的值为undefined
console.log(typeof a);		// undefined(未定义)
console.log(typeof b);		// undefined(未定义)
```

> ​	对于尚未声明过的变量,只能执行一项操作,即使用 typeof 操作符检测其数据类型(对未经声明的变量调用 delete 不会导致错误,但这样做没什么实际意义,而且在严格模式下确实会导致错误)。 

```javascript
console.log(c);				//出现错误，因为没有定义变量c
console.log(typeof c); 		//undefined
```

#### Null类型

> ​	Null 类型是第二个只有一个值的数据类型,这个特殊的值是 null 。从逻辑角度来看, null 值表示一个空对象指针,而这也正是使用 typeof 操作符检测 null 值时会返回 “object” 的原因,　比如：

```javascript
var a = null;
console.log(typeof  a);		//object
```

> ​	如果定义的变量准备在将来用于保存对象,那么最好将该变量初始化为 null 而不是其它值,然后可以判断变量是否包含对象来做对应的操作，比如：　

```javascript
if (a != null) {
  ....
}
```

#### 字符串类型

> ​	String 类型用于表示由零或多个 16 位 Unicode 字符组成的字符序列,即字符串。字符串可以由双引号(")或单引号(’)表示,因此下面两种字符串的写法都是有效的:
>
> 注意： 不要混合使用单引号或者双引号，要同一，否则会报错。

```javascript
var a = "string1";
var b = 'string2';
```

> ECMAScript 中的**字符串**是不可变的,也就是说,字符串一旦创建,它们的值就不能改变。要改变某个变量保存的字符串,首先要销毁原来的字符串,然后再用另一个包含新值的字符串填充该变量, 比如：

```JavaScript
var lang ="java";				//lang是变量名，不是字符串，字符串"java"不可变
lang = "java" + "script";		//字符串拼接"+"
```

> 其他类型转换为字符串的方法**toString()**, 比如：

```javascript
var A = 10;
console.log(A.toString());
console.log(A.toString(2));		//转换为２进制，“1010”
console.log(Ａ.toString(8));		//转换为8进制　“12”
console.log(Ａ.toString(10));	//转换为10进制　“10”
console.log(A.toString(16));	//转换为16进制 “a”

var b = false;
console.log(b.toString());
```

> parseInt()方法:可解析一个字符串，并返回一个整数

```javascript
var a = '10abc';
//parseInt()
alert(parseInt(a));
//打印的结果是：10
```

> parseFloat()方法:可解析一个字符串，并返回一个浮点数

```javascript
var a = "10.23abc34";
//parseFloat()
alert(parseFloat(a));
//打印的结果是：10.23
```

> 在不知道要转换的值是不是 null 或 undefined 的情况下,还可以使用转型函数 String() ,这个函数能够将**任何类型**的值转换为字符串。 

```javascript
var a = null;
console.log(String(a));			//null
var b = undefined;
console.log(String(b));			//undefined
```

#### 布尔类型

> Boolean 类型是 ECMAScript 中使用得最多的一种类型,该类型只有两个字面值: true 和 false .

```javascript
var a = true;
var b = false;							
console.log(Boolean(a));				//true
console.log(Boolean(b));				//false
```

> 将一个值转换为其对应的 Boolean 值,可以调用转型函数 Boolean(). 

```javascript
var a = 10;
console.log(Boolean(a));				//true

var b = "hello";
console.log(Boolean(b));				//true

console.log(Boolean("helloworld"));		//true
console.log(Boolean(""));				//false
console.log(Boolean(10));				//true
console.log(Boolean(0));				//false
console.log(Boolean(undefined));		//false
```

![](https://nts.newbieol.com/static/k111/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/class-005/image/bool1.png)

![](https://nts.newbieol.com/static/k111/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/class-005/image/bool2.png)

```javascript
var a = 10;
if(a){
    alert("a is exist");
}
```

#### 数值类型

> 最基本的数值字面量格式是十进制整数,除了以十进制表示外,整数还可以通过八进制(以 8 为基数)或十六进制(以 16 为基数)的字面值来表示。比如：

```javascript
//javascript不支持直接写二进制
var a = 123;
var b = 0123;		//8进制使用'0'开头
var c = 0x123;		//16进制，使用'0x'开头

//科学计数法
var num1 =3.5e18;
console.log("num1 = ",num1);

//JavaScript保留17位有效数字
console.log(100000.123456789876543212);

console.log(0.1);
console.log(0.1 + 0.2);//不等于0.3!!!!!!
						//0.30000000000000004
```

##### 浮点型

```javascript
var a = 10.12;
var b = 0.12;
var c = .12;		//不推荐
```

> 对于那些极大或极小的数值,可以用 e 表示法(即科学计数法)表示的浮点数值表示, 比如：

```javascript
var a = 3.5e7;		//表示3.5 × 10^7;
var b = 3.5e-7;		//表示3.5 × 10^-7;
```

> ​	浮点数值的最高精度是 17 位小数,但在进行算术计算时其精确度远远不如整数。例如,0.1 加 0.2的结果不是 0.3,而是 0.30000000000000004。这个小小的舍入误差会导致无法测试特定的浮点数值。

```javascript
//if条件不成立
if ((a + b) == 0.3 ) {
  alert("a+b==0.3");
}
```

##### NaN(非零值)			?????

> ​	NaN ,即非数值(Not a Number)是一个特殊的数值,这个数值用于表示一个本来要返回数值的操作数未返回数值的情况(这样就不会抛出错误了)。
>
> ​	NaN是数值类型(NaN===>number)
>
> ​	ECMAScript 定义了isNaN() 函数。这个函数接受一个参数,该参数可以是任何类型,而函数会帮我们确定这个参数是否“**不是数值**”。 

```javascript
console.log(10 * "hello");

alert(isNaN(NaN));		//true

alert(isNaN(10));		//false

alert(isNaN(""));		//false		隐式转换,将字符串转换为0

alert(isNaN("blue"));	//true

alert(isNaN("10"));		//false		隐式转换10

alert(isNaN(true));		//false		隐式转换1

alert(Boolean(NaN));  	//false		0/NaN都是转成false
```

> - NaN自己不等于自己,NaN与任意的字符进行数学运算结果还是NaN
>
>   console.log(10  *  "10" );	//结果为NaN,而不是100.

### 10、JavaScript语句

> ECMAScript 中的语句以一个分号结尾;如果省略分号,则由解析器确定语句的结尾, 比如：

```javascript
var  value1 = a - b    //不推荐　     
var  value2 = a + b;　 //推荐  
```

> 使用代码块，让代码看起来更加清晰, 比如：

```javascript
//不推荐
if (value)
    alert("value is ...");

//推荐
if (value) {
   alert("value is ...");
}
```

### 11.关键字

![](https://nts.newbieol.com/static/k111/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86/class-005/image/keywords.png)

> **注意**：定义标识符时不要使用关键字和保留字。

### 12.字符串操作

```javascript
<script type="text/javascript">
// onload 页面加载完毕之后
onload = function(){

//HTML DOM document对象
//getElementById 返回对拥有指定 id 的第一个对象的引用。
document.getElementById("btn").onclick = function(){
//声明字符串并初始化
var sString = "hello world";

// length是输出字符串的长度
console.log("sString.length : " + sString.length);
  
// charAt(x)是输出 下标为x的字符
console.log("sString.charAt(2) : " + sString.charAt(2));
  
// substring(x,y) 是输出下标为 x~y的字符
console.log("sString.substring(1,8) : " + sString.substring(1,8));
  
// substr(x,y) 是输出下标从x开始的连续的y个字符
console.log("sString.substr(1,4) : " + sString.substr(1,4));
  
// indexof("x") 是输出字符串中从左到右第1个字符开始的x字符第一次出现的位置的数组下标
console.log("sString.indexOf('l'):" + sString.indexOf("l"));
  
// indexof("x",y)是输出字符串中从左到右第y个字符开始的x字符第一次出现的位置的数组下标
console.log("sString.indexOf('l',4) : " + sString.indexOf("l",4));
  
// indexof("x")是输出字符串中从右到左第 1个字符开始的x字符第一次出现的位置的数组下标
console.log("sString.lastIndexOf('l') : " + sString.lastIndexOf("l"));
  
// indexof("x",y)是输出字符串中从右到左第y个字符开始的x字符第一次出现的位置的数组下标
console.log("sString.lastIndexOf('l',4):" + sString.lastIndexOf("l",4));
      }
}
</script>
```







