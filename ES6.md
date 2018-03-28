## ES6新语法

[TOC]

### 1. 变量的声明

#### var 

```javascript
for(var i = 0; i < 8; i++) {}
console.log(i);  // 8
```

#### let 声明变量 

- ES6 新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。

```javascript
for(let j = 0;j < 8; j++) {}
console.log(j);  // 报错, j未定义
```

- 注意: let不存在变量声明

#### const 声明常量

```javascript
// const 声明常量,常量名用大写字母,常量一旦声明,不允许修改
const PI = 3.14;

// 声明的常量具有块级作用域
if(true){
    const HEIGHT = 100;
}
console.log(HEIGHT);  // HEIGHT 未定义
```

### 2. 块级作用域

```javascript
// 为了避免出现变量的污染,使用立即执行函数,即匿名函数
var aa = 100;
// 块级作用域
(function () {
    var aa = 200;
})();

console.log(aa);  // 100

{
    let aa = 300;
}
console.log(aa);  // 100

// let 声明的变量不能重名
let str = "春江水暖鸭先知";
// let str = "儿童散学归来早";
console.log(str);  // 重名报错
```

### 3.模式匹配 (解构赋值)

```javascript
var a = 1;
var b = 2;
var c = 3;

console.log(a,b,c);  // 1 2 3
a = b = c = 10;
console.log(a,b,c);  // 10 10 10

// 模式匹配: 等号左边的模式相同,左侧的变量就会附上右侧对应的值
var [a ,b, c] = ['曹操','刘备','关羽'];
console.log(a,b,c);  // 曹操 刘备 关羽

var [a1,,c1] = ['曹操','刘备','关羽'];
console.log(a1,c1);  // 曹操 关羽

// ...e1 获取剩余的内容,吧内容全部赋值给 '...' 修饰的变量
var [d1,...e1] = ['曹操','刘备','关羽'];
console.log(d1,e1); // 曹操 (2)["刘备", "关羽"]

// 传入默认值
var [f1,f2 = '窦娥'] = ['小包菜','司马毛'];
console.log(f1,f2);  // 小包菜 司马毛
```

#### 对象解构

```javascript
// 对象进行解构,只与对象的属性名有关,与次序无关
var {name,job,age} = {age:'56',job:'开封府府尹',name:'包文正'};
console.log(name,job,age);  // 包文正 开封府府尹 56
```

#### 模式匹配的用途

```javascript
var num1 = 100;
var num2 = 200;
var temp = 0;

// 用途1:交换变量
temp = num1;
num1 = num2;
num2 = temp;
console.log(num1,num2);  // 200 100

var num1 = 100;
var num2 = 200;
[num1,num2] = [num2,num1];
console.log(num1,num2);  // 200 100


// 用途2:函数返回多个值:
function afun () {
    return ['悟空','八戒','沙僧'];
}

var [w1,w2,w3] = afun();
console.log(w1,w2,w3);  // 悟空 八戒 沙僧

// 用途3:解析后台传过来的数据
var json = {
    name:'孙传挺',
    age:34,
    job:'武将'
};

var {name,job,age} = json;
console.log(name,age,job);  // 孙传挺 34 武将
```

### 4.字符串扩展

#### startsWith/ endsWith 判断字符串开头和结尾的字符

```javascript
var str = "老当益壮,宁移白首之心";
// 判断字符串开头和结尾的字符
console.log(str.startsWith('老当'));  // true 表示以什么开头
console.log(str.endsWith('老当'));  // fasle
console.log(str.endsWith('心'));  // true
```

#### includes 判断是否有给出的参数字符串

```javascript
var str = "老当益壮,宁移白首之心";
// includes 判断是否有给出的参数字符串
console.log(str.includes('白首'));  // true
console.log(str.includes('哈哈'));  // fasle
```

#### 模板字符串

```javascript
// 模板字符串
let name = '伏羲';
let age = 20000;
let job = '人皇始祖';

var str1 = "你好:" + name + ",你今年" + age + "岁了,你是" + job + "!";
console.log(str1);  // 你好:伏羲,你今年20000岁了,你是人皇始祖!

// 模板字符串,可以直接插入变量
var str2 = `你好:${name},你今年${age}岁了,你是${job}!`;
console.log(str2); // 你好:伏羲,你今年20000岁了,你是人皇始祖!

// 模板字符串可以支持多行书写
var str3 = "你好:" + name + ",你今年"
    + age + "岁了,你是" + job + "!";
console.log(str3);

var str4 = `你好:${name},
你今年${age}岁了,
你是${job}!`;
console.log(str4);

// 模板字符串可以写表达式,也可以写函数
var x = 1;
var y = 3;
var str5 = `${x} + ${y} = ${x+y}`;
console.log(str5);  // 1 + 3 = 4

function add(x,y) {
    return x + y;
}
var str6= `${x} + ${y} = ${add(1,3)}`;
console.log(str6); // 1 + 3 = 4
```

### 5.数组扩展

```javascript
var arr1 = new Array();  // 创建一个空数组
var arr2 = new Array(2);  // 创建一个长度为2的空数组
var arr3 = new Array(2,3);  // 创建一个数组,并给数组添加2和3两个元素

// Array.of() 参数为数组的元素,把参数集体转换为数组,不管是几个数
var arr4 = Array.of();
console.log(arr4);  // 空数组

var arr5 = Array.of(3);
console.log(arr5); // [3]
```

### 6.Class 类 和 extends  继承

```javascript
// es6 具有类的概念
class Animal {
    // es6 里面的函数的定义可以不写 function
    // 构造函数,在类里面声明,作用是接收或者设置基本的属性
    constructor(){
        this.type = '动物';
    }

    // 设置方法
    say(str) {
        console.log(this.type + "说:" + str);
    }
}

let cat = new Animal();
cat.say('喵喵喵');

// 继承 extends
class animal extends Animal{
    constructor() {
        // 子类的构造方法里面必须执行一个 super 方法
        super();
        this.type = '猫';
    }
}
// 实例化
let c = new animal();
c.say('喵喵');

// es6里面函数可以给参数设置默认值
function test(a,b){
    console.log(a+b);
}

test(1,2);

// 设置默认
function test1(a,b = 20){
    console.log(a+b);
}
test1(1);
```

### 7. 箭头函数

```javascript
// 箭头函数
var test = function (i) {
    return i + 1;
}

console.log(test(3));  // 4

var test1 = (i) => i + 1;
console.log(test1(4));  // 5

var test2 = (i,j) => {
    console.log(i+j);
}
test2(1,2);  // 3

// 获取函数的参数集合
function sum1() {
    var sum = 0;
    for(var i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}
console.log(sum1(1,2,3,4,5));  // 15

// es6 中获取参数集合的方法
function sum2(...value) {
    console.log("----------");
    console.log(value);
    console.log("----------");
    var sum = 0;
    for(let i of value) {
        sum += i;
    }
    return sum;
}
console.log(sum2(1,2,3,4,5));
```





