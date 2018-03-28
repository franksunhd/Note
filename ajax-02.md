## PHP中与ajax的交互/跨域请求 jsonp

[TOC]

### 1.ajax - get 请求

```html
<!--
    前端发起请求(ajax) -> 服务器 -> 服务器接收请求 -> 
    -> 服务器执行事件 ->服务器把执行的数据返回给前端 -> 前端处理数据
-->
<!--
    1.form 
    2.websocket 即时通信
    3.ajax 
    4.a标签href
-->

姓名: <input type="text" id="username" value="" /><br />
年龄: <input type="text" id="age" value="" /><br />

<button id="btn">提交</button>
<p id="msg"></p>

<script type="text/javascript">
    var name1 = document.getElementById("username");
    var age = document.getElementById("age");
    var btn = document.getElementById("btn");
    var msg = document.getElementById("msg");
    // 原生 ajax 局部刷新
    // 异步请求:客户端向服务器发送请求,不需要等待这个请求是否得到回应,其他代码正常执行,
    // 			如果请求成功,返回请求的数据,不对其他代码造成影响.
    // 同步请求:客户端向服务器发送请求,需要等到这个请求完成之后,其他代码才可以执行,这样会造成浏览器
    // 			假死的现象.
    // 一般都是异步请求.

    // ajax 使用场景:提交数据,显示实时数据,今日头条,新浪微博的新闻更新

    // ajax 的流程:
    // 1. 创建 XMLHttpRequest 对象
    // 2. 设置请求的 url
    // 3. 发送请求给服务端
    // 4. 注册事件
    // 5. 在事件中获取返回的数据并处理数据

    btn.onclick = function(){
        // 1.创建 XMLHttpRequest 对象 
        // IE 7及其以上含有 XMLHttpRequest 对象,所以可以直接创建,但是 IE6及其以下没有
        if(window.XMLHttpRequest){
            var xhr = new XMLHttpRequest();
        } else {
            var xhr = ActiveXObject('Microsoft.XMLHTTP');
        }

        // 监听 statechange事件
        xhr.onreadystatechange = function(){
            // xhr.status 返回的状态码
            // 1开头 已经接受请求,正在处理当中
            // 2开头 数据处理成功
            // 3开头 重定向,请求地址发生变化时的状态码
            // 4开头 客户端错误
            // 5开头 服务端错误(503,504 代表请求当时错误)

            // xhr.readyState 一般的 XMLHttpRequest请求会经历的几个状态,直到请求被处理,请求数据才会响应到客户端
            // 0:代表还没有调用 open()方法
            // 1:载入,已经调用 send 方法正在执行
            // 2.载入完成, send 方法已经执行完成,已经接受到全部的响应内容
            // 3.交互,解析内容
            // 4.解析完成,可以使用
            if(xhr.readyState == 4) {
                if(xhr.status >= 200 && xhr.status <300 || xhr.status == 304) {
                    // 操作成功
                    msg.innerHTML = xhr.responseText;
                } else {
                    // 操作失败
                    msg.innerHTML = "请求失败";
                }
            }
        }
        // onreadystatechange 一般放在 open 之前,执行却在其后

        // open方法 参数1,请求方式,参数2,请求的url
        xhr.open('GET','02-ajax-GET.php?name='+ name1.value +'&age='+ age.value);
        // send方法 get请求将数据放到 url 上
        xhr.send();
    }
</script> 
```

```php
// php 文件
<?php
	header("Content-Type:text/html;charset=UTF-8;");
	
	$name = $_GET['name'];
	$age = $_GET['age'];
	
	echo "你好{$name},你今年{$age}岁了!";
?>
```

### 2.ajax - post 请求

```html
姓名: <input type="text" id="username" value="" /><br />
年龄: <input type="text" id="age" value="" /><br />

<button id="btn">提交</button>
<p id="msg"></p>

<script type="text/javascript">
    var name1 = document.getElementById("username");
    var age = document.getElementById("age");
    var btn = document.getElementById("btn");
    var msg = document.getElementById("msg");
    btn.onclick = function(){
        var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : ActiveXObject('Microsoft.XMLHTTP');				

        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4) {
                if(xhr.status >= 200 && xhr.status <300 || xhr.status == 304) {
                    msg.innerHTML = xhr.responseText;
                } else {
                    msg.innerHTML = "请求失败";
                }
            }
        }
        xhr.open('POST','03-ajax-post.php',true);

        // 发送数据按照 form 表单的格式进行发送
        // 需要在 http 头部设置请求头,里面必须是 key->value
        // Content-Type 文件类型
        // Content-length 文件长度
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        // 数据放到 send 里面参数的样式为 name=aa&age=bb&job=cc
        xhr.send("name="+ name1.value + "&age=" + age.value);
    }
</script>
```

```php
<?php
	header("Content-Type:text/html;charset=UTF-8;");
	
	$name = $_POST['name'];
	$age = $_POST['age'];
	
	echo "你好:{$name},你今年{$age}岁了!";
?>
```

### 3. 封装 ajax

```javascript
// 封装 ajax

/* 参数格式
{
	url: 接口地址
	type:get/post
	data:{} json 格式的数据最后变化为 name=aa&age=bb&job=cc
	fun:回调函数
}
*/
function ajax(obj) {
	// 检测用户是否输入请求类型,有,转为大写,没有返回 get
	var type = obj.type ? obj.type.toUpperCase() : 'GET';
	var arr = [];

	for(v in obj.data) {
		arr.push(v + '=' + obj.data[v]);
	}

	// 把数组转换为字符串,用 & 链接
	var data = arr.join("&");
	
	// 创建对象
	var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP');
	// 监听状态
	xhr.onreadystatechange = function() {
		if(xhr.readyState == 4) {
			if(xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
				obj.success(xhr.responseText);
			} else {
				console.log("请求失败");
			}
		}
	}
	
	if(type == 'GET') {
		xhr.open('GET',obj.url + '?' + data);
		xhr.send();
	}else {
		xhr.open('POST',obj.url);
		xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
		xhr.send(data);
	}
}
```

```javascript
// 使用
ajax({
    url:'02-ajax-GET.php',
    data:{
        name:"悟空",
        age:18
    },
    success: function(data){
        alert(data);
    }
});
```

### 4. jsonp 跨域请求

```html
<!--
    基础:
    同源策略:它是一种约定,是浏览器的基本核心的安全功能,如果缺少了同源策略,浏览器正常的功能将将会受到影响

    所有的浏览器都支持同源策略

    域名: 每一个网站都有自己的服务器,每个服务器都有一个 IP 地址,每一个 ip 地址都有他指定的域名,
    域名有一级域名,二级域名,三级域名

    http://a(三级域名).aa(二级域名).com(一级域名)  越往后范围越大,输入之后会进行 DNS 解析

    JS 同源策略:
    js 规定 协议,域名,端口都一致则为同源
    1. 协议不同
        http://www.baidu.com 和 https://www.baidu.com
    2. 域名不同
        http://www.baidu.com 和 http://www.sina.com
    3. 端口号不同
        http://www.baidu.com:8080 和 http://www.baidu.com:8088
    4. 父子级域名
        http://www.a.baidu.com 和 http://www.b.baidu.com

    只有 js 才会考虑同源跨域问题, 
    img,a,iframe,link,script,在浏览器加载的时候不用考虑跨域问题,
    但是浏览器设置了权限,所以想要跨域也不是那么随意.

    js 解决跨域问题:
    1. jsonp: 虽然 js 有同源策略,但是 script 没有,所以可以使用
    2. html5 新增方法: postMessage()
    3. iframe:  配合 js 解决跨域问题
    4. 后台CORS方法: 也就是设置接口全网可调用

    jsonp 跨域的实现步骤:
        1.创建 script 标签
        2.在 script标签上添加 src = 路径,该路径是要跨域请求的路径,在路径的最后要加上一个回调函数,要保证本页面有要执行的回调函数
        3.把 script 标签放到 body 中,写入立即执行
        4.删除该 script 标签
-->
```

```javascript
<script src="07-jsonp.php?name=wukong&age=18&fun=aa" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
    function aa(data) {
        alert(data);
    }
</script>
```

```php
<?php
	header('Content-Type:text/html;charset=UTF-8;');
	
	$name = $_GET['name'];
	$age = $_GET['age'];
	$fun = $_GET['fun'];
	
	$str  = "你好:{$name},今年{$age}岁了!";
	
//	echo "{$fun}('{$str}')";
	
	echo $fun."('".$str."')";
?>
```

### 5.jsonp实例

```php
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>jsonp实例</title>
	</head>
	<body>
		姓名: <input type="text" id="username" value="" /><br /> 
		年龄: <input type="text" id="age" value="" /><br />
		<button id="btn">提交</button>
		<p id="msg"></p>
	</body>

</html>
<script type="text/javascript">
	var name1 = document.getElementById("username");
	var age = document.getElementById("age");
	var btn = document.getElementById("btn");
	var msg = document.getElementById("msg");
	
	btn.onclick = function(){
		// 1.创建 script 标签
		var scom = document.createElement("script");
		scom.src = "http://172.18.30.237/PHP%E4%BB%A3%E7%A0%81/PHP/php04-ajax/07-jsonp.php?name="+ name1.value +"&age=" + age.value + "&fun=aa";
		// 把创建的标签放到 body 中立即执行
		
		document.body.appendChild(scom); 
		// 删除标签
		document.body.removeChild(scom);
	}
	
	// 声明回调函数
	function aa(data){
		msg.innerHTML = data;
	}
</script>
```

```php
// php 文件
<?php
	header('Content-Type:text/html;charset=UTF-8;');
	
	$name = $_GET['name'];
	$age = $_GET['age'];
	$fun = $_GET['fun'];
	
	$str  = "你好:{$name},今年{$age}岁了!";
	
//	echo "{$fun}('{$str}')";
	
	echo $fun."('".$str."')";
?>
```

### 6. jquery - jsonp

```php
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>jq-jsonp</title>
	</head>
	<body>
		姓名: <input type="text" id="username" value="" /><br /> 
		年龄: <input type="text" id="age" value="" /><br />
		<button id="btn">提交</button>
		<p id="msg"></p>
	</body>
</html>
<script src="jquery.min.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	$("#btn").click(function(){
		$.ajax({
			// 数据类型 json/jsonp
			dataType:'jsonp',
            
			// jsonpCallback:回调函数名,默认是 ?
			jsonpCallback:"aa",
            
			// jsonp 传入的 aa 的键值
			jsonp:"fun",
            
			type:'get',
			url:"http://172.18.30.237/PHP%E4%BB%A3%E7%A0%81/PHP/php04-ajax/07-jsonp.php",
			data:{
				name:$('#username').val(),
				age:$('#age').val()
			},
			success:function(data){
				$('#msg').text(data);				
			}
		});
	});
</script>
```

```php
// php 文件
<?php
	header('Content-Type:text/html;charset=UTF-8;');
	
	$name = $_GET['name'];
	$age = $_GET['age'];
	$fun = $_GET['fun'];
	
	$str  = "你好:{$name},今年{$age}岁了!";
	
//	echo "{$fun}('{$str}')";
	
	echo $fun."('".$str."')";
?>
```

### 7. jquery 简写 jsonp

```php
// $.get(url(URL拼接数据),回调函数)
// $.post(url,data,回调函数)

$.get('02-ajax-GET.php?name=悟空&age=12',function(data){
    console.log(data);
});

$.post('03-ajax-post.php',{name:'wukong',age:12},function(data){
    console.log(data);
});
```

