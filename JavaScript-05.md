## JavaScript PC 端事件/事件冒泡/事件捕获/回调函数/ ECMA5数组新方法/事件处理四种方式/ Event 事件对象

[TOC]

### 1.事件

#### 鼠标事件

- 单击事件 - onclick
- 鼠标按下 - onmousedown
- 鼠标抬起 - onmouseup
- 鼠标移入 - onmouseover/onmouseenter 后者不支持冒泡
- 鼠标移出 - onmouseout/onmouseleave 后者不支持冒泡
- 鼠标移动 - onmousemove
- 鼠标右键 - oncontentmenu - return false;阻止事件传递
- 取消文本被选中 - onselectstart return false;
- 鼠标双击 - ondbclick

```javascript
// 1.单击事件 down->up->click
var box = document.getElementById("box");
var box1 = document.getElementById("box2");
box.onclick = function(){
    console.log("单击...");
}
// 鼠标按下
box.onmousedown = function(){
    console.log("鼠标按下");
}
// 鼠标抬起
box.onmouseup = function(){
    console.log("鼠标抬起");
}

// 鼠标移入
box.onmouseover = function(){
    console.log("鼠标移入over");
}
// onmouseover 和 onmouseenter 的区别是后者不支持 冒泡
box.onmouseenter = function(){
    console.log("鼠标移入enter")
}

// 鼠标移除
box.onmouseout = function(){
    console.log("鼠标移出out");
}

// leave:在冒泡阶段不会执行,而 out 可以执行
box.onmouseleave = function(){
    console.log("鼠标移出leave");
}

// 鼠标移动
var index = 0;
box.onmousemove = function(){
    index++;
    console.log("鼠标移动" + index + "次");
}

// 鼠标右键
box1.oncontextmenu = function(event){
    console.log("鼠标右键");
    event.preventDefault(); // 阻止浏览器默认的行为
    return false; // 阻止默认
}

// 取消文本被选中
box1.onselectstart = function(){
    return false;  // 阻止拉取选中文本
}

// 鼠标双击
box1.ondblclick = function(){
    console.log("鼠标双击");
}

// 2. 取消绑定事件 event 事件对象
document.addEventListener("contextmenu",function(event){
    event.preventDefault();
    console.log(event);
    console.log("文档--右键");
    return false;  // 监听中无法阻止默认事件
});
```

#### 键盘事件

```javascript
username.onkeydown = function(){
    console.log("键盘按下.");
}

username.onkeypress = function(){
    console.log("按压....");
    console.log(this.value);  // 第一次执行 值 为空
}

username.onkeyup = function(){
    if(this.value.length >= 10){
        alert("超过十个");
    }
    console.log("键盘抬起....");
}

/*
 * 键盘事件可以使用 document 进行监听
 *  document,body,documentElement 都可以
 */
document.body.onkeyup = function(){
    console.log("文档:键盘弹起");
}
```

#### 表单事件

- 获得焦点 onfocus
- 失去焦点 onblur
- 表单重置 onreset
- 元素选中:onselect
- 用户输入 oninput 写一下触发一下
- 用户输入 onchange 写完失去焦点时触发一次

```javascript
username.onfocus = function(){
    console.log("获得焦点");
}
username.onblur = function(){
    console.log("失去焦点");
}

// 输入框改变时调用,输一次调一次
username1.oninput = function(){
  console.log("input:" + this.value)
}
//  输入框内容发生改变,并且失去焦点时调用
username1.onchange = function(){
    console.log("input --:" + this.value);
}

// 选择的时候:
username1.onselect = function(){
    console.log("开始选择:" + this.value);
}
```

#### 剪贴板事件

- 拷贝时触发 oncopy
- 剪切时触发 oncut
- 粘贴时触发 onpaste

```javascript
// 选择的时候:
username1.onselect = function(){
    console.log("开始选择:" + this.value);
}

// 拷贝的时候
username1.oncopy = function(){
    console.log("开始拷贝");
}
// 剪切的时候
username1.oncut = function(){
    console.log("开始剪切");
}
// 粘贴的时候
username1.onpaste = function(){
    console.log("开始粘贴");
}
```

#### 动画事件

- animationstart 动画开始时回调
- animationiteration 动画重复播放时调用
- animationend动画结束时调用

```javascript
// 监听
// 动画结束时回调
box.addEventListener("animationend",function(ev){
    alert("动画完了!");
});

// 动画开始时回调
box.addEventListener("animationstart",function(ev){

});
// 动画重复播放时触发
box.addEventListener("animationiteration",function(ev){

});
```

### 2.事件冒泡/事件捕获

```html
<body id="body">
    <div id="div1">
      <div id="div2">
        <p id="span">this is a span tag!</p>
      </div>
    </div>
    <script src="./js/jquery-3.1.1.min.js" charset="utf-8"></script>
    <script type="text/javascript">
      $("#body").bind("click",function(e){
        // e.target 表示被点击的目标
        alert("事件冒泡了！点击的元素是：" + $(e.target).attr("id") + " 单击事件绑定在Body上");
      });
    </script>
  </body>
```

```javascript
// 从上到下
window.onclick = function(){console.log("window");}
document.onclick = function(){console.log("html");}
document.body.onclick = function(){console.log("body");}
box1.onclick = function(){console.log("box1");}
box2.onclick = function(){console.log("box2");}
box3.onclick = function(){console.log("box3");}

/*
 * 事件冒泡:
 * 1.通过 onclick 方式添加的事件都是冒泡事件
 * (onmouseenter,leave不冒泡)
 * 2.通过监听方式绑定的事件,如果参数3默认(false)也是冒泡事件
 * 
 * 冒泡的开始:从被点击的元素开始,然后会继续往父元素上冒泡->body->html->window->丢弃
 * 冒泡过程中:只要元素绑定了单击事件,都会被执行.
 */
```

- 事件捕获

```javascript
<div id="box1">box1
    <div id="box2">box2
        <div id="box3">box3</div>
    </div>
</div>

box1.onclick = function(){
    console.log("冒泡: box1");
}

box2.onclick = function(){
    console.log("冒泡: box2");
}

box3.onclick = function(){
    console.log("冒泡: box3");
}

window.onclick = function(){
    console.log("冒泡: window");
}
/*
 * 捕获型事件:只能通过监听的方式 参数3是 true
 * 
 * 捕获是从外向内执行,window开始->html->...->事件源结束
 * 这个过程中,谁绑定了捕获型事件,就会被执行
 * 1.捕获型事件,只在捕获的过程中执行
 * 
 * 捕获完成后(window->点击的元素):接着从该元素冒泡出去
 * 
 * 2.冒泡型事件:只在冒泡过程中执行
 * 
 * 冒泡和捕获同时具备,先执行捕获,再执行冒泡,如果某个元素同时具备冒泡和捕获,从整体来看,先执行捕获,在执行冒泡,当执行到当前同时具备捕获和冒泡的元素上时,当前元素先执行冒泡,在执行捕获,然后从该元素冒泡出去.
 */

box1.addEventListener("click",function(){
    console.log("捕获: box1");
},true);

box2.addEventListener("click",function(){
    console.log("捕获: box2");
},true);
box3.addEventListener("click",function(){
    console.log("捕获: box3");
},true);
window.addEventListener("click",function(){
    console.log("捕获: window");
},true);
```

### 3.ECMA5 中数组新方法

#### forEach()

```javascript
var b = [1,2,3,4,5,6];
// current  当前项数值
// index    索引
// err      整个数组
b.forEach(function(current,index,err){
  // console.log("current = ",current);
  console.log("index = ",index);
  // console.log("err = ",err);
});
```

#### for in

```javascript
var obj = {
    name:'悟空',
    age:234,
    job:'取经'
}

for(var keys in obj) {
    console.log(keys + '=' + obj[keys]);  
}
// name=悟空
// age=234
// job=取经
```

#### map()

- map 需要每次返回,将返回的数据共同组成一个新的数组

```javascript
// map 函数
var a = [1,2,3,4,5,6,7,8];
var result = a.map(function(current,index,arr){
  //map需要每次返回，由返回的数据共同组成一个新数组
   return current + 10;
});
console.log(typeof(result)); // object
console.log(result);  // [ 11,12,13,14,15,16,17,18 ]
```

#### filter() 过滤器

- 测试数组的每个元素的函数 保留返回 true

```javascript
// filter 测试数组的每个元素的函数 保留返回 true
var a = [1,2,3,4,5,6,7,8];
var result1 = a.filter(function(e,i,a){
    if (e % 2 == 0) {
        return true;
    }
});
console.log(result1);
```

#### every()

- 测试数组的每个元素的函数,只有所有元素通过测试才返回true

```javascript
// every
var a = [1,2,3,4,5,6,7,8];
var ret = a.every(function(e,i,a){
     return i > 3;
  });
console.log(ret);//false
```

#### some()

- 测试数组的每个元素的函数,只要有一个元素通过测试就返回true

```javascript
// some
var a = [1,2,3,4,5,6,7,8];
var rets = a.some(function(e,i,a){
     return i > 3;
  });
console.log(rets);//true
```

#### reduce()

```javascript
pre   上一次调用回调返回的值，或者是提供的初始值（initialValue）        
cur   数组中当前被处理的元素          
index   当前元素在数组中的索引         
array   调用 reduce 的数组  
// reduce
var he = a.reduce(function(pre,cur,i,a){
  return pre + cur;
},0);
console.log(he);

var mul = a.reduce(function(pre,cur,i,a){
  return pre * cur;
},1);
console.log(mul);
```

#### indexOf()

- 判断数组是否含有指定元素

```javascript
// indexOf
console.log(a.indexOf(2)); //  下标位置 1
console.log(a.indexOf(2,3)); //  查找 2 从 下表位置为3开始
console.log(a.indexOf(19)); // -1 代表没有
```

#### find()

- 找到满足条件的第一个元素,并返回,未找到返回 undefined

```javascript
var number = [13,20,21,3];
var fin = number.find(function(value) {
    return value > 20;
});
console.log(fin);  // 21
```

### 4. join和split的区别

- join方法是将数组元素转化为字符串
- split 方法 是将字符串转换为数组对象

```javascript
var a = ['html','css','java','javascript'];
console.log(a.join("#"));
console.log(typeof(a.join())); // string
console.log(typeof(a));         // object
var b = "html#css#java#javascript";
console.log(b.split("#"));
console.log(typeof b);        //  string
console.log(typeof(b.split()));   // object
```

### 5. 事件处理的四种方式(事件绑定)

#### HTML事件处理

- 直接在标签上加事件

```html
<input type="button" name="" value="提交1" onclick="alert('点击1');">
```

#### DOM 0 级事件

```javascript
<input id="btn1" type="button" name="" value="提交2">
  var btn = document.getElementById('btn1');
  // onclick 绑定触发函数,只有最近的一次绑定有效
  btn.onclick = function(){
      console.log("快放假了!");
  }

  btn.onclick = function(){
      console.log("高兴了哦!");
  }
  
  // 取消绑定
  btn.onclick = null;
```

#### DOM 2 级事件 (标准情况)

```
obj.addEventListener("事件名", "事件处理函数", "布尔值")
 true 事件捕获方式
 false  事件冒泡

 obj.removeEventListener("事件名", "事件处理函数", "布尔值")
```

```JavaScript
<input id="btn2" type="button" name="" value="提交3">
var btn = document.getElementById('btn2');
/*
 * 2.监听器: 标准浏览器下方法: IE9+
 * 区别:可以绑定多个触发函数,并且同时有效
 * 
 * 参数1:绑定事件的类型 (click,dbclick,change,mouseover,mouseout)
 * 参数2:回调函数
 * 参数2:控住事件类型  捕获/冒泡 默认:false冒泡
 */

function listener() {
    console.log("我是监听器1");				
}
btn.addEventListener("click",listener,false);
btn.addEventListener("click",function(){
    console.log("我是监听器2");
},false);

/*
 * 取消绑定: 标准浏览器下方法: IE9+
 * 参数1:事件类型
 * 参数2:事件名称
 * 参数3:布尔值 -> 捕获/冒泡
 */
btn.removeEventListener("click",listener,false);

// 封装
function addEvent(ele,evType,callback){
    if(ele.attachEvent){
        ele.attachEvent(evType,callback);
    } else{
        ele.addEventListener(evType,callback);
    }
}

addEvent(btn1,"click",listener,false);
```

#### DOM 2级事件 (兼容IE)

```javascript
// 绑定事件
obj.attachEvent("on事件名", "事件处理函数")
// 取消绑定
obj.detachEvent("on事件名", "事件处理函数")

// IE 6,7,8
// 标准浏览器下报错,为了兼容先判断有没有,没有不执行后边的,利用了逻辑与的短路原理
btn.attachEvent && btn.attachEvent("onclick",listener);
btn.detachEvent && btn.detachEvent("onclick",listener);

function handel1(){
    alert("点击4");
    btn3.detachEvent('onclick',handel1);
}

btn3.attachEvent('onclick',handel1);
```

### 6.even事件对象

- event 事件对象，包含了一堆和该事件有关系的属性和方法
- 在事件处理函数内部，this完全等价于 event.currentTarget 指向的都是注册该事件处理程序的元素。
- 在事件处理函数内部，event.target 指向的都是触发该元素的该事件的<源头>

#### 事件类型 event.type

#### 事件来源(点击的是谁) event.target 

#### 绑定事件元素 event.currentTarget  直接在事件对象上查看是 null

#### 事件类型是否冒泡 event.bubbles

#### 左键还是右键 event.button

#### ALT 键: altKey

#### ctrl 键: ctrlKey

#### shift 键:shiftKey

#### 键盘值: keyCode

```javascript
document.onclick = function () {
  	/*
     * type: 事件类型
     */
  	console.log("type:",event.type);  // click
}

btn.onclick = function (event) {
      /*
      在事件处理函数内部：
      this完全等价于 event.currentTarget, 指向的都是注册该事件处理程序的元素!!!
      */
  
      console.log(this);
      console.log(event.currentTarget);
  
      /*
      在事件处理函数内部：
       event.target, 指向的都是 触发该元素的该事件的<源头>！！！！
      */
      console.log(event.target);
  	  // IE 下,是否阻止冒泡,默认是 false 
	  console.log("是否阻止冒泡?",event.cancelBubble);
  	  // 标准下阻止冒泡
      event.stopPropagation();
      // 阻止默认事件
      event.preventDefault();
      // 事件类型是否是冒泡
      console.log("冒泡吗?",event.bubbles);  // true
  	  // 判断是鼠标左键还是右键
	  console.log("左键是:",event.button);  // 左键是 0 右键是 1
  	  // 监听是否按住 ALT 键 ,shift 键 ,ctrl 键
	  console.log("按住ALT键了吗?",event.altKey);
	  console.log("按住Ctrl键了吗?",event.ctrlKey);
	  console.log("按住Shift键了吗?",event.shiftKey);
    };
```

#### 阻止事件传递

- event.stopPropagation( )   阻止 事件的传递  在onclick = function(){}  中
- event.preventDefault( )  阻止默认的行为
- event.stopImmediatePropagation( )   停止冒泡  在addEventListener() 中


```javascript
console.log(window.event);  // undefined

btn.onclick = function(ev){
  /*
   * 谷歌:两种方式都支持:
   * 火狐:只支持事件对象以参数形式获取,不支持全局 event
   * IE: 只能通过全局 event, 不能通过事件对象获取
   */

  // 兼容性写法:
  ev = ev || window.event;
  console.log(ev);
  console.log(window.event);
  // 是否取消冒泡  执行完,直接丢弃,不再冒泡
  // 1.IE 特有,但是现在新的浏览器都支持
  ev.cancelBubble = true;
  // 2.标准写法, IE 6 7 8不支持
  ev.stopPropagation();

  // 兼容性写法
  if(event.stopPropagation){
      // 2.标准写法, IE 6 7 8不支持
      event.stopPropagation();
  } else {
      // 1.IE 特有,但是现在新的浏览器都支持
      event.cancelBubble = true;
  }
}
```

#### 事件坐标点

```javascript
box.onclick = function(event){
    event = event || window.event;
    console.log(event);  // event 事件对象

    /*
     * clientX/Y:鼠标点参照浏览器页面左上角的间距
     * pageX/Y:鼠标点参照文档左上角的间距,低版本的 IE 不兼容
     * 
     * 上述两者关系:页面不滚动,两者相等
     * pageY = clientY + 滚上去的距离
     * 
     * 高版本的浏览器的一个属性
     * offsetX/Y:鼠标点参照点击元素本身左上角的间距
     * offsetY = pageY - 元素距离文档顶部的距离
     */

    // 浏览器的页面,不考虑文档的滚动
    console.log("clientX",event.clientX);
    console.log("clientY",event.clientY);
  
    // 文档的,考虑到了文档的滚动
    console.log("pageX",event.pageX);
    console.log("pageY",event.pageY);
  
    // 元素的,
    console.log("offsetX",event.offsetX);
    console.log("offsetY",event.offsetY);
}
```

### 9. 回调函数 callback

- 函数作为参数时,通常称该函数为回调函数(会在将来某个时刻执行)
- cllick 内部的函数作为回调函数使用,又称为事件处理函数
- 事件可以注册多个函数,触发事件在时候按照注册的顺序触发.








