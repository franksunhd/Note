## HTML5 新标签/URL(统一资源定位符)/HTML 5 Web存储

[TOC]

### 1.mark  - - 标记(行元素)

```html
H5新的标签<mark>标记</mark>
<!--
      mark 标记 背景黄色
      定义带有记号的文本。
      <行元素>
    -->
```

### 2.time - - 时间标签,没有任何样式,只有语义化(行元素)

```html
<time>2月10号</time>就可以放假了
```

### 3.nav - - 导航,没有任何样式.(块元素)

```html
<nav>导航栏</nav>
```

### 4.section - - 区段 (块元素)

```html
<section>第一个区段</section>
<section>第二个区段</section>
```

### 5.article - -文章段落 (块元素)

```html
<article>我是一段文章</article>
```

### 6.aside - - 侧边栏(块元素)

```html
<aside>定义侧边栏</aside>
```

### 7.ruby - - 定义 ruby注释 (行元素)

```html
<ruby>
  汉<rp>(</rp><rt>Han</rt><rp>)</rp>
  字<rp>(</rp><rt>Zi</rt><rp>)</rp>
</ruby>

<!-- 支持它的浏览器中注释在汉字上方,在 IE6,7中显示为 汉(Han)字(Zi) -->
```

### 8.wbr - - 单词换行

```html
hello Henry,<wbr>welcome to beijing.
<!--避免那种英文单词过长,在换行时造成的单词差分,加入<wbr>会使得长度较长的单词全部切换到下一行-->
```

### 9.fieldset - - 将表单内的元素进行分组(块元素)

```html
<fieldset></fieldset>
```

### 10.legend - - 给 fieldset设置标题

```html
<fieldset>
  <legend>fieldset标题</legend>
</fieldset>
```

### 11.meter - - 条状度量衡 (行元素)

```html
<meter low="20" high="80" value="90" min="0" max="100">
  您的浏览器不支持,请更新浏览器!
</meter>
```

### 12.progress - - 进度条 (行元素)

```html
<progress value="50" max="100">
  您的浏览器不支持,请更新您的浏览器
</progress>
```

### 13.details - - 下拉列表 (块元素)

### 14.summary - - 为details设置标题

```html
<details>
  <summary>点击选择</summary>
  <p>1.抽烟</p>  
  <p>2.喝酒</p>
  <div>3.烫头</div>
</details>
```

### 15.figure - - 独立的流内容(块元素)

```html
<figure>
  <img width="300" src="./img/1.png" alt="无法显示图片" />
  <figcaption>这是一张图片</figcaption>
</figure>
```

### 16.datalist - - 为 input 设置可能的选项列表

```html
<!-- 
	支持性较差 建议少用
	input 设置 list 属性 属性值为 datalist 的 id 属性值
-->
<input list="emails" name="email" />
<datalist id="emails">
  <option value="111"></option>  
  <option value="222"></option>
  <option value="333"></option>
</datalist>
```

### 17.audio - - 音频文件 (块元素)

```html
<audio src="./video/1.mp3" controls loop autoplay muted preload="auto">
  浏览器不支持,请升级浏览器或更换浏览器
</audio>
<!-- 
	controls:控制面板
	loop: 控制是否循环,属性默认循环
	autoplay:自动播放
	muted:设置静音
	proload="auto":当网页加载时,音频是否默认被加载,以及如何被加载
-->

<!--
	兼容性写法:
	使用<source>元素 src 引入资源
-->
```

### 18.viedo - - 视频文件 (块元素)

```html
<!--
	使用基本与音频文件用法类似
	只是视频文件多了属性: width 和 height
	poster:指定封面上的显示图片
	兼容写法与音频文件类似
-->

<video>
  您的浏览器不支持,请升级您的浏览器或者更换您的浏览器
</video>
```

## URL(统一资源定位符)

```javascript
var a = new URL("/", "https://developer.mozilla.org");
console.log(a.toString());  // https://developer.mozilla.org/

var b = new URL("https://developer.mozilla.org");
console.log(b.toString());    // https://developer.mozilla.org/

var c = new URL('en-US/docs', b);
console.log(c.toString());    // https://developer.mozilla.org/en-US/docs

var d = new URL('/en-US/docs', b);
console.log(d.toString());      //https://developer.mozilla.org/en-US/docs

var f = new URL('/en-US/docs', d);
console.log(f.toString()); // https://developer.mozilla.org/en-US/docs

var g = new URL('/en-US/docs', 'https://developer.mozilla.org/fr-FR/toto');
console.log(g.toString());   // https://developer.mozilla.org/en-US/docs

var h = new URL('/en-US/docs', a);
console.log(h.toString());  // https://developer.mozilla.org/en-US/docs

var k = new URL('http://www.example.com', 'https://developers.mozilla.com');
console.log(k.toString());  // http://www.example.com

var l = new URL('http://www.example.com', b);
console.log(l.toString());  //http://www.example.com
```

## HTML 5 Web存储

```javascript
if(typeof(Storage)!=="undefined")
{
    // 是的! 支持 localStorage  sessionStorage 对象!
    // 一些代码.....
} else {
    // 抱歉! 不支持 web 存储。
}
```

### 1. localStorage 用于没有时间限制的数据存储

- 本地持久存储, HTML5 新方法,只有标准浏览器支持
- 存储在了本地的浏览器目录中,不同浏览器不能共享localStorage 数据
- 因为持久存储,所以需要手动清除
- 可以在一个网站下实现页面之间数据的交互(页面之间是共享的,可以互相修改的)
- 同一个网站不同的页面之间的通信,也可以使用 localStorage.search

```javascript
console.log(localStorage);		
localStorage.name = "孙素";
console.log(localStorage.name);  // 孙素
```

#### 保存数据 localStorage.setItem(key,value)

#### 读取数据 localStorage.getItem(key)

#### 删除单个数据 localStorage.removeItem(key)

#### 清空所有数据 localStorage.clear()

#### 得到某个索引的key localStorage.key(index)

- 任意类型存储到 localStorage 都会被转换为 字符串类型

```javascript
localStorage.setItem("key0", 0);
localStorage.setItem("key1", 1);
localStorage.setItem("key2", 2);
console.log(localStorage.key0);  // 0

console.log(localStorage.age);

localStorage.age = 20;
// 任意类型存储到 localStorage 都会被转换为 字符串类型
localStorage.hobby = ["抽烟","喝酒","烫头"];
console.log(localStorage.hobby);  // 抽烟,喝酒,烫头
```

```javascript
/*
代码必须在服务器上测试，本地测试是不会触发的
当localStorage的值被其他页面修改时，当前页面的该事件会触发
如果是自己修改的，那么自己的事件不会触发
*/
window.onstorage = function(event){
  // 01页面
  console.log("event.key ", event.key);
  console.log("event.oldValue", event.oldValue);
  console.log("event.newValue", event.newValue);
}
```

```javascript
/*********************页面1*********************/
<body>
    <div id="box">
        <input type="text" name="user" id="user" value="蓝海"/>
        <button onclick="save()">保存</button>
    </div>
    <p>
        <a href="09-storage2.html" id="show" target="_blank">展示</a>
    </p>
    <script type="text/javascript">
        var users = null;
        // 旧的数据读出来
        var oldValue = localStorage.users;
        if(oldValue) {
            users = oldValue.split(",");
        } else {
            // undefined
            users = [];
        }
        function save(){
            users.push(user.value);
            // 数组存在本地
            localStorage.users = users;
        }
    </script>
</body>
/**********************页面2**************************/
<body>
    <ol id="list"></ol>
    <script type="text/javascript">
        var newArr = localStorage.users === undefined ? [] : localStorage.users.split(",");
        console.log(newArr);
        for(var i = 0, len = newArr.length; i < len; i++) {
            var lis = document.createElement("li");
            lis.innerText = newArr[i];
            list.appendChild(lis);
        }
    </script>
</body>
```

### 2. sessionStorage  针对一个 session 的数据存储

- sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除。


```html
<!--
localStorage:
	1.目前:50MB
	2.永久存储,不会自动清除,需要手动清除(用户直接在浏览器删除/开发者代码删除), 不清除的话,永久保存在本地
sessionStorage:
	1.目前:50MB
	2.关闭浏览器,缓存自动清除,再次打开浏览器没有记录
cookie:
	1.大小:4KB
	2.可以设置缓存的有效期,一般是以秒作为单位,
-->
```






