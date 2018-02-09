## JavaScript 高级应用/函数绑定/柯里化/函数记忆/高阶函数/定时器节流/设计模式

[TOC]

### 1.函数绑定

1. 函数绑定就是创建一个函数，可以在特定的this环境中指定参数调用另一个参数.

2. 函数一旦bind成功，那么从此以后返回的新函数的this就已经固定了
  在任何位置调用该函数，this都不会变

3. 其中的参数, arg1 和 arg2 相当于提前给fun1传递了参数
  在调用fun1时传入的参数会紧跟其后，作为额外的参数.

4. bind功能: 一个函数可以bind任意次数，想bind到哪个this都行
    1). 绑定this
    2). 提前传入参数

```javascript
<script type="text/javascript">
      var btn1 = document.getElementById('btn1');
      var btn2 = document.getElementById('btn2');
      btn1.value = 1000;
      btn2.value = 10000;
      var value = 10;
      var obj = {
        value : 100
      }
      function handler(arg1,arg2) {
        console.log("this.value = ",this.value);
        console.log("arg1 = ",arg1);
        console.log("arg2 = ",arg2);
      }
      // fun1 是bind返回的新函数
      var fun1 = handler.bind(obj,10,20);
      fun1(); // 100 10 20
      handler(20,30);  // 10 20 30
      /*
        函数一旦bind成功，那么从此以后返回的新函数的this就已经固定了
        在任何位置调用该函数，this都不会变
      */
      btn1.addEventListener('click',fun1,false); // 100 10 20
      btn2.addEventListener('click',fun1,false); // 100 10 20
</script>
```

```javascript
<script type="text/javascript">
      function handler(arg1,arg2) {
        console.log(arg1,arg2);
        console.log(arguments);
      }
      /*
        其中的参数, 100 和 1000 相当于提前给fun1传递了参数
        在调用fun1时传入的参数会紧跟其后，作为额外的参数.
      */
      var fun1 = handler.bind(null,100,1000);
      fun1(); // 100 1000 arguments[2] ==> 100 1000
      fun1(20,30); // 100 1000 arguments[4] ==> 100 1000 20 30
      /*
        bind功能: 一个函数可以bind任意次数，想bind到哪个this都行
        1. 绑定this
        2. 提前传入参数
      */
      var fun2 = handler.bind(null,195,200);
      fun2();  // 195 200 arguments[2] ==> 195 200
      fun2(222,333);  // 195 200 arguments[4] ==> 195 200 222 333
    </script>
```

### 2.函数柯里化

- 提前给该函数传入固定的参数

```javascript
<script type="text/javascript">
      function count(rate,price) {
        return console.log(price + " * " + rate + " = " + price*rate);
      }
      var newCount = count.bind(null,0.95);
      newCount(1000); // 950
      newCount(100);  // 95
      newCount(20); // 19
    </script>
```

### 3.函数记忆/函数缓存

```javascript
<script type="text/javascript">
      /*
        函数缓存:
      */

      // 判断是否是偶数
      // 充分利用了 函数可自定义属性的特点！！！
      function isEven(num) {

        // 第一次调用该函数 没有result属性，所以添加一个result属性
        if (!isEven.result) {
          // result非空执行
          isEven.result = {}
        }

        // 每次都试图从已有结果中查找
        if (isEven.result[num] != undefined) {
          // 如果找到 则返回
          return isEven.result[num];
        }

        // 如果没有结果，则需要重新计算
        console.log("-----重新计算------");

        var temp = (num % 2 === 0 );  // 返回的是true or false

        // 计算之后 保存计算结果
        return isEven.result[num] = temp;
      }

      console.log(isEven(2));  //重新计算 true
      console.log(isEven(3));  // 重新计算 false
      console.log(isEven(2));  // true
      console.log(isEven(3));  // false
    </script>
```

### 4.高阶函数

- 高阶函数其实就是传入一个或者多个参数，返回一个函数。

```javascript
<script type="text/javascript">
  	// 子函数 sum
      function sum(a,b) {
        return a + b;
      }
	// 子函数 pow
      function pow2(num) {
        return num * num;
      }
	// 函数工厂
      function createFun(fun1,fun2) {
        return function(arg1,arg2) {
          return fun2(fun1(arg1,arg2));
        }
      }
	// 函数调用
      var str = createFun(sum,pow2);
      console.log(str(10,20));  // 900
    </script>
```

### 5.定时器节流

- 基本思想是指，某些代码不可以在没有间断的情况连续重复执行。第一次调用函数，创建一个定时器，在指定的时间间隔之后运行代码。当第二次调用该函数时，它会清除前一次的定时器并设置另一个。

```javascript
<script type="text/javascript">
      var btn = document.getElementById('btn1');
      var tb = document.getElementById('item');
      var str = document.getElementById('str');

      var count = 0,timer;
      function createTable() {
        count++;
        if (count > 1000) {
          clearTimeout();
          return;
        }

        for (var i = 0; i < 5; i++) {
          // var content = "<tr><td>lisi</td><td>22</td><td>男</td></tr>";
          var content = "<li>aaaaa</li>";
          // tb.innerHTML += content;
          str.innerHTML += content;
        }
        timer = setTimeout(createTable,0);
        console.log(count);
      }
      document.onclick = function() {
        alert("点击了document");
      }
      btn.onclick = function(event) {
        event.stopPropagation(); // 阻止事件传递 DOM0级
        createTable();
        /*
        for (var i = 0; i < 5000; i++) {
          var content = "<tr><td>lisi</td><td>22</td><td>男</td></tr>";
          tb.innerHTML += content;
        }
        */
      }
    </script>
```

### 6.设计模式

#### 1).单例模式

- 用来划分命名空间,以减少网页中的全局变量的数目，还可以在一种名为分支的技术中用来封装浏览器之间的差异。
- 闭包的本质不是函数嵌套函数,而是作用域链的延伸
- 惰性创建单例对象

##### 字面量创建

```javascript
// 方法一 使用字面量创建一个简单的单例对象
var obj = {
        name : "lisi",
        age : 23,
        score : 89,
        eat : function() {
          console.log("-----eat-----");
        },
        drink :function() {
          console.log("----drink----");
        }
      }
```

##### 使用闭包封装私有成员和方法

```javascript
// 方法二 使用闭包在其内部封装私有成员和方法
var mySingleton = function() {
        // 这里声明私有变量和私有方法
        var privateA = "hello world";
        function showHello() {
          console.log(privateA);
        }
        // 返回公有变量和方法
        return {
          publicMethod:function() {
            showHello();
          },
          publicVar : "ssy"
        };
      };

      var single = mySingleton();
      single.publicMethod();  // hello world
      console.log(single.publicVar); // ssy
```

##### 使用惰性创建单例对象

```javascript
// 方法三 : 惰性创建单例对象
      var mySingletons = (function() {
        var instantiated;
        function init() {
          // 这里定义单例代码
          return {
            publicMethod:function() {
              console.log("hello world!");
            },
            publicProperty:"test"
          };
        }
        return {
          // 静态方法
          getInstance: function() {
            if (!instantiated) {
              instantiated = init();
            }
            return instantiated;
          }
        };
      })();

      mySingletons.getInstance().publicMethod(); // hello world!
      var property = mySingletons.getInstance().publicProperty;
      console.log(property); // test
```

```javascript
<script type="text/javascript">
      var MyNameSpace = {};
      MyNameSpace.singleton = (function(){
        var exist = null;
        function Singleton() {
          var privateA = 10;
          var privateB = 20;
          // 私有方法和变量
          function privateFn1(value) {
            privateA = value;
          }
          function privateFn2() {
            return privateA;
          }

          return {
            publicA:30,
            publicB:40,
            setPrivateA:function(value) {
              privateFn1(value);
            },
            getPrivateA:function() {
              return privateFn2();
            }
          };
        }

        return {
          // 该方法就是惰性创建单例对象的特点
          getInstrance:function() {
            if (!exist) {
              exist = Singleton();
            }
            return exist;
          }
        }
      })();

      MyNameSpace.singleton.getInstrance().setPrivateA(15);  
      var single = MyNameSpace.singleton.getInstrance().getPrivateA();
      console.log(single);  // 15
    </script>
```

##### 单例对象的应用

```javascript
<script type="text/javascript">
    // 单例模式主要用于在系统间各种模式的通信协调上
    var SingletonTester = (function() {
      // 参数:传递给单例的一个参数集合
      function Singleton(args) {
        // 设置args变量为接收的参数或者为空(对应没有提供的情况)
        var args = args || {};
        // 设置name 参数
        this.name = "SingletonTester";
        // 设置pointX的值
        this.pointX = args.pointX || 6;
        // 设置pointY的值
        this.pointY = args.pointY || 10;
      }

      // 实例容器
      var instance;
      var _static = {
        name:"Ssy",

        // 获得实例的方法
        // 返回SingletonTester
        getInstance:function(args) {
          if (instance === undefined) {
            instance = new Singleton(args);
          }
          return instance;
        }
      }

      return _static;
    })();

    var singletonTester = SingletonTester.getInstance();
    console.log(singletonTester.name);  // SingletonTester
    console.log(singletonTester.pointX);  // 6
    console.log(singletonTester.pointY);  // 10
    </script>
```

#### 2).工厂模式

- 工厂模式就是将成员对象的实例化推迟到子类中进行的类.

```javascript
<script type="text/javascript">
      var Car = (function() {
        // 这里上下的 Car 完全不是一回事
        var Car = function(model,year,miles) {
          this.model = model;
          this.year = year;
          this.miles = miles;
        };

        // 返回一个匿名函数
        return function(model,year,miles) {
          // 实例化 内部的Car
          return new Car(model,year,miles);
        };
      })();

      // 这里的 Car 指的是 外层函数的 Car
      var tom = new Car("Tom",2017,2000);
      var dudu = new Car("dudu",2018,5000);
      console.log(tom.year);  // 2017
      console.log(dudu.year);  // 2018
    </script>
```

```javascript
<script type="text/javascript">
  	  // 创建对象
      var productManager = {};
      // 子函数 1
      productManager.createProductA = function() {
        console.log("ProductA");
      }
	  // 子函数 2
      productManager.createProductB = function() {
        console.log("ProductB");
      }
      // 工厂函数
      productManager.factory = function(type) {
        return new productManager[type];
      }
	  // 函数调用
      productManager.factory("createProductA");  // ProductA
      productManager.factory("createProductB");  // ProductB
    </script>
```

##### 工厂函数的应用

```javascript
<script type="text/javascript">
      var page = page || {};
      page.dom = page.dom || {};

      // 子函数1: 处理文本
      page.dom.Text = function() {
        this.insert = function(where) {
          var txt = document.createTextNode(this.text);
          where.appendChild(txt);
        };
      };
      // 子函数2: 处理link
      page.dom.Link = function() {
        this.insert = function(where,value) {
          var link = document.createElement('a');
          link.href = this.url;
          link.appendChild(document.createTextNode(this.value));
          where.appendChild(link);
        };
      };
      // 子函数3: 处理img
      page.dom.Img = function() {
        this.insert = function(where) {
          var image = document.createElement('img');
          image.src = this.url;
          where.appendChild(image);
        };
      };

      // 工厂函数
      page.dom.factory = function(type) {
        return new page.dom[type];
      };

      var x = page.dom.factory('Link');
      x.url = "http://www.baidu.com";
      x.value = "百度一下";
      x.insert(document.body);

      x = page.dom.factory('Text');
      x.text = "天下第一";
      x.insert(document.body);

      x = page.dom.factory('Img');
      x.url = "./1.jpg" ;
      x.insert(document.body);
    </script>
```
