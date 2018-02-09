## 移动端事件/移动端事件对象/touch 类/touch.js 框架

[TOC]

### 1.移动端鼠标滚轮事件

- 注意:这个事件具有很大的兼容性问题,在 Chrome 浏览器中使用 mousewheel ,而在Firefox 浏览器中这个设置确是无效的. 火狐特有的滚轮事件 DOMMouseScroll

#### wheelDelta 代表滚动的方向

- 正数代表向上滚动
- 负数代表向下滚动

```javascript
var index = 0;
// 不兼容火狐
document.onmousewheel = function(ev){
    ev = ev || window.event;
    /*
     * wheelDelta:
     * 正数: 向上滚动
     * 负数: 向下滚动
     */
    if(ev.wheelDelta < 0){
        index += 20;
        console.log("下滚动");
    } else {
        index -= 20;
        index = index <= 0 ? 0 : index;
        console.log("上滚动");
    }
    setScrollTop(index);
    ev.preventDefault();
};

function setScrollTop(value) {
    document.body.scrollTop = document.documentElement.scrollTop = value;
}
```

#### DOMMouseScroll 火狐特有的滚轮事件

-  ev.detail 存储方向 只有两个值
-  -1代表向上,+1代表相下

```javascript
/*
 * 火狐特有滚轮事件
 */
document.addEventListener("DOMMouseScroll",function(ev){
	console.log("火狐特有...");
    console.log(ev);  // 火狐没有 ev.wheelDelta 属性

    /*
     * ev.detail
     * -1 代表:向上
     * 1 代表:向下
     */
    console.log(ev.detail);
});
```

### 2.移动端事件对象

- event 事件对象在移动端和 PC 端拥有较小区别
- 移动端对象的考虑到有多根手指的操作,将一些手指信息存储在一个结合中.

#### event.target 绑定事件源(点击的是谁)

#### event.type 事件类型

#### event.targetTouches 保存触摸对象的手指信息,他是一个集合对象

#### event.touches: 保存屏幕对象的手指信息

```javascript
box.ontouchstart = function(ev){
    console.log("event事件对象:",ev);
    console.log("type:",ev.type);  // touchstart
    console.log("target:",ev.target);  // box 对象
    /*
     * targetTouches:保存触摸对象上的手指信息
     * touches: 保存屏幕对象上的手指信息
     */
    console.log("pageY:",ev.targetTouches[0].pageY);
    this.innerHTML = "现在屏幕上有" + ev.targetTouches.length + "根手指";
    this.innerHTML += "<hr/>现在屏幕上有" + ev.touches.length + "根手指";

    // 移动端要写:默认事件很多
    ev.preventDefault();
    // 停止事件冒泡
    ev.stopPropagation();
}
```

### 3.移动端事件 — touch 类

#### onclick 点击事件

- 这是移动端和 Pc 端通用的事件
- 问题: onclick 在移动端具有 200ms 到300ms 的延迟 

#### 手指按下事件 ontouchstart/touchstart

- 最开始不是 使用 ontouchstart 的方式,都是使用 监听的方式

```javascript
box.ontouchstart = function(){
    console.log("手指按下");
}
```

#### 手指抬起事件 ontouchend/touchend

```javascript
box.addEventListener("touchend",function(){
    console.log("手指抬起");
});
```

#### 手指移动事件 ontouchmove / touchmove

```javascript
/*
 * touchmove:手指移动
 */
var index = 0;
box.addEventListener("touchmove",function(){
    index++;
    console.log("move:",index);
    this.innerHTML = "move" + index;
});
```

#### 被迫取消 ontouchcancel / touchcancel

- 不会主动调用,突然来了电话等,突发事情,系统调用此方法,可以保存信息

```javascript
/*
 * touchcancel:被迫取消
 * 不会主动调用,突然来了电话等,突发事情,系统调用此方法,可以保存信息
 */
box.addEventListener("touchcancel",function(){
    console.log("被迫取消");
});
```

### touch.Js 框架

[Touch.js API 文档](http://cloudajs.org/docs/step4_API_Documentation#h2_7)

[百度touch.js API教程](http://blog.csdn.net/libin_1/article/details/50534611)

#### 旋转手势

```javascript
// 旋转
var angle = 0;
touch.on('#box', 'touchstart', function(ev) {
    // 开始旋转: touch方法
    ev.startRotate();
    //阻止默认:原生
    ev.preventDefault();
});
touch.on('#box', 'rotate', function(ev) {
    // ev.rotation:旋转的角度
    var totalAngle = angle + ev.rotation;
    if(ev.fingerStatus === 'end') { //这一句很重要
        angle = angle + ev.rotation;
    }
    this.style.webkitTransform = 'rotate(' + totalAngle + 'deg)';
    texts.innerText = "本次旋转角度为:" + ev.rotation + "度, 方向:" + ev.direction + ".";
});
```

#### 缩放手势

```javascript
// 缩放
var target = document.getElementById("box");
target.style.webkitTransition = 'all ease 0.5s';
touch.on('#box', 'touchstart', function(ev) {
    ev.preventDefault();
});
// 设置初始缩放比例
var initialScale = 1;
// 设置当前缩放比例
var currentScale;
touch.on('#box', 'pinchend', function(ev) {
    // 捏合的缩放倍数 缩小就是0-1
    currentScale = ev.scale - 1;
    currentScale = initialScale + currentScale;
    currentScale = currentScale > 5 ? 5 : currentScale; //自己调节可以放大的最大倍数
    currentScale = currentScale < 0.1 ? 0.1 : currentScale; //自己调节可以缩小的最小倍数
    this.style.webkitTransform = 'scale(' + currentScale + ')';
    show.innerText = "当前缩放比例为:" + currentScale + "倍.";
});
touch.on('#box', 'pinchend', function(ev) {
    initialScale = currentScale;
});
```

#### 左右滑动手势

```javascript
var w = 205;
var tw = box.offsetWidth;
var lf = document.getElementById("box").offsetLeft;
var rt = tw - w - lf;
show.innerText = "向左, 向右swipe滑动";
touch.on('#box', 'touchstart', function(ev) {
    ev.preventDefault();
});
var target = document.getElementById("box");
target.style.webkitTransition = 'all ease 0.2s';
touch.on(target, 'swiperight', function(ev) {
    this.style.webkitTransform = "translate3d(" + rt + "px,0,0)";
    show.innerText = "向右滑动.";
});
touch.on(target, 'swipeleft', function(ev) {
    show.innerText = "向左滑动.";
    this.style.webkitTransform = "translate3d(-" + this.offsetLeft + "px,0,0)";
});
```

#### 拖拽手势

```javascript
show.innerText = "抓取并拖拽目标元素";
touch.on('#box', 'touchstart', function(ev) {
    ev.preventDefault();
});
var target = document.getElementById("box");
var dx, dy;
// 拖拽手势
touch.on('#box', 'drag', function(ev) {
    dx = dx || 0;
    dy = dy || 0;
    var offx = dx + ev.x + "px";
    var offy = dy + ev.y + "px";
    this.style.webkitTransform = "translate3d(" + offx + "," + offy + ",0)";
});
touch.on('#box', 'dragend', function(ev) {9
    dx += ev.x;
    dy += ev.y;
    show.innerText = "当前x值为:" + dx + ", 当前y值为:" + dy + ".";
});
```

#### 单击/双击/长按手势

```javascript
touch.on('#box', 'touchstart', function(ev) {
    ev.preventDefault();
});
touch.on('#box', 'hold tap doubletap', function(ev) {
    // 动画完成后,清除 class
    this.className = "animated";
});
// 监听
// 动画结束时回调
box.addEventListener("animationend",function(ev){
    // alert("动画完了!");
    // 删除动画的 class
    this.className = "";
    this.style.border = "5px solid red";
});

// 动画开始时回调
box.addEventListener("animationstart",function(ev){});
// 动画重复播放时触发
box.addEventListener("animationiteration",function(ev){});
```

