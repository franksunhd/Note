## Path 模块 / jsonp跨域 /express(nodeJs的框架)

[TOC]

### 1.Path 模块 对文件路径进行操作

#### normalize 格式化路径

```js
var path = require('path');
// 1. normalize 格式化路径
var str1 = './a/ss/../../ad/ss/d/..a/aa';
var str2 = path.normalize(str1);
console.log(str2);  // ad/ss/d/..a/aa
```

#### join 拼接路径 规范化输出路径

```javascript
var path = require('path');
// 2.拼接路径,规范化输出路径
var str3 = '../a/a/aaa///a/..../asas/as';
var str4 = '//b/c';
var str5 = path.join(str3,str4);
console.log(str5);  // ../a/a/aaa/a/..../asas/as/b/c
```

#### __dirname 获取当前目录的绝对路径

```javascript
// 3. 获取当前目录的绝对路径
console.log(__dirname);  // /Users/lanou3g/Desktop/H5-1207/ES6-node/node-03
```

#### __filename 获取当前文件的绝地路径

```javascript
// 4. 获取当前文件的绝对路径
console.log(__filename); // /Users/lanou3g/Desktop/H5-1207/ES6-node/node-03/01-path.js
```

#### isAbsolute 判断是否是绝对路径

```javascript
// 5.判断是否是绝对路径
var result = path.isAbsolute('./a/c/ds/a');
console.log(result);  // false
var result1 = path.isAbsolute(__dirname);
console.log(result1);  // true
```

#### resolve 相对路径转绝对路径

```javascript
// 6.把相对路径转为绝对路径
var str6 = path.resolve('./a/c/ds/a');
console.log(str6);  // /Users/lanou3g/Desktop/H5-1207/ES6-node/node-03/a/c/ds/a
```

#### dirname 获取路径 A 到路径 B 的相对路径

```javascript
// 7.获取路径 A 到路径 B 的相对路径
var str7 = path.dirname('./a/../b/v','./s/sc/as');
console.log(str7);  // ./a/../b
```

#### basename 获取文件路径的最后一部分

```javascript
// 8.获取文件路径的最后一个部分
var str8 = path.basename('./aa/bb.txt');
console.log(str8);  // bb.txt

// 9.获取文件的的文件名
var str9 = path.basename('./aa/bb.txt','.txt');
console.log(str9); // bb
```

#### extname 获取文件的后缀名

```javascript
// 10.获取文件的后缀名
var str10 = path.extname('./aa/bb.txt');
console.log(str10); // .txt
```

#### parse 解析路径

```javascript
// 11.解析路径
var str11 = path.parse('./aa/bb.txt');
console.log(str11);  // { root: '', dir: './aa', base: 'bb.txt', ext: '.txt', name: 'bb' }
```

#### format 路径编码

```javascript
// 12.路径编码,把对象转换为字符串
var str12 = path.format(str11);
console.log(str12);
```

### 2. jsonp 跨域问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jsonp</title>
</head>
<body>
    姓名: <input type="text" name="username" value="" id="user"> <br>
    年龄: <input type="text" name="age" value="" id="age">
    <button id="btn">点击</button>
    <div id="msg"></div>
</body>
</html>
<script type="text/javascript">
    var user = document.getElementById('user');
    var age = document.getElementById('age');
    var btn = document.getElementById('btn');
    var msg = document.getElementById('msg');

    btn.onclick = function () {
        var sc = document.createElement("script");
        sc.src = "http://127.0.0.1:8080/02-jsonp.js?username=" + user.value + "&age=" + age.value + "&cb=aa";
        document.body.appendChild(sc);
        document.body.removeChild(sc);
    }

    // 定义回调函数
    function aa(data) {
        msg.innerText = data;
    }
</script>
```

```javascript
var http = require('http');
var url = require('url');

var server = http.createServer(function (req,res) {
    // 获取前端传过来的数据,其中包含回调函数 cb
    var urlObj = url.parse(req.url,true);
    var name = urlObj.query.username;
    var age = urlObj.query.age;
    var cb = urlObj.query.cb;

    var str = "你好" + name + ",你今年" + age + "岁了!";
    res.end(cb + "('" + str + "')");
});

server.listen(8080);
console.log("服务启动成功");
```

### 3. express: nodeJs 框架 实质上并没有新的模块加入,只是把现有的模块重新封装

#### 路由

```javascript
var formidable = require('formidable');
var express = require('express');
var app = new express();

// 路由,不需要引 http 服务了

// get 的第一个参数: 用户请求的路径--Route的Path
// 第二个参数: 回调函数
app.get('/',function (req,res) {
    res.setHeader('content-type','text/html;charset=utf-8');
    console.log(req);
    res.send("<h1>行到水穷处</h1>");
});

app.get('/aa.html',function (req,res) {
    res.setHeader('content-type','text/html;charset=utf-8');
    // req.query 是前台发送过来的信息,她以json 的格式存储
    console.log(req);
    res.send("<h1>坐看云起时</h1>");
});

app.get('/act',function (req,res) {
    var name = req.query.name;
    res.send(name + "我要这铁棒有何用!");
});

app.listen(8080);
console.log("服务启动成功!");
```

```javascript
app.get('/02-post.html',function(req,res){
    // req.path 实质上就是第一个参数的实体
    console.log(req.path);  //  /02-post.html
    // res.sendFile(__dirname + '/02-post.html');
    res.sendFile(__dirname + req.path);
});

app.get('/02-post.css',function(req,res){
    res.sendFile(__dirname + req.path);
});

// 路径参数,就是说参数写在了路径上
app.get('/aaa/:name/:age',function (req,res) {
    // 路径参数的数据都存在 req.params里面,以 json 的格式存储的
    console.log(req.params);
    var name = req.params.name;
    var age = req.params.age;
    res.send("请求成功!name=" + name + ",age=" + age);
});

app.post('/post',function (req,res){
    var form = formidable.IncomingForm();
    form.parse(req,function(err,fields,files){
        // 获取从 html 中的用户名和年龄
        var name = fields.username;
        var age = fields.age;
        res.send("你好" + name + ",你今年" + age + "岁了!");
    });
});

// 终极写法
// * 代表所有的请求的路径
app.get('*',function (req,res) {
    res.sendFile(__dirname + req.path);
});

app.listen(8080);
console.log("服务启动成功!");
```

#### 中间件

- 中间件: 控制流程是否执行,中间件的 req 和 res 都是指的同一个对象,如果中间键没有停止,就会一直执行下去,数据也就一直向下传递

```javascript
/*
    中间件: 控制流程是否执行,中间件的 req 和 res 都是指的同一个对象,如果中间键没有停止,就会一直执行下去,数据也就一直向下传递
 */

var express = require('express');

var app = new express();

// 中间件的关键字是 use

// 国
app.use(function (req,res,next) {
    req.money = 100000;
    next();
});

// 省
app.use(function (req,res,next) {
    req.money -= 5000;
    next();
});

// 市
app.use(function (req,res,next) {
    req.money -= 2500;
    next();
});

// 县
app.use(function (req,res,next) {
    req.money -= 2000;
    next();
});

// 村
app.use(function (req,res,next) {
    req.money -= 100;
    next();
});

// app.all 不管什么操作,统一执行
app.all('*',function (req,res) {
   res.send("发钱了,发了" + req.money + "呢!");
});

app.listen(8080);
console.log("服务启动成功!");
```

#### 模板

- express 支持模板引擎
- 使用 ejs 模板需要安装

```javascript
// express 支持模板引擎
// 使用 ejs 模板需要安装


var express = require('express');
var app = new express();

// ejs需要设置 express 模板引擎
app.set('view engine','ejs');

// 设置模板引擎的位置
app.set('views',__dirname);

app.get('/abc/:name/:age',function (req,res) {
   // 渲染 参数1:模板的名称,参数2:执行的数据
   res.render('muban',{
      name:req.params.name,
      age:req.params.age
   });
});

app.listen(8080);
console.log("服务启动成功!");
```

