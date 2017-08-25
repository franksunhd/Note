## JavaScript的函数重载

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

