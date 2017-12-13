## JavaScript基础进阶

[TOC]

### 1.事件冒泡

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

### 2. 回调函数

- 函数作为参数时,通常称该函数为回调函数(会在将来某个时刻执行)
- cllick 内部的函数作为回调函数使用,又称为事件处理函数
- 事件可以注册多个函数,触发事件在时候按照注册的顺序触发.

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

### 5. 事件处理的四种方式

#### HTML事件处理

- 直接在标签上加事件

```html
<input type="button" name="" value="提交1" onclick="alert('点击1');">
```

#### DOM 0 级事件

```javascript
<input id="btn1" type="button" name="" value="提交2">
  var btn1 = document.getElementById('btn1');
  btn1.onclick = function(){
        alert("点击2");
  }
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
var btn2 = document.getElementById('btn2');
function handel(){
    alert("点击3");
    btn2.removeEventListener('click',handel,false);
}
btn2.addEventListener('click',handel,false);
```

#### DOM 2级事件 (兼容IE)

```javascript
obj.attachEvent("on事件名", "事件处理函数")
obj.detachEvent("on事件名", "事件处理函数")

function handel1(){
    alert("点击4");
    btn3.detachEvent('onclick',handel1);
}

btn3.attachEvent('onclick',handel1);
```

### 6.event对象

- event 事件对象，包含了一堆和该事件有关系的属性和方法
- 在事件处理函数内部，this完全等价于 event.currentTarget 指向的都是注册该事件处理程序的元素。
- 在事件处理函数内部，event.target 指向的都是触发该元素的该事件的<源头>

```javascript
document.onclick = function () {
      console.log(this);
      console.log(event.currentTarget);
      console.log(event.target);
    }

btn.onclick = function (event) {
      console.log(event.type);

      /*
      在事件处理函数内部：
      this完全等价于 event.currentTarget, 指向的都是注册该事件处理程序的元素!!!
      */
  
      console.log(this);
      console.log(event.currentTarget);
      
      event.currentTarget.style.color = "red";
  
      /*
      在事件处理函数内部：
       event.target, 指向的都是 触发该元素的该事件的<源头>！！！！
      */
      console.log(event.target);
    };
```

#### 阻止事件传递

- event.stopPropagation()   阻止 事件的传递  在onclick = function(){}  中
- event.preventDefault( )  阻止默认的行为
- event.stopImmediatePropagation()   停止冒泡  在addEventListener() 中











