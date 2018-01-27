## JavaScript的函数重载/事件机制/定时器

[TOC]

### 1.函数的重载

- 实现函数的重载:参数的类型,参数的数量
- 从语言角度来说，javascript不支持函数重载，不能够定义同样的函数然后通过编译器去根据不同的参数执行不同的函数。但是javascript却可以通过自身属性去模拟函数重载。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函数的重载</title>
    <script type="text/javascript">
      
      function test() {
        alert("我没有任何参数!");
      }
      function test(a,b) {
        alert("我有两个参数!");
      }
      function test(a,b,c) {
        alert("我有三个参数!");
      }
      function test(a,b,c){
        alert("我形参的个数为:["+ test.length + "]" + "实际传入的参数为:["+ arguments.length +"]");
      }
      //在JS中,形参的数目和实参的数目可以不同
	  //函数名相同的执行最近的一个
    </script>
  </head>
  <body>
    <h1>函数的重载</h1>
    <!-- 测试函数的重载 -->
  </body>
</html>
```

#### 实现函数的重载

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函数的重载</title>
    <script type="text/javascript">
      //在JS中,形参的数目和实参的数目可以不同
      //实现函数的重载:参数的类型,参数的数量
      function sayHello(a,b,c){
        //获取参数
        var args = arguments;
        //判断参数的数目
        alert("我形参的个数为:["+ test.length + "]" + "实际传入的参数为:["+ arguments.length +"]");
        if(args.length == 1 && typeof args[0] == "string")
        {
          alert("执行一个参数的方法===字符串");
        } else if(args.length == 1 && typeof args[0] == "number") {
          alert("执行一个参数的方法===数字");
        } else if(args.length == 2){
          alert("执行两个参数的方法");
        } else if(args.length == 3){
          alert("执行三个参数的方法");
        } else {
          alert("暂无处理参数的方法");
        }
      };

    </script>
  </head>
  <body>
    <h1>函数的重载</h1>
    <!-- 测试函数的重载 -->
    <input type="button" name="" value="测试函数重载" onclick="test(1,2);" />
    <input type="button" name="" value="测试重载" onclick="sayHello(1);" />
  </body>
</html>
```

### 2.事件机制

#### 事件的引入方式

##### 第一种:直接给标签加事件

```html
<input type="button" value="测试第一个按钮" onclick="test();">
  
<script type="text/javascript">
function test() {
  alert("我是一个按钮");
};
</script>
```

##### 第二种:标签设置Id,在js代码中找到id加载事件

```html
<input type="button" value="测试外部事件" id="btn">
<script type="text/javascript">

onload = function() {
  document.getElementById('btn').onclick = function() {
    alert('我是外部按钮');
  }
}
</script>
```

#### javaScript的事件驱动

- 在浏览器中，事件作为一个极为重要的机制，给予JavaScript响应用户的操作和DOM变化的能力。

#### 事件的触发

- 用户的互动操作(单击,双击,拖动)
- 业务逻辑触发(Ajax的 readyState 的值从0~4的改变)

#### 常见的事件操作

- 单击　双击
- 鼠标移动
- 键盘按下
- 表单
- 页面事件

### 3.定时器

- 页面中有很多效果是动态的发生变化，比如轮播图，每隔一定的时间都换一张图片显示，这些效果都可以用javascript的定时器实现。 

#### 间隔定时器 setInterval()

- setInterval(callback, delay);//每隔delay毫秒的时间就执行一次fun函数 

```javascript
var si = setInterval("alert('helloworld')", 1000);//每隔1s输出helloworld
function fun(){
    console.log("helloworld");
}

si = setInterval(fun, 1000); //传入函数也可以，比较常用
```

- 注意：setInterval如果调用的程序在间隔的时间内没有完成，那么仍然会再次执行该函数 

#### 取消间隔定时器clearInterval()

```javascript
var si = setInterval(fun, 1000);
clearInterval(si);//需要用到setInterval返回的id
```

#### 超时定时器 setTimeout(callback,delay);

- 间隔delay毫秒之后执行函数callback,并且只执行一次。 

```javascript
// 延时调用
		setTimeout(run,2000);

		function run() {
			console.log("run执行...");
		}

// 1.超时定时器只调用一次,如何实现无限调用
setTimeout(function() {
			pn++;
			console.log(pn);
            // callee 被调用的函数 在这里指代这个匿名函数
			// console.log(arguments.callee);
			setTimeout(arguments.callee,1000);
		},1000);

// 2.
		var pn = 0;
		var timedId;
        function loop() {
			pn++;
			console.log(pn);
            // 递归循环
			// loop();

            //  函数里面代码量很大,同步的请求可能等上1s或以上,
            //  导致一次函数还没执行结束就开始执行下一次
			timedId = setTimeout(loop,1000);
        }

		loop();	
```

#### 取消超时定时器clearTimeout()

- setTimeout函数会在指定的时间过后运行函数，并且只运行一次，所以可以每次重新调用。而setInterval却没有被自己所调用的函数所束缚，它只是简单地每隔一定时间就重复执行一次那个函数,如果在间隔时间内函数没有执行完，也会继续执行.使用arguments.callee
   可以返回调用函数本身, 使用setTimeout可以更好取代setInterval。使用clearTimeout()可以取消超时。