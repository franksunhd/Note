## Vue 基础

[TOC]

### 1.简介

- 它是一个 MVVM 框架
- 两种方式使用
  - 直接引入 js, 类似 jquery 的引用
  -  创建 vue 脚手架,使用命令行工具操作 vue 类似刚刚认识的 angular5 ,Vue2.0以后该方式为主流方式

```html
<!--
	初始化一个 vue model
    1. 首先要有一个 vue 的视图容器,一般是在 body 里面设置一个 div
    2. js 中使用 el:'#app' 指的是视图的模型,它是指定要把运行的逻辑或者数据挂载到哪一个容器中,也就是el 指定了哪一个容器才能使用当前对象中的属性和方法
    3. data: 代表的是 vue 实例化的基本数据,以及存放的变量
	4. methods: 存储所有使用到的方法
-->
```

### 2. 数据绑定/ 属性绑定/事件绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基础语法</title>
    <style type="text/css">
        .aa {color: #f00;}
    	.bb {width: 200px;height: 200px;background: #f00;}
    </style>
</head>
<body>
<!--
    vue 简介:
    它是一个 MVVM 框架
    两种方式使用
    1. 直接引入 js, 类似 jquery 的引用
    2. 创建 vue 脚手架,使用命令行工具操作 vue 类似刚刚认识的 angular5 ,Vue2.0以后该方式为主流方式

    初始化一个 vue model
    1. 首先要有一个 vue 的视图容器,一般是在 body 里面设置一个 div
    2. js 中使用 el:'#app' 指的是视图的模型,它是指定要把运行的逻辑或者数据挂载到哪一个容器中,也就是el 指定了哪一个容器才能使用当前对象中的属性和方法
    3. data: 代表的是 vue 实例化的基本数据,以及存放的变量
	4. methods: 存储所有使用到的方法

    vue基础知识点:
    1. 数据绑定
        值绑定: {{}}  插值表达式 里面可以放数值,变量, js 语句,但是不要写多行 js
        指令绑定: v-html 和 v-text 都可以绑定数据
    2. 属性的绑定
        在 vue 中,没有对属性进行 html 属性和 dom 属性的区分
        在 vue 中不能使用插值表达式绑定属性,想要绑定属性使用 v-bind 指令绑定
        语法为:
        v-bind: 属性名='值/表达式'
        
        动态绑定 css
        1.动态改变 class
        2.通过 style 动态改变内联样式
        
        注意在指令中,一定是 js 方式,因为指令创建了一个 js 作用域,在作用域中使用 js 语句
        eg: v-bind:class="'aa'"
        
        v-bind 还有简写的方式
        v-bind:class 也可以写成  :class
	3. 事件绑定
		语法为: v-on:事件名="要执行的方法"
		可以简写为  @事件名 ="要执行的方法"
		
		修饰符: 具有特殊含义的指令
		.self 指的是只能获取他自己,不包括子元素,如果写在事件上,则表示只点击他自己,没有点击子元素
		.stop 指的是他可以阻止冒泡事件
		.once 只执行一次事件
		
		键盘事件:
		13代表 enter 键
		按下 enter 键触发事件 @keydown.13='要执行的事件'
		@keydown.ctrl  敲击 ctrl 键
		@keydown.alt
		
		
		同时按下 ctrl alt enter
		@keydown.ctrl.alt.13
-->
<div id="app1">
    <h1>{{message}}</h1>
    <h1 v-bind:class="'aa'" v-bind:title="str">{{2>1?'真':'假'}}</h1>
    
    <!-- v-html 和 v-text 的区别就像 innerHTML 和 innerText -->
    <h1 v-html='html'></h1>
    <h1 v-text="html"></h1>
    
    <h1 v-bind:style="'color:green;font-size:30px;'">砍头不要紧</h1>
    
    <!-- v-bind:class  的简写 :class -->
    <h1 :class="ClassName0">天地英雄气</h1>
    <!--绑定图片-->
    <div><img v-bind:src="src" v-bind:width="300"/></div>
    
    <!-- 绑定事件 -->
    <button v-on:click="clickFun()">点我查看小秘密</button>
    
    <!-- 获取当前事件操作的元素 -->
    <div v-bind:class="ClassName1" v-on:mouseenter="mouseEnter($event)"></div>
	<div @click.self="showHTML($event)"  v-bind:class="ClassName1">
		<p @click.stop="showHTML($event)">天生我才必有用</p>
	</div>
	<button v-on:click.once="onceFun()">点击我</button>
	<input type="text" @keydown.13="enterKeyUp()" value=""/>
	<input type="text" @keydown.alt="altKeyUp()" value=""/>
	<button @click="changeTxt()">点击</button>
</div>
</body>
</html>
<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript">
    // 实例化一个 vue 对象
    var vm1 = new Vue({
        el: '#app1',
        data: {
            message: '请开始你的表演',
            html: '<a href="http://www.baidu.com">百度</a>',
            str:"{{2>1?'真':'假'}}",
            ClassName0:"aa",
            ClassName1:"bb",
            src:"../img/m.png",
        },
        methods:{
        		clickFun:function(event){
        			alert("你好" + this.message);
        		},
        		mouseEnter:function(event) {
        			event.target.style.backgroundColor = '#f0f';	
        		},
        		showHTML:function(event){
        			alert(event.target.innerHTML);
        		},
        		onceFun: function() {
        			alert("百无一用是书生");
        		},
        		enterKeyUp: function() {
        			alert('你按下了 enter 键');
        		},
        		ctrlKeyUp: function() {
        			alert('你按下了 ctrl 键');
        		},
        		altKeyUp: function() {
        			alert('你按下了 alt 键');
        		},
        		changeTxt: function(event) {
        			this.message = '见血封喉';
        		}
        },
        // 钩子函数,它是在实例化加载成功之后执行的方法
        created: function(){
//      		var _this = this;
//      		setTimeout(function(){
//      			_this.message = '天将降大任于斯人也';
//      		},2000);
			
			setTimeout(()=>{
				this.message = '天将降大任于斯人也1';
			},2000);
        }
    });
	console.log(vm1);
</script>
```

### 3. 控制语句

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>控制语句</title>
		<style type="text/css">
			* {margin: 0;padding: 0;}
		</style>
	</head>
	<body>
		<!--
			Vue 内置的控制指令
			v-if: 可以单独使用,值为true,false
			v-else: 需要配合 v-if 使用
			v-else-if 需要配合 v-if 使用

			以上三个控制是否添加 dom 结构,如果为 true, 他所修饰的元素被写入到 dom 结构上,否则在dom上不显示

			v-show: 控制 css 级别的元素显示或者隐藏.实际上是 display: none 和 block 的转换

			v-for: 循环创建 dom 结构
			v-pre: 他所修饰的内容格式不变
			v-once: 只渲染一次
			
			v-for="形参 in 数组/对象"
			还可以在 v-for 的后面设置一个 key:value 虚拟的 dom, 他可以提高渲染的速率
			v-for="(item,index) in arr":key="value"
		-->
		<div id="app">
			<h1 v-if="bol">我是显示的</h1>
			<h1 v-else="bol">我是不显示的</h1>
			<h1 v-if="!bol">我是不显示的</h1>
			<button v-on:click="changeBol()">点击显示/隐藏</button>
			<h1 v-if="name=='悟空'">大师兄</h1>
			<h1 v-else-if="name=='八戒'">二师兄</h1>
			<h1 v-else>沙师弟</h1>
			
			<h1>
				<ul>
					<li v-for="(item,index) in dat" :key='item.name'>
						序号:{{index + 1}}--姓名:{{item.name}}--年龄:{{item.age}}
					</li>
				</ul>
			</h1>
			<h1 v-pre>'滴自己的汗,吃自己的饭'</h1>
			<h1 v-once>{{str}}</h1>
			<button @click="changeStr()">改变数据</button>
			<!-- 一般使用template控制for 循环 -->
			<template v-for="item in dat">
				姓名:{{item.name}}--年龄:{{item.age}}
			</template>
			<h1 v-show="bol">关公</h1>
			<h1 v-show="!bol">秦琼</h1>
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:'#app',
		data:{
		    bol:true,
		    name:'悟空',
		    dat:[
		    		{name:'悟空',age:223},
		    		{name:'八戒',age:232},
		    		{name:'沙僧',age:213}
		    ],
		    str:'二营长你他娘的意大利炮呢'
		},
		methods:{
			changeBol(){
				this.bol = !this.bol
			},
			changeStr(){
				this.str = '吃俺老孙一棒'
			}
		},
		// 钩子函数
		created:function(){}
	});
</script>
```

### 4.表单

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>表单</title>
	</head>
	<body>
		<!--
			v-model: 绑定 input 的 value 值可以实现双向绑定
		-->
		<div id="app">
			<input type="text" v-model="val" />
			<p>{{val}}</p>
			<!-- 单选 -->
			<label for="">男</label>
			<input type="radio" value="男" name="sex" v-model="sex"/>
			<label for="">女</label>
			<input type="radio" value="女" name="sex" v-model="sex"/>
			<p>{{sex}}</p>
			<!-- 复选 -->
			<h4>爱好:</h4>
			<template v-for="item in arr">
				<input type="checkbox" name="" v-model="checkArr" :value="item"/><label>{{item}}</label>	
			</template>
			<p>你选择了{{checkArr}}</p>
			
			<!-- 下拉框 -->
			<select v-model="selectVal">
				<option v-for="mo in arr">{{mo}}</option>
			</select>
			<p>您选择了{{selectVal}}</p>
			
			<textarea rows="" cols="" v-model="text"></textarea>
			<p>{{text}}</p>
		</div> 
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			val:'书生意气',
			sex:'男',
			arr:['苹果','橘子','梨','葡萄'],
			checkArr:[],
			selectVal:'苹果',
			text:'请输入你的文本...'
		},
		methods:{
			
		},
		created:function(){}
	});
</script>
```

### 5图书管理

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>图书管理</title>
		<link rel="stylesheet" href="../css/style.css" />
	</head>

	<body>
		<div id="app">
			<dl>
				<dt>
				    <span>序号</span>
				    <span>书名</span>
				    <span>价格</span>
				    <span>数量</span>
				    <span>总价</span>
				    <span>操作</span>
				  </dt>
				<dd v-for="(item,index) in dat">
					<span>{{index+1}}</span>
					<span>{{item.bookName}}</span>
					<span>{{item.price}}元</span>
					<span class="price">
				      <button class="jian" @click="reduceData(index)">-</button>
				      <em>{{item.num}}</em>
				      <button class="jia" @click="addData(index)">+</button>
				    </span>
					<span>{{item.num * item.price}}元</span>
					<div>
						<em @click="editData(index)">编辑</em>
						<em @click="delData()">删除</em>
					</div>
				</dd>
			</dl>

			<h2>
			  <span>总价:</span>
			  <span>{{sum}}</span>
			  <span>元</span>
			</h2>

			<h2 v-if="flag == 0">新建</h2>
			<h2 v-if="flag == 1">编辑</h2>

			<ul>
				<li>
					<label>书名:</label>
					<input type="text" v-model="bookName">
				</li>
				<li>
					<label>价格:</label>
					<input type="number" v-model="bookPrice">
				</li>
				<li>
					<label>数量:</label>
					<input type="number" v-model="bookNum">
				</li>
			</ul>
			<button class="add" @click="reset()">重置</button>
			<button class="add" @click="submitData()">提交</button>

		</div>
	</body>

</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el: "#app",
		data: {
			sum: 0,
			flag: 0, // 0代表新建 ,1代表编辑
			bookName: '',
			bookPrice: null,
			bookNum: null,
			myindex: null,
			dat: [{
					bookName: '三国演义',
					price: 10,
					num: 2
				},
				{
					bookName: '红楼梦',
					price: 20,
					num: 2
				},
				{
					bookName: '西游记',
					price: 10,
					num: 2
				},
				{
					bookName: '水浒传',
					price: 20,
					num: 2
				},
				{
					bookName: '三毛流浪记',
					price: 10,
					num: 2
				},
				{
					bookName: '高级程序设计',
					price: 20,
					num: 2
				}
			]
		},
		methods: {
			// 删除数据
			delData() {
				this.dat.splice(0, 1);
				this.sum = 0;
				this.priceAll();
			},
			// 编辑数据
			editData(str) {
				this.flag = 1;
				this.bookName = this.dat[str].bookName;
				this.bookPrice = this.dat[str].price;
				this.bookNum = this.dat[str].num;
				this.myindex = str;
			},
			// 点击 加 号
			addData(index) {
				this.dat[index].num++
				this.sum = 0;
				this.priceAll();
			},
			// 点击减号
			reduceData(index) {
				if(this.dat[index].num > 1) {
					this.dat[index].num--;
					this.sum = 0;
					this.priceAll();
				} else {
					if(confirm("确定要删除吗?")) {
						this.dat.splice(index, 1);
						this.sum = 0;
						this.priceAll();
					}
				}
			},
			// 计算总价
			priceAll() {
				for(var i = 0; i < this.dat.length; i++) {
					this.sum += this.dat[i].price * this.dat[i].num;
				}
				return this.sum;
			},
			// 重置数据
			reset() {
				this.flag = 0;
				this.bookName = '';
				this.bookPrice = null;
				this.bookNum = null;
				this.myindex = null;
			},
			// 点击提交按钮
			submitData() {
				if (this.bookName === '') {
			      alert('请填写完整的图书名');
			    }
			    if (this.bookPrice <= 0 || !this.bookPrice) {
			      alert('请填写正确的价格');
			    }
			    if (this.bookNum <= 0 || !this.bookNum) {
			      alert('请填写正确的图书数量');
			    }
				if(this.flag == 0) {  // 新建
					if (this.bookName !== '' && this.bookPrice !=='' && this.bookNum !== '') {
						var obj = {bookName:this.bookName,price:this.bookPrice,num:this.bookNum};
						this.dat.push(obj);
						this.bookName = '';
						this.bookPrice = null;
						this.bookNum = null;
						this.sum = 0;
						this.priceAll();
					}
				} else {  // 编辑
					if (this.bookName !== '' && this.bookPrice !=='' && this.bookNum !== '') {
						this.dat[this.myindex].bookName = this.bookName;
						this.dat[this.myindex].price = this.bookPrice;
						this.dat[this.myindex].num = this.bookNum;
						this.bookName = '';
						this.bookPrice = null;
						this.bookNum = null;
						this.sum = 0;
						this.priceAll();
					}
				}
			}
		},
		created: function() {
			this.priceAll();
		}
	});
</script>
```

