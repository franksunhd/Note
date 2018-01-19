## JavaScript 闭包、面向对象、继承、JSON

[TOC]

### 闭包

#### 1. 什么是闭包？

- 闭包是指是指有权访问另一函数作用域中变量的函数.子函数可以访问父函数中的变量.
- 返回值是一个函数.

#### 2. 闭包的优缺点

##### 优点

- 减少全局变量的定义,有利于变量的私有化.注意:JS 目前没有私有变量.

##### 缺点

- 运行环境 会一直存在,变量常驻内存,增加内存损耗,不容易被释放.

#### 3. 闭包

- 闭包就是函数内嵌套函数
- 闭包函数在外面被调用，访问
- 闭包可以访问函数外变量，函数外变量不可以访问闭包内部

#### 4. 如何创建闭包

- 在函数内部定义一个内部函数,内部函数引用了当前作用域的变量,并且将内部函数返回
- 内部函数就是闭包.

#### 5. this

- this 指向的 永远只可能是对象
- this 指向谁 永远不取决于this在哪,而是取决于函数在哪调用   
- this 指向的对象 我们称之为函数的**执行上下文** 也叫**函数的调用**

```javascript
// 创建闭包
<script type="text/javascript">
    function fun() {
      var a = 10;
      return function() {
        console.log("a = " + a);
      }
    }
    var ret = fun();
    ret();
</script>
```

```javascript
// 清除执行环境
<script type="text/javascript">
      function fun1(){
        var a = 10; // enclosing 作用域
        // fun2 就是闭包
        function fun2(){
          a++;
          alert(a);
        }
        return fun2;
      }

      var fun = fun1();
      fun(); //11
      // 执行环境保留
      fun(); //12
      // 清除执行环境
      fun = null;
      fun();
    </script>
```

```javascript
// 闭包的作用 保留执行环境
<script type="text/javascript">
      function fun1(){
        var a = 10;
        // fun2 是闭包
        function fun2(){
          for (var i = 0; i < 5; i++) {
            a++;
          }
          console.log(a);
        }
        return fun2;
      }

      var ret = fun1();
      ret();  //15
      // 执行环境保留
      ret();  //20
    </script>
```

```javascript
// 闭包优点
function fun() {
      //计数功能
      var count = 0;

      function addCount() {
        count++;
      }

      function minCount() {
        count--;
      }

      function getCount() {
        return count;
      }

      return [addCount, minCount, getCount];
    }

    var result = fun();
    // var add = result[0];
    // var min = result[1];
    // var get = result[2];
    //
    // add();
    // min();
    // console.log(get());

    // 等价于
    result[0]();    // add
    result[1]();    // min
    console.log(result[2]());
```

```javascript
// 闭包缺点 闭包变量常驻内存，增加内存消耗
<script type="text/javascript">
      function fun() {
      var a = [];

      for (var i = 0; i < 5; i++) {
          a[i] = function() {
            console.log("我是: ", i);
          };
      }

      return a;
    }

    var result = fun();
    result[0]();
    result[1]();
    result[2]();
    result[3]();
    result[4]();
</script>
```

#### 6. 经典闭包问题

```javascript
<script type="text/javascript">
    function fun(n,o) {
      console.log(o);
      return {
        fun:function(m){
          return fun(m,n);
        }
      };
    }
    var a = fun(0); // undefined
    a.fun(1);  // 0
    a.fun(2);  // 0
    a.fun(3);  // 0

    var b = fun(0).fun(1).fun(2).fun(3);
    //undefined,0,1,2

    var c = fun(0).fun(1); // undefined 0
    c.fun(2); // 1
    c.fun(3);//  1
    //问:三行a,b,c的输出分别是什么？
    </script>
```

#### 7. 作用域和作用域链

```javascript
<script type="text/javascript">
      var name = "The Window";
      var object = {
        name : "My object",
        getNameFunc : function(){
          // 下面这个匿名函数是 闭包
          return function(){
            var name = "ssy";
            console.log(this);
            return this.name;
          }
        }
      }

      var first = object.getNameFunc();
      var s = first();
      alert(s);

      // 等价于
      // alert(object.getNameFunc()());

      /*
        this 指向的 永远只可能是对象
        this 指向谁 永远不取决于this写在哪!,而是取决于函数在哪调用
        this 指向的对象,我们称之为函数的上下文context,也叫函数的调用者.
      */
    </script>
```

```javascript
<script type="text/javascript">
      var name = "The Window";
      var object = {
        name : "My object",
        getNameFunc : function(){
          var that = this;
          console.log(this);
          // 下面这个匿名函数是 闭包
          return function(){
            var name = "ssy";
            return that.name;
          }
        }
      }
  alert(object.getNameFunc()());
</script>
```

### 面向对象

#### 1. 对象:属性和方法的集合

#### 2. 类:变量和方法的集合

#### 3. 封装:隐藏实现细节,只提供对外接口

- 封装，为程序员提供了在这门语言中构建对象的能力，对象是属性和方法的集合，调用对象时是通过对象调用方法，对象不同，调用的方法会有所不同。

#### 4. 继承:子类 继承 父类 的属性和方法

#### 5. 多态:对两个或多个属于不同类的对象,对同一方法的调用作出不同响应的方式.

#### 6. JS没有函数重载,C没有继承和多态

#### 7. 创建对象的常见方式

##### 1) 使用已有类型创建

```javascript
var obj = new Object();
var date = new Date();
```

##### 2) 直接使用字面量的方法创建

```javascript
var obj = {
  name:'ssy',
  age:23,
  sayName:function(){
    console.log('this.name');
  }
}
```

##### 3) 工厂模式

```javascript
function CreatePerson(name,age){
  var x = new Object();
  x.name = name;
  x.age = age;
  x.sayName = function(){
    console.log('this.name');
  }
  return x;
}

var str = CreatePerson('ssy',12);
str.sayName();
```

##### 4) 构造函数

```javascript
function Person(name,age){
    this.name=name;
    this.age=age;
    this.sayName=function(){
        console.log(this.name);
    }
}
var person1=new Person('amy',23);
var person2=new Person('amy',24);
```

##### 5) 原型模式

```javascript
function Person(){
}
Person.prototype.name = "lisi";
Person.prototype.age = 12;

var one = new Person();
```

##### 6) 原型模式和构造函数结合

```javascript
function Person(name,age){
    this.name=name;
    this.age=age;
}

Person.prototype={
  <!-- costructor 构造函数 -->
    costructor:Person,
    sayName:function(){
        console.log(this.name);
    }
}
```

#### 8. 查找顺序

```javascript
<script type="text/javascript">
    var name = 'html name';
    function Person(){
      this.name = 'this.name'
    }

    Person.prototype.name = 'ssy';
    Person.prototype.age = 12;

    var one = new Person();
    var two = new Person();
    two.name = 'hello';

    console.log(one.name); // this.name
    /*
      查找顺序: 全局作用域  函数作用域  原型
    */
    console.log(two.name);  // hello
</script>
```

### 函数和方法的区别

- 函数 ： 它是独立运行的功能模块
- 方法 ： 是绑定在对象上的

### 四种作用域

```
   L       >     E       >       G       >       B
(local)     (enclosing)       (global)       (build in)
 局部           闭包              全局            内置
```



### 继承

- 继承方式总共有6种，比较常用的有3种
- 原型链继承 / 借助构造函数继承  /  组合继承

构造函数，构造函数原型，实例 这这三者之间的关系

```javascript
// 构造函数
      function Person(name) {
        this.name = name;
      }

      // 构造函数原型
      Person.prototype.getName = function() {
        console.log(this.name);
      };

      // person 是实例
      var person = new Person("ssy");

      // 构造函数的 prototype属性 指向构造函数原型
      console.log(Person.prototype);

      // 构造函数原型的 constructor属性 指向构造函数
      console.log(Person.prototype.constructor);  // 指向构造函数

      // 构造函数生成的实例 通过_proto_属性指向 构造函数原型
      console.log(person.__proto__); // 指向 构造函数原型

   // 判断构造函数原型的prototype属性 和 实例的 __proto__ 属性 指向是否相同
      console.log(Person.prototype == person.__proto__);  //true
```

#### 原型链继承

![](./images/Prototype.png)

```javascript
<script type="text/javascript">
      // 构造函数 Animal
      function Animal(name){
        this.name = name;
      }

      // 构造函数Animal原型上定义了一个方法,并且Animal的实例会继承该方法
      Animal.prototype.getPlanet = function() {
        return this.planet;
      }

      // 构造函数Person

      function Person(name){
        this.name = name;
      }

      /*
        Person的原型用Animal的实例进行赋值,(实例A)
        Person的原型 (构造函数原型B)就有了Animal(实例A)的一切属性和方法
        Animal实例(实例A)的属性和方法都是继承自Animal构造函数和原型的属性和方法
      */
      Person.prototype = new Animal("earth");

      // Person的原型添加自己的一个新方法 getName
      Person.prototype.getName = function() {
        return this.name;
      }

      /*
      person 是Person构造函数的实例,继承了Person原型上的新增方法
      又有Animal实例继承自Animal原型上的属性和方法
      person 实例也可以作为值, 赋给别的构造函数的原型,供其实例进行继承,这样做就会变成了一个链式继承,这就是原型链继承
      */

      var person = new Person('ssy');
      // 判断 person 是否是 Person构造函数的原型
      console.log(person instanceof Person);   // true

      // console.log(Animal.isPrototypeof(Person.prototype));

      console.log(person);   // Person{}

      var p = person.getPlanet();
      console.log(p);  // undefined

    </script>
```

```javascript
<script type="text/javascript">
      function SuperType(){
        this.property = true;
      }

      SuperType.prototype.getSuperValue = function(){
        return this.property;
      }

      function SubType() {
        this.subproperty = false;
      }

      // SubType的原型 继承了SuperType 的属性和方法
      SubType.prototype = new SuperType();

      SubType.prototype.getSubValue = function () {
        return this.subproperty;
      }

      var instance = new SubType();
      console.log(instance.getSuperValue()); //true
      console.log(instance.getSubValue());  //false

      // 判断instance 是否是 xxxx 的一个实例对象
      console.log(instance instanceof Object);  //true
      console.log(instance instanceof SuperType);  // true
      console.log(instance instanceof SubType);    // true

      // 判断 instance 是否在 xxx 原型链上
      console.log(Object.prototype.isPrototypeOf(instance));  //true
      console.log(SuperType.prototype.isPrototypeOf(instance));  //true
      console.log(SubType.prototype.isPrototypeOf(instance));  // true
    </script>
```

##### 原型链继承的缺点

```javascript
<script type="text/javascript">
      function Super(){
        this.colors = ['red','green','blue'];
      }

      function Sub() {
      }

      Sub.prototype = new Super();

      /*
        所有实例共享属性,修改任意一个都会影响所有实例
        在创建实例时无法传递参数
      */

      var one = new Sub();
      console.log(one.colors);

      one.colors.push("pink");

      var two = new Sub();
      console.log(two.colors);
    </script>
```

##### call 和 apply

```javascript
<script type="text/javascript">
      var name = 'global';  // window.name
      function fun(arg1,arg2) {
        console.log("this = " , this);
        console.log("this.name = ",this.name);
        console.log("arg1 = ", arg1);
        console.log("arg2 = ", arg2);
      }

      fun();
      //  window  global undefined undefined
      console.log('-----------间接调用-----------');

      var obj1 = {
        name:'ssy',
        age : 12
      }

      var obj2 = {
        name : "lisi",
        age : 23
      }

      /*
        call 方法的功能:在一个指定的this上调用函数,其实就是将函数内部的this指向搞清楚
        call 方法从第二个参数开始的参数,都是传递给函数的参数!!!
      */

      fun.call(obj1,10,20);
      fun.call(obj2,30,23);
      fun.call(null,10,20);


      console.log('-----------apply-----------');

      /*
        apply:功能和call一模一样
        区别:最多接受两个参数,给函数传参使用的是数组,
      */
      fun.apply(obj, [10,20]);
    </script>
```

#### 借助构造函数继承

```javascript
<script type="text/javascript">
      function Super(name) {
        this.name = name;
        // this 指定的执行环境为 Sub
        console.log(this);   // Sub{}
        console.log(this.name);  // lisi
      }

      function Sub(name,age) {
        Super.call(this,name);  //调用父类构造函数
        this.age = age;
      }

      var one = new Sub('lisi',10);
      console.log(one.name);  // lisi
      console.log(one.age);   // 10
    </script>
```

```javascript
<script type="text/javascript">
      function Person(name,age) {
        this.name = name;
        this.age = age;
      }

      Person.prototype.sayHello = function() {
        console.log('say Hello!');
      }

      function Student(name,age,score) {
        // 借用构造函数
        Person.call(this, name,age);
        this.score = score;
      }

      var one = new Student('lisi',20,88);
      // 借用构造函数的缺点就是 只能继承构造函数的属性和方法
      // 无法继承构造函数原型上的属性和方法
      // 也就是 sayHello 没有被调用
      console.log(one);  // Student{}
      one.sayHello(); // one.sayHello is not a function
    </script>
```

#### 组合继承

```javascript
<script type="text/javascript">
    function Super(name){
      this.name = name;
      this.colors = ["red", "blue"];
    }
    Super.prototype.getName = function(){
      return this.name;
    };

    function Sub(name,age){
      Super.call(this,name);
      this.age = age;
    }

    Sub.prototype = new Super();
    Sub.prototype.constructor = Sub;
    Sub.prototype.getAge = function(){
      return this.age;
    };

    var one = new Sub('lisi', 10);
    console.log(one.getName());// lisi
    console.log(one.getAge()); //10
    one.colors.push("black");

    var two = new Sub('wangwu', 12);
    console.log(two.getName());// wangwu
    console.log(two.getAge()); //12
    console.log(two.colors); //["red", "blue"];
    </script>
```

```javascript
<script type="text/javascript">
      function Person(name,age) {
        this.name = name;
        this.age = age;
      }

      Person.prototype.sayHello = function() {
        console.log('say Hello!');
      }

      function Student(name,age,score) {
        // 借用构造函数,继承构造函数内部的属性
        Person.call(this, name,age);
        this.score = score;
      }


      // 使用原型链继承原型的方法和属性
      Student.prototype = new Person();
      Student.prototype.constructor = Student;


      var stu1 = new Student('lisi',12,56);
      console.log(stu1);
      stu1.sayHello();
    </script>
```

```javascript
<script type="text/javascript">
      function Super(name) {
        this.name = name;
        this.colors = ['red','green'];
      }

      Super.prototype.getName = function() {
        return this.name;
      }

      function Sub(name,age) {
        Super.call(this,name);
        this.age = age;
      }

      Sub.prototype = new Super();
      Sub.prototype.constructor = Sub;

      Sub.prototype.getAge = function(){
        return this.age;
      }

      var one = new Sub('lisi',10);
      console.log(one.getName());  // lisi
      console.log(one.getAge());   // 10

      one.colors.push('blue');

      var two = new Sub('ssy',32);
      console.log(two.getName());  // ssy
      console.log(two.getAge());   // 32
      console.log(two.colors);   // ['red','green']
    </script>
```

###  JSON

#### JSON序列化

- JSON序列化就是将JSON对象转换为字符串类型
- JSON.stringify()

```json
<script type="text/javascript">
      var stu = {
        "name" : "lisi",
        "age" : 23,
        "hobby" : ['read','write','drink'],
        "score" : 88
      }

      var str = JSON.stringify(stu,function(key,value){
        if (key === "age") {
          return value + 100;
        }

        if (key === "score") {
          return value - 10;
        }

        return value;
      });

      console.log(str);
	  // {"name":"lisi","age":123,"hobby":["read","write","drink"],"score":78}

      str = JSON.stringify(stu,['name','age','score']);
      console.log(str);
	// {"name":"lisi","age":23,"score":88}

      str = JSON.stringify(stu,null,'\t');
      console.log(str);
/*
	{
      "name": "lisi",
      "age": 23,
      "hobby": [
          "read",
          "write",
          "drink"
      ],
      "score": 88
	}
*/
    </script>
```

#### JSON解析

- 将一个JSON字符串解析为一个JavaScript值，在解析的过程中可以选择性修改一些属性值
- JSON.parse()

```json
<script type="text/javascript">
      var str = '{"name":"lisi","age":10,"score":90}';
      var json = JSON.parse(str);

      console.log(json);

      var obj = JSON.parse(str,function(key,value){
        if (key === 'name') {
          return "我是" + value;
        }

        if (key === 'score') {
          return "实际成绩为:" + (value - 10);
        }

        return value;
      });

      console.log(obj);
    </script>
```

