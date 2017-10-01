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







## Browser对象