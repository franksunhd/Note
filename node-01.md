## Node.js

[TOC]

### 1.什么是Node.js?

- `Node.js` 是一个让 `JavaScript` 运行在服务端的开发平台

### 2. http 模块

```js
// 创建一个 http 服务
// 引入 http 模块

var http = require('http');

// 创建一个服务
var server = http.createServer(function(req,res) {
    // req:request 从前台传来的信息(传参)
    // res:response  服务器发送给前端的信息(响应)

    // 设置 utf-8编码格式
    res.setHeader('content-type','text/html;charset=utf-8');
    // end 方法把组装好的信息,发送给前台. end方法是 res 执行的最终方法,也就是说 end 是最后执行的方法,在 end 之后执行方法,没有效果
    // end 的参数只能是字符串

    res.end('马瘦毛长蹄子肥');
});

// 监听端口
server.listen(8080);
console.log("服务启动成功!");
```

### 3.获取请求的 url

```javascript 
// 如果请求 aa.html 返回粒粒皆辛苦 否则返回 野火烧不尽
var http = require('http');
var server = http.createServer(function (req,res) {
    res.setHeader("content-type","text/html;charset=utf-8");

    // console.log(req.url);
    if(req.url == '/aa.html') {
        res.end('粒粒皆辛苦!');
    } else {
        res.end("野火烧不尽");
    }
});

server.listen(8080);
console.log("服务启动成功!");
```

### 4. 引入 url 模块  — 操作url

```javascript
var http = require('http');
// 引入 url 模块
var url = require('url');

var server = http.createServer(function (req,res) {
    res.setHeader("content-type","text/html;charset=utf-8");
    // url模块 处理 前端通过 url 传到后台的数据
    var objUrl = url.parse(req.url,true);
    console.log(req.url);  // /aa.html
    console.log(objUrl);  // Url对象

    res.end('红军不怕远征难!' + objUrl.query.name);
});
server.listen(8080);
console.log("服务器启动成功!");
```

### 5. 自定义的模块

```javascript
// 引入模块
var tian = require('myindex');
// 调用
tian.addFun();
/*
    node 官方给出的模块 叫原生模块
    node 自定义的模块 叫文件模块
    文件模块如果执行在引用模块的那个 js 的相同目录下,会直接执行
    如果文件模块在 node_modules 文件夹中,它会一直的寻找这个文件模块,不管是不是在同一个目录下,直到找到这个文件为止
 */

// myindex/index.js 文件
function add() {
    console.log("你好");
}

module.exports = {
    addFun:add
}
```

### 6. 什么是 npm

```javascript
/*
    npm 是一个包管理工具
    npm 安装模块使用 npm install 模块名 -g
        如果加 -g 说明是全局安装
    npm 模块卸载: npm uninstall 要卸载的模块名
    也可以在前面加 sudo 表示临时的超级权限
*/

/*
    REPL(read eval print loop) 交互式解释器
 */
```

### 7. util 引入工具模块

- 三个常用功能: 继承,输出对象,验证类型

#### 继承

```javascript
var util = require('util');
// inherits:继承

// 创建一个父类
function Yase(name,age,job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.fun = function () {
        console.log(this.name);
    }
}
Yase.prototype.jobFun = function () {
    console.log(this.job);
}

// 创建一个子类
function Libai(name,job) {
    Yase.call(this);
    this.name = name;
    this.job = job;
}

// 继承方法 inherits 两个参数:(子类,父类)
// inherits 只能继承原型上的方法
util.inherits(Libai,Yase);

// 创建一个子类实例
var ys = new Libai("李白","诗人");
ys.jobFun();
ys.fun();
```

#### 输出对象

```javascript
var util = require('util');
function Aa() {
    this.name = "王维";
    this.age = 10;
    this.job = "诗人";
}

var shi = new Aa();
// 输出对象类型的形式,但实质上还是字符串
var obj = util.inspect(shi);
console.log(obj,typeof obj); // Aa { name: '王维', age: 10, job: '诗人' } string
```

#### 验证类型

```javascript
var util = require('util');
// 验证类型
var arr = [1,2,3,4];
var str = "绝胜烟柳满皇都";
console.log(util.isString(str)); // true
console.log(util.isArray(arr));  // true
```

### 8. events 事件模块

- 又叫观察者模式, 类似 js 中的绑定
- 又叫发布订阅模式 类似 js 中的监听

```javascript
/*
    events 事件模块
    又叫观察者模式, 类似 js 中的绑定
     又叫发布订阅模式 类似 js 中的监听
 */

// 引入事件模块
var event = require('events');
// 所创建的对象,要使用 event 中的方法,可以使用 util 中的继承方法来完成
var util = require('util');

// 创建一个女孩对象
function Girl(name) {
    this.name = name;
};
// 创建一个男孩对象
function Boy(name,res) {
    this.name = name;
    this.res = res;
};

// 给女孩加事件,要继承 event 的事件
util.inherits(Girl,event);

// 实例化一个小乔
var xiaoqiao  = new Girl('小乔');

// 实例化 boy
var caocao = new Boy('曹操',function () {
    console.log('曹操兵发东吴,抢小乔!');
});

var zhouyu = new Boy('周瑜',function () {
    console.log('周瑜火烧赤壁,救小乔!')
});


// 设置最大的监听数量.可以设置绑定 某一个事件 的最大的值
// xiaoqiao.setMaxListeners(2);
// 设置小乔出嫁事件
xiaoqiao.addListener('chujia',function () {
    console.log("小乔出嫁了!");  // 小乔出嫁了
});
xiaoqiao.addListener('chujia',caocao.res);  // 曹操兵发东吴,抢小乔
xiaoqiao.addListener('chujia',zhouyu.res);  // 周瑜火烧赤壁,救小乔
xiaoqiao.addListener('chujia',function () {
    console.log("小乔伤心欲绝,出家了!");  // 小乔伤心欲绝,出家了
});

xiaoqiao.addListener('huijia',function () {
    console.log("左手一只鸡,右手一只鸭!");
});

// once 只执行一次, 该方法指的是执行的时候执行代码只执行一次
xiaoqiao.once('over',function () {
    console.log('曹操败走华容道!');
});
xiaoqiao.once('over',function () {
    console.log('Game Over!');
});

// 解除绑定
xiaoqiao.removeListener('chujia',caocao.res);
xiaoqiao.removeListener('chujia',zhouyu.res);

// 解除出嫁
xiaoqiao.removeAllListeners('chujia');

// 执行出嫁事件
xiaoqiao.emit('chujia');
xiaoqiao.emit('over');  // 曹操败走华容道
xiaoqiao.emit('over');  // Game Over
```

### 9. querystring 模块: 处理 name=aa&age=12&job=www 类型的数据

```javascript
/*
    querystring 模块: 处理 name=aa&age=12&job=www 类型的数据
 */

// application/x-www.form-urlencoded 类型的数据
var formString = require('querystring');

// 对字符串进行解析
var str1 = "name=亚瑟&age=18&job=战士";

var json1 = formString.parse(str1);
console.log(json1,typeof json1);  // { name: '亚瑟', age: '18', job: '战士' } 'object'

// 键值一样,相应的值会被解析为数组
var str2 = "name=亚瑟&age=18&job=战士&job=刺客&job=BOSS";
var json2 = formString.parse(str2);
console.log(json2,typeof json2);  // { name: '亚瑟', age: '18', job: [ '战士', '刺客', 'BOSS' ] } 'object'


// 还可以把 json 对象转为 application/x-www.form-urlencoded 类型的数据

var json3 = {
    name:'铁木真',
    age:72,
    job:['可汗','大王']
}

// 可以设置分隔符(&) 和 分配符(=)
var str3 = formString.stringify(json3,'||','==');
console.log(decodeURI(str3));  // name==铁木真||age==72||job==可汗||job==大王
```

### 10. 文件系统模块

#### 读取文件 fs.readFile

```javascript
/*
    文件系统模块:
 */
var fs = require('fs');

// readFile(文件路径,编码格式,回调函数) 读取文件
// 回调函数有两个参数:(error,data)
fs.readFile('aa.txt','utf8',function (err,data) {
    console.log(data);
    console.log(err);
});

// 同步读取,不用执行回调函数,返回的就是文件的内容
var data = fs.readFileSync('aa.txt','utf-8');
console.error(data);
```

#### 写入文件 fs.writeFile

````javascript
// writeFile(文件路径,要写入的内容,修改的范围,回调函数) 写入文件
// 修改的范围:值为 a,则是追加, w 为覆盖
// 回调函数只有一个参数: err
var fs = require('fs');
function read(OldPath) {
    fs.readFile(OldPath,'utf-8',function (err,data) {
        if (err) {
            console.log("读取失败")
        } else {
            write(NewPath,data);
        }
    });
}

function write(NewPath,str) {
    // 设置追加的内容
    // var str = "唐僧师徒四人西天取经" + "\n";
    fs.writeFile(NewPath,str,{flag:'a'},function (err) {
        if(err) {
            console.error('写入失败');
        } else {
            console.log('写入成功');
        }
    });
}
// 拷贝文件
function copy(OldPath,NewPath) {
    fs.readFile(OldPath,'utf-8',function (err,data) {
        if (err) {
            console.log("读取失败")
        } else {
            fs.writeFile(NewPath,data,{flag:'a'},function (err) {
                if(err) {
                    console.error('写入失败');
                } else {
                    console.log('写入成功');
                }
            });
        }
    });
}
copy('aa.txt','bb.txt');
````

#### 追加内容 js.append

```javascript
/*
    fs-append: 追加
 */
var fs = require('fs');
// appendFile(文件路径,内容,回调函数)
fs.appendFile('bb.txt','\n我不是归人',function (err) {
    if (err){
        console.error("追加失败");
    } else {
        console.log('追加成功');
    }
});

```

### 11. 目录操作

#### 创建目录

```javascript
var fs = require('fs');
fs.mkdir('./mk','0777',function (err) {
   if (err){
       console.error("创建失败");
   } else {
       console.error("创建成功");
   }
});
```

#### 重命名目录

```javascript
// 重命名目录
// fs.rename(oldPath,newPath,回调函数)
var fs = require('fs');
fs.rename('mk','mkdir',function (err) {
    if (err){
        console.error("重命名失败");
    } else {
        console.error("重命名成功");
    }
});
```

#### 删除目录

```javascript
var fs = require('fs');
// fs.rmdir(目录名,回调函数)
fs.rmdir('mkdir',function (err) {
    if (err){
        console.error("删除失败");
    } else {
        console.error("删除成功");
    }
});
```

#### 查看目录详情 stat

```javascript
var fs = require('fs');
// fs.stat(目录名,回调函数)
fs.stat('mk',function (err,data) {
    if(err){
        console.error("查询出错");
    } else {
        console.log(data);
    }
});
```

#### 查看文件是否存在 exists

```javascript
var fs = require('fs');
// fs.exists(文件路径,回调函数);
// 回调函数的参数为一个 boolean 值
fs.exists('mk',function (bool) {
    if (bool) {
        console.log("有这个文件");
    } else {
        console.log("没有这个文件");
    }
});
```

### 12.流操作 stream

```javascript
/*
    stream
 */
var stream = require('stream');
var fs = require('fs');

// 流操作, 主要操作 大 数据

// 创建一个可读流
var rs = fs.createReadStream('/Users/lanou3g/Downloads/新年舞.mp4');

// 创建一个可写流
var ws = fs.createWriteStream('./mk/新年舞.mp4');
// 把可读流的资源放到可写流里面.完成复制

/*
var timer = 0;
// 循环复制,每一次的循环大约传送 64kb 的资源
rs.on('data',function (chunk) {
    timer++;
    ws.write(chunk,function () {
        console.log("复制成功" + timer);
    });
});
*/
//  复制的终极方法
rs.pipe(ws);
```

```javascript
var fs = require('js');
function copy(readFile,writeFile) {
    // 创建一个可读流
    var rs = fs.createReadStream(readFile);

    // 创建一个可写流
    var ws = fs.createWriteStream(writeFile);
    rs.pipe(ws);
}
```

### 13.formidable 非原生的模块 处理 form 表单数据

- 必须先安装,再使用,它是专门处理 form 表单的提交文件的模块.

```javascript
/* post: */
// formidable 模块: 非原生模块,必须先安装,再使用,它是专门处理 form 表单的提交文件的模块.
var formidable = require('formidable');
var fs = require('fs');
var http = require('http');

var server = http.createServer(function (req,res) {
   res.setHeader('content-type','text/html;charset=utf-8');

   if (req.url == '/post.html') {
       fs.readFile('./11.html','utf-8',function (err,data) {
           if(err){
               console.log('查询出错');
           } else {
               res.end(data);
           }
       })
   } else if (req.method  == 'POST'){
       if(req.url == '/info'){
           //  实例化一个 formidable
           var form = new formidable.IncomingForm();
           // parse 方法处理数据 err 为错误信息, fields 为前台传过来的文字信息, files 为前台传过来的文件信息
           form.parse(req,function (err,fields,files) {
               // console.log(fields);
               // console.log("----------");
               // console.log(files);

               // 创建一个可读流,先从前台的数据中获取临时路径
               var path = fs.createReadStream(files.pic.path);
               // 创建一个可写流,存储前台传过来的数据
               var ws = fs.createWriteStream('./mk/' + files.pic.name);
               path.pipe(ws);
               res.end("你好" + fields.username + ',你去' + fields.job + '吧!');
           });
       }
   }
});

server.listen(8080);
console.log("服务启动成功!");
```

