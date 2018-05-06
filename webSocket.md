## webSocket 通信

[TOC]

### 1. webSocket 简介

- WebSocket 发起单个请求，服务端不需要等待客服端，客户端在任何时候都能发消息到服务端，减少了轮询时候的延迟。经历一次连接后，服务器能给客户端发多次。
- 基于http的实时消息是相当的复杂，在无状态的请求中维持回话的状态增加了复杂度，跨域也比较麻烦，使用ajax处理请求有序请求需要考虑更多。通过
  ajax进行交流也不简单。每一个延伸http功能的目的不是增加他的复杂度。websocket 可以大大简化实时通信应用中的链接。

### 2.Websocket的链接

- 调用WebSocket构造函数来创建一个WebSocket连接，构造函数会返回一个WebSocket实例，可以用来监听事件。
- WebSocket协议定义了两种URL方 案，WS和WSS分别代表了客户端和服务端之间未加密和加密的通信。WS(WebSocket)类似于Http
  URL，而WSS（WebSocket
  Security）URL 表示连接是基于安全传输层（TLS/SSL）和https的连接是同样的安全机制。

### 3.Websocket的事件

- Open：一旦服务端响应WebSocket连接请求，就会触发open事件。响应的回调函数称为onopen。open事件触发的时候，意味着协议握手结束，WebSocket已经准备好收发数据。如果你的应用收到open事件，就可以确定服务端已经处理了建立连接的请求，且同意和你的应用通信。
- Message：当消息被接受会触发消息事件，响应的回调函数叫做onmessage 。
- Error：如果发生意外的失败会触发error事件，相应的函数称为onerror,错误会导致连接关闭。如果你收到一个错误事件，那么你很快会收到一个关闭事件，在关闭事件中也许会告诉你错误的原因。而对错误事件的处理比较适合做重连的逻辑。
- Close：当连接关闭的时候回触发这个事件，对应onclose方法，连接关闭之后，服务端和客户端就不能再收发消息。可以调用close方法断开与服务端的链接来触发onclose事件。

### 4.Websocket的方法

- send()：一旦在服务端和客户端建立了全双工的双向连接，可以使用send方法去发送消息，当连接是open的时候send()方法传送数据，当连接关闭或获取不到的时候回抛出异常。一个通常的错误是人们喜欢在连接open之前发送消息。
- close()：使用close方法来关闭连接，如果连接以及关闭，这方法将什么也不做。调用close方法只后，将不能发送数据。

### 5.Websocket的属性

- readyState：WebSocket对象通过只读属性readyState来传达连接状态，它会更加连接状态自动改变。
- bufferedAmount：检查已经进入队列但还未被传输的数据大小。这个值不包含协议框架、操作系统缓存和网络软件的开销。
- protocol：在构造函数中，protocol参数让服务端知道客户端使用的WebSocket协议。而WebSocket对象的这个属性就是指的最终服务端确定下来的协议名称，当服务端没有选择客户端提供的协议或者在连接握手结束之前，这个属性都是空的。

### 6.NodeJS和 webSocket 实现简单聊天室

```html
<!-- 05-webSocket.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>webSocket聊天室</title>
    <link rel="stylesheet" href="./05-webSocket.css">
</head>
<body>
    <ul></ul>
    昵称: <input type="text" placeholder="输入昵称" value="" id="niName"> <br> <br>
    信息: <br>
    <textarea placeholder="输入聊天内容" id="msg" name="" id="" cols="30" rows="10"></textarea> <br>
    <button id="send">发送</button>
    <button id="close">退出聊天室</button>
</body>
</html>
<script type="text/javascript" src="jquery-3.1.1.js"></script>
<script type="text/javascript">
    // 1.实例化一个 webSocket 实体
    var ws = new WebSocket('ws://172.18.30.237:3000');

    // 2.检查是否链接成功
    ws.onopen = function(){
        // 设置链接成功
        // ws.readyState 可以获取链接的状态, 值为1 链接成功,值为0 链接失败
        var state = ws.readyState == 1 ? "成功" : "失败";
        console.log(state);
    };

    // 3.设置接收信息
    ws.onmessage = function(ev){
        $("ul").append("<li>"+ ev.data +"</li>");
    };

    // 4.关闭信息,服务器自动断开
    ws.onclose = function(ev){
        console.log(ev);
    }

    // 5.发送信息
    $("#send").click(function(){
        var userName = $.trim($("#niName").val());
        var msg =  $.trim($("#msg").val());

        // 把数据拼接成 json 发送给 websocket 服务器
        if(userName == "" || msg == "") {
            alert("请补全信息!");
        } else {
            var jsonStr = '{"name":"'+ userName +'","msg":"'+ msg +'"}'
            // 发送
            ws.send(jsonStr);
        }
    });

    // 6. 关闭链接
    $("#close").click(function(){
        ws.close();  // 关闭也就是下线了
    });
</script>
```

```css
/* 05-webSocket.css */
ul li {list-style-type: none;}
button {outline: none;cursor: pointer;padding: 5px;margin: 0 10px;border-radius: 5px;}
```

```javascript
/* 05-wenSocket.js */
var ws = require('ws');
var webServer = ws.Server;
// 实例化一个 webServer
var wss = new webServer({port:3000});
// 链接 websocket 使用 on 方法绑定链接
wss.on('connection',function(ws){
    // 接收信息 就是前台发送过来的json字符串
    ws.on('message',function(json){
        // console.log(json);
        var obj = JSON.parse(json);
        // 在 wss 上设置一个 user ,如果说用户退出的话,可以通过 user 获取到用户的姓名
        this.user = obj;
        // 广播信息
        wss.wifi(obj,1);
    });
    // 退出
    ws.on('close',function(){
        var name = this.user.name;
        wss.wifi(name,0);
    });
});
// 广播 广播时会有两种情况:
wss.wifi = function (info,m) {
    // wss.clients 当前链接该服务器的所有人 ,也就是所有的 wenSocket 实例
    wss.clients.forEach(function(n){
        console.log(info.name + ":" + info.msg);
        if (m == 1) {
            n.send(info.name + ":" + info.msg);
        }
        if (m == 0) {
            n.send(info + "下线了!");
        }
    });
}
```

```javascript
/* 05-http.js */
var express = require('express');
var app = new express();
app.get("*",function(req,res){
   res.sendFile(__dirname + req.path);
});
app.listen(8080);
console.log("服务启动成功!");
```

