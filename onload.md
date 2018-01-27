## 详解浏览器渲染页面过程/控制台输出

[TOC]

###1.解析HTML文件，创建DOM树

- 自上而下，遇到任何样式（link、style）与脚本（script）都会阻塞（外部样式不阻塞后续外部脚本的加载）。

### 2.解析CSS

- 优先级：浏览器默认设置<用户设置<外部样式<内联样式<HTML中的style样式；
- 特定级：id数*100+类或伪类数*10+tag名称*1

### 3.将CSS与DOM合并，构建渲染树（renderingtree）

- DOM树与HTML一一对应，渲染树会忽略诸如head、display:none的元素

### 4.布局和绘制，重绘（repaint）和重排（reflow）

- 重排：若渲染树的一部分更新，且尺寸变化，就会发生重排；
- 重绘：部分节点需要更新，但不改变其他集合形状。如改变某个元素的颜色，就会发生重绘。

#### 1.重绘和重排何时会发生：

（1）增加或删除DOM节点；

（2）display:none（重排并重绘）；visibility:hidden（重排）；

（3）移动页面中的元素；

（4）增加或修改样式；（5）用户改变窗口大小，滚动页面等。

#### 2.如何减少重绘和重排以提升页面性能：

（1）不要一个个修改属性，应通过一个class来修改
错误写法：div.style.width="50px";div.style.top="60px";
正确写法：div.className+=" modify";
（2）clone节点，在副本中修改，然后直接替换当前的节点；
（3）若要频繁获取计算后的样式，请暂存起来；
（4）降低受影响的节点：在页面顶部插入节点将影响后续所有节点。而绝对定位的元素改变会影响较少的元素；
（5）批量添加DOM：多个DOM插入或修改，应组成一个长的字符串后一次性放入DOM。使用innerHTML永远比DOM操作快。（特别注意：innerHTML不会执行字符串中的嵌入脚本，因此不会产生XSS漏洞）。

 



—————————————————

### 5.控制台(console)

#### 控制台打印日志

```javascript
console.log("log");
console.info("info");
console.debug("debug");
console.error("error");
console.warn("warn");
```

#### 打印方法中的占位符

```javascript
console.log('%s 买了%d个西瓜,花了%f元钱.','小明',2,21.5);
```

#### 控制台分组打印/console.group()

```javascript
console.group('第一组');
console.log('第一组-1');
console.log('第一组-2');
console.groupEnd();

console.group('第二组');
console.log('第二组-1');
console.log('第二组-2');
console.groupEnd();
```

#### 控制台打印对象信息/console.dir()

```javascript
var svendInfo = {
  site:"http:svend.cc",
  github:"https://github.com/JSW5297",
  email:"jinshouw@163.com",
  sayHi:function(name){
    console.log('Hello '+ name);
  }
};
// 控制台打印对象信息
console.dir(svendInfo);
```

#### 控制台打印 DOM 节点或 XML/console.dirxml()

```javascript
// 控制台打印DOM节点或XML
var svendInfo = document.getElementById('svendInfo');
console.dirxml(svendInfo);
```

#### 判断表达式是否为真/console.assert()

```javascript
// 判断表达式是否为真
console.assert(true);
console.assert(1);
console.assert(true == false);
```

#### 将数据表格打印/console.table()

```javascript
// 将数据表格打印
var data = [
  {'索引':'1','名称':'蛋糕','数量':5},
  {'索引':'2','名称':'啤酒','数量':2}
];
console.table(data);
```

#### 计时/console.time()

```javascript
console.time('time-1');
for (let i = 0; i < 5; i++) {
  console.log(i);
}
console.timeEnd('time-1');
```

#### 清空控制台/console.clear()

```javascript
// 清空控制台
console.clear();
```

#### 输出样式

```javascript
console.log('%cHello World!', 'font-size:50px; color:green;')
```

#### 性能分析器/console.profile()

```javascript
function All(){
  for(var i=0;i<10;i++){
    funcA(2);
    console.log('----------');
  }
  funcB(20);
}

function funcA(count){
  for(var i=0;i<count;i++){
    console.log(i);
  }
}

function funcB(count){
  for(var i=0;i<count;i++){
    console.log(i);
  }
}

console.profile('性能分析器');
All();  // funA 执行10次, funB打印20个数
console.profileEnd('性能分析器');
```



