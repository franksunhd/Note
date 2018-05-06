## Vue 基础

[TOC]

### 1. 计算属性

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<!--
			vue 中可以使用{{}} 来展示相对比较简单的数据,如果要展示比较庞大的或者逻辑比较复杂的数据,{{}} 就会有它的局限性,不利于操作,难以维护,
			所以使用计算属性(computed) 来展示数据
			
			计算属性的优点:
			1.数据没有变化的时候,优先读取计算属性里面的值
			2.他有 set 和 get 方法可以灵活设置
			
		-->
		<div id="app">
			<h1>{{str1}}</h1>
			<template v-for="item in arr1">
				<p>{{item}}</p>
			</template>
			<h1>{{showTxt}}</h1>
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			str:'青龙白虎',
			arr:[1,2,3,4,5,6,7,8,9,10]
		},
		methods:{},
		// 计算属性的钩子函数
		computed:{
			str1:function(){
				return this.str + ",朱雀玄武"; 
			},
			arr1:function(){
				// filter 过滤方法 参数为一个 回调函数,它是书写过滤规则的
				return this.arr.filter(function(n){
					return n%2 == 0;
				});
			},
			showTxt:{
				// 每一个计算属性的方法里面都有两个函数,一个是 set, 一个是 get ,默认是 get
				// 先 get 再 set
				set:function(value){
					// 参数为 该数据原来的值
					console.log("set");
					this.str += value; 
				},
				get:function(){
					console.log("get")
					return this.str += '孰能生巧';
				}
			}
		}
	});

	vm1.showTxt = '孔子东游';
</script>
```

### 2. watch 监听数据

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>数据监听</title>
	</head>
	<body>
		<div id="app">
			<label for="">姓名1:</label>
			<input type="text"  v-model="val"/> <br />
			<label for="">姓名2:</label>
			<input type="text"  v-model="name"/> <br />
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			val:'天苍苍,野茫茫',
			name:'风吹草低见牛羊'
		},
		// 数据监听的方法
		watch:{
			// 监控数据需要写数据的名称为 watch 的属性名
			// 它的值是一个函数,该函数有两个参数,第一个参数为变化后的值,第二个参数为变化前的值
			val:function(newVal,oldVal){
				console.log("新=" + newVal);
				console.log("旧=" + oldVal);
			}
		}
	});
	// 在外部进行监听,使用 $watch 方法,
	// 第一个参数为 要监听数据的变量名,第二个方法是监听的回调函数
	vm1.$watch('name',function(newName,oldName){
		console.log("新=" + newName);
		console.log("旧=" + oldName);
	});
</script>
```

### 3. 生命周期

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>生命周期</title>
	</head>
	<body>
		<div id="app">
			<input type="text" v-model="a"/>
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			a:3
		},
		created:function(){
			// 该方法在实例化创建之后执行
			console.log("create方法= " + this.a);
		},
		beforeCreate:function(){
			// 在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
			console.log("beforeCreate方法");
		},
		beforeMount:function(){
			// 只有在实例化之后,也就是在执行了挂载之后也就是指定了 el 之后调用
			console.log("beforeMount方法");
		},
		mounted:function(){
			// 只有在 mounted 之后才能执行一系列的 dom 操作
			// 可以在该函数里面使用加载立即执行的方法
			console.log("欢迎 mounted方法");
		},
		beforeUpdate:function(){
			// 当数据发生变化时,或者 view 视图重新绘制的时候执行该方法
			console.log("beforeUpdate方法");
		},
		updated:function(){
			// 数据或者 dom 发生改变时
			console.log("updated 方法");
		},
		beforeDestroy:function(){
			// 实例销毁之前调用
			console.log("beforeDestroy");
		},
		destroyed:function(){
			// 实例销毁的时候被调用,该方法调用后, vue 实例就被销毁
			console.log("destroyed 方法");
		}
	});
	// 综上,都是 vue 的生命周期函数,也叫钩子函数
	// 常用的: mounted(欢迎提示),methods(方法),computed(监听)
</script>
```

### 4.数组和对象检测

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>数组和对象检测</title>
	</head>
	<body>
		<!--
			检测数组和对象数据的变动
			1. 数组更新检测
				数组的更新方法,数组的内容变化,视图内容就会变化
				push pop shift unshift splice sort
				
				Vue.set(实例中的数组或者对象,下标/key,要更新的值)
			
				在 vue 中 使用 filter,map,slice 方法返回的都是数组,不会引起视图的更新,需要给老数组重新赋值
				注意: this.arr[index] = val 也不会引起视图的改变
			2. 对象的更新检测
				对象通过键名,更新 value, 是可以引起视图的更新,需要注意的是:
				对已有对象再次新加或者删除,不会引起视图的变化
				如果要同时更新多个值
				Object.assign()
		-->
		<div id="app">
			<template v-for="item in arr">
				<p>{{item}}</p>
			</template>
			<button @click="change()">点击改变数据</button>
			<hr />
			<template v-for="item in girls">
				<p>{{item.name}} == {{item.age}}</p>
			</template>
			<hr />
			<template v-for="(item,key) in boys">
				<p>{{key}}:{{item}}</p>
			</template>
			<button @click="del()">删除hobby</button>
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			arr:[1,2,3,4,5,6,7,8,8,9,10],
			girls:[
				{name:"安其拉",age:23},
				{name:"王昭君",age:34},
				{name:"杨玉环",age:35},
				{name:"小乔",age:18}
			],
			boys:{
				name:"亚瑟",
				age:23,
				job:'战士'
			}
		},
		methods:{
			change(){
				this.arr[1] = 10;
				console.log(this.arr);
				this.girls[1].name = '甄姬';
				this.boys.name = '姜子牙';
				this.boys.love = '兵法';
				// 数组改变值
				Vue.set(this.arr,1,100);
				// 对象改变值
				Vue.set(this.boys,'age','19')
				// 对象添加多个值
				this.boys = Object.assign({},this.boys,{sex:'男',hobby:'钓鱼'})
				console.log('已经执行了');
			},
			del(){
				// 删除数据
				Vue.delete(this.boys,'hobby');
			}
		},
		mounted:function(){
			this.change();
		}
	});
	
	vm1.$set(vm1.arr,2,'一段神话');
	// 外部删除 sex
	vm1.$delete(vm1.boys,"sex");
</script>
```

### 5.自定义指令

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>自定义指令</title>
		<style type="text/css">
			.aa {
				width: 200px;
				height: 200px;
				background: indianred;
			}
		</style>
	</head>

	<body>
		<!--
			自定义的指令
			当需要对 dom 进行底层操作,使用自定义指令
			
			创建全局指令:directive
			
			Vue.directive('指令名',{ 指令内容 });
			指令内容对象一般包含四个方法.
			bind:指令第一次绑定到 dom 元素的时候触发
			inserted: 指令所在的元素插入到父节点的时候调用
			update: 指令所在的元素值发生改变的时候调用
			unbind: 解绑的时候触发
		-->
		<!-- 第一个 vue 视图 -->
		<div id="app">
			<div v-abc="{color:'#f00'}" class="aa">第一个视图</div>
			<hr />
			<div v-jubu="{color:'#0f0'}" class="aa">第1.1个视图</div>
		</div>
		<hr />
		<!-- 第二个 vue 视图 -->
		<div id="bpp">
			<div v-abc="{color:'#f00'}" class="aa">第二个视图</div>
		</div>
	</body>

</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	// 全局指令
	// 先指令,
	Vue.directive('abc', {
		// 第一个参数为当前绑定的元素,第二个参数为指定的值
		bind: function(el, val) {
			console.log(el, val);
			el.onmouseenter = function() {
				el.style.backgroundColor = val.value.color;
			};
			el.onmouseleave = function() {
				el.style.backgroundColor = 'indianred';
			};
		},
		update: function(el, val) {
			console.log(el, val);
			el.onmouseenter = function() {
				el.style.backgroundColor = val.value.color;
			};
			el.onmouseleave = function() {
				el.style.backgroundColor = 'indianred';
			};
		}
	});

	// 简写: 当 bind 和 update 一致的时候,不管其他的钩子函数,可以写成简写的方式
	Vue.directive('abc', function(el, val) {
		el.onmouseenter = function() {
			el.style.backgroundColor = val.value.color;
		};
		el.onmouseleave = function() {
			el.style.backgroundColor = 'indianred';
		};
	});
	// 创建局部指令
	// 后实例化
	var vm1 = new Vue({
		el: '#app',
		data:{},
		methods:{},
		directives:{
			jubu:{
				bind:function(el,val){
					console.log(el,val);
					el.onmouseenter = function() {
						el.style.backgroundColor = val.value.color;
					};
					el.onmouseleave = function() {
						el.style.backgroundColor = 'indianred';
					};
				},
				// 需要访问该指令所绑定元素的父级,所以要写在 inserted 中
				inserted:function(el,val){
					console.log(el.parentElement);
				}
			}
		}
	});
	var vm2 = new Vue({
		el: "#bpp"
	})
</script>
```

### 6.过滤器

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>过滤器</title>
	</head>

	<body>
		<!--
		 	过滤器关键字:filter
		 	第一个参数: 过滤器的名字
		 	第二个参数: 回调函数,参数1:要过滤的值,参数2,3...要过滤的参数列表
		 	Vue.filter('过滤器名字',function(要过滤的值,arg1,arg2){}),
		-->
		<div id="app">
			<p>{{12.34|currency('¥',2)}}</p>
			<p>{{123.4| addTxt('¥',2) }}</p>
		</div>
	</body>

</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	// 全局过滤
	Vue.filter('currency', function(value, arg1, arg2) {
		if(!arg1) {
			return '$' + value;
		} else {
			if(arg2) {
				return arg1 + value.toFixed(arg2);
			} else {
				return arg1 + value;
			}
		}
	});
	// 局部过滤
	var vm1 = new Vue({
		el: "#app",
		data: {},
		methods: {},
		// 局部过滤,关键字 filters
		filters: {
			addTxt: function(value, arg1, arg2) {
				if(!arg1) {
					return '$' + value;
				} else {
					if(arg2) {
						return arg1 + value.toFixed(arg2);
					} else {
						return arg1 + value;
					}
				}
			}
		}
	})
</script>
```

### 7.组件

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>组件</title>
	</head>

	<body>
		<!--
			组件: 是 vue 的核心部分,组件一旦创建完成,就可以重复使用
			
			创建全局组件
			组件的命名:
			1.组件的命名要区别于 html 标签
			2.组件的命名原则最好为 a-a 的形式
			3.支持驼峰命名, myTop, 引用的时候使用 my-top的方法使用
			
			注册全局组件,尽量使用驼峰命名法
			
			关键字为component 第一个参数为 组件名,第二个参数组件的实体
			Vue.component(组件名,{})
			
			组件的显示内容都赋值给 template 显示在 html 中
			
			组件模板可以写在 template 标签中, 在其中必须是一个整体标签, template 有一个 id 值,作为外部引入的标识
			此刻创建的组件里面 写 template:'#id' 即可使用
		-->
		<div id="app">
			<my-top></my-top>
			<my-head></my-head>
			<ten></ten>
			<get-all></get-all>
			<set-all></set-all>
		</div>
	</body>
</html>
<template id="com">
	<div>
		<p>滕王高阁临江储</p>
		<p>佩玉鸣鸾罢歌舞</p>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	Vue.component('myTop', {
		// 模板
		template: '<p>刑天舞干戚</p>'
	});

	Vue.component('myHead', {
		// 模板
		template: `
		<pre>
			人之初
			性本善
		</pre>
		`
	});
	Vue.component('Ten', {
		// 模板
		template: '#com'
	});

	var vm1 = new Vue({
		el: "#app",
		data:{},
		methods:{
			
		},
		// 注册局部组件,创建组件的关键字为 components
		components:{
			getAll:{
				template:'<h1>天生我才必有用</h1>'
			},
			setAll:{
				template:'#com'
			}
		}
	});
</script>
```

### 8.组件处理数据

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>组件处理数据</title>
	</head>
	<body>
		<div id="app">
			<get-all></get-all>
			<hr />
			<du-shu></du-shu>
			<hr />
			<get-all></get-all>
			<hr />
			<set-all></set-all>
			<hr />
			<temp></temp>
			<hr />
			<guan-fang></guan-fang>
		</div>
	</body>
	<!-- 
		组件的 data 和 vue 实例中的 data 不同,组件中的 data 是一个函数,返回一个对象
	-->
</html>
<template id="alldom">
	<div>
		<p>{{txt}}</p>
		<p>{{aaa}}</p>
	</div>
</template>

<template id="gg">
	<div>
		<template v-for="item in arr">
			<p>{{item}}</p>
		</template>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	Vue.component('getAll',{
		template:'<p>{{name}},你今年{{age}}岁了</p>',
		data:function() {
			return {
				name:'孙文',
				age:18
			}
		}
	});
	
	var temp = {
		template:'#alldom',
		data:function(){
			return {
				txt:'百无一用是书生',
				aaa:'万紫千红一片绿'
			}
		}
	}
	
	// 全局引用外部模板
	Vue.component('duShu',temp);
	
	var vm1 = new Vue({
		el:"#app",
		// 创建局部组件
		components:{
			getAll:{
				template:'#alldom',
				data:function(){
					return {
						txt:'百无一用是书生',
						aaa:'万紫千红一片绿'
					}
				}
			},
			// 引入外部组件1
			setAll:temp,
			// 引入外部组件2
			temp,  // 相当于 temp:temp
			guanFang:{
				template:'#gg',
				data:function(){
					return {
						arr:[1,2,3]
					}
				}
			}
 		}
	});
</script>
```

### 9.组件获取属性值

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>组件获取属性值</title>
	</head>
	<body>
		<div id="app">
			<child :tag="'红消香断有谁怜'"></child>
			<hr />
			<child :tag="txt"></child>
			<hr />
			<aa :url="url1"></aa>
		</div>
	</body>
</html>
<template id="child">
	<div>
		<p v-show='bol'>{{tag}}</p>
		<button @click="change()">点击切换</button>
	</div>
</template>

<template id="aa">
	<a :href="url">百度</a>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	
	var vm1 = new Vue({
		el:'#app',
		data:{
			txt:'天生我才必有用',
			url1:'http://www.baidu.com'
		},
		methods:{},
		components:{
			aa: {
				template:"#aa",
				props:['url']
			},
			child:{
				template:'#child',
				// 组件中设置属性
				props:['tag'],
				data:function(){
					return {
						bol:true
					}
				},
				methods:{
					change(){
						this.bol = !this.bol;
					}
				}
			}
		}
	});
</script>
```

