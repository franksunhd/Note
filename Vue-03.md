## Vue 基础

[TOC]

### 1. props多样性(子元素的值传给父元素)

- 按钮在子元素中,点击按钮触发事件,此时要获取父元素设置值的方法,使用 this.$parent方法

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>props多样性</title>
	</head>
	<body>
		<div id="app">
			<h1>{{str}}</h1>
			<get-all :str-mo="'雍正'" :my-obj="{name:'忽必烈',age:20}"></get-all>
			<hr />
		</div>
	</body>
</html>
<template id="tem">
	<div>
		<p>{{strMo}}</p>
		<template v-for="(item,key) in myObj">
			<p>{{key}}:{{item}}</p>
		</template>
		<p>{{msg}}</p>
		<button @click="chuan()">点击获取子元素的值</button>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var temp = {
		template:'#tem',
		data:function(){
			return {
				msg:'传位于四阿哥---子'
			}
		},
		props:{
			// 属性名尽量不要驼峰,若写成驼峰需要大写转-小写
			strMo:{
				type:String,
				default:'康熙'
			},
			myObj:{
				type:Object,
				default:function(){
					return {
						name:'康熙'
					}
				},
				required:true
			}
		},
		methods:{
			// 子组件调用父组件的方法
			chuan(){
				// $parent 获取父组件,也就是通过 this.$parent 访问父组件的所有内容
				this.$parent.shou(this.msg);
			}
		}
	}
	/*
	 * 实现了将父元素的值改为子元素的值
	 * 传给八阿哥 改为了 传给四阿哥
	 */
	var vm1 = new Vue({
		el:"#app",
		data:{
			str:'传位于八阿哥---父'
		},
		methods:{
			//设置父元素的接收方法
			shou(info){
				// 改变 str 的值
				this.str = info;
			}
		},
		components:{
			getAll:temp
		}
	});
</script>
```

### 2. Refs属性(父元素的值传给了子元素)

- 按钮设置在了父组件上, son(子) 组件上设置 ref 属性,父组件的方法上使用 this.$refs 获取其属性值,设置给子元素传的值,子元素获取值就传给了子元素

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>refs</title>
	</head>
	<body>
		<!--
			this.$refs 获取所有的 携带 ref 属性的元素集合
			this.$refs.你的元素的ref值,就可以获取到 ref 所在的元素
		-->
		<div id="app">
			<son ref="mm"></son>
			<hr />
			<p>{{str}}</p>
			<button @click="chuan()">点击获取父元素的值</button>
		</div>
	</body>
</html>
<template id="son">
	<div>
		<p>{{msg}}</p>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var son = {
		template:"#son",
		data:function(){
			return {
				msg:'能全世界能全我---子'
			}
		},
		methods:{
			// 子接收
			show(info){
				this.msg = info;
			}
		}
	}
	
	/*
	 * 这个是实现了将子元素显示的值改为父元素的值,
	 * 也就是 父值传给 子值
	 * 能全世界能全我 改为 半哭苍生半哭公
	 */
	var vm1 = new Vue({
		el:"#app",
		data:{
			str:'半哭苍生半哭公---父'
		},
		methods:{
			// 父传子方法
			chuan(){
				this.$refs.mm.show(this.str);
			}
		},
		components:{
			son
		}
	});
</script>
```

### 3. $emit(子元素的值传给父元素)

- 按钮加在了子组件中,子组件中绑定一个 自定义的 事件名(方法名) 在操作自组件时,使用 $emit 触发自定义的事件,自定义的事件执行父组件的方法,从而将子元素的值传给了父组件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<!--
			1.在子组件上绑定一个 自定义的 事件名(方法名) aa-fun
			2.在子组件的操作中,使用 $emit 方法触发 aa-fun 事件,
			  进而执行绑定在 aa-fun 上的父组件的方法,
			  从而达到将子元素的值传给父元素
		-->
		<div id="app">
			<h1>{{str}}</h1>
			<hr />
			<mingyue @aa-fun="shou($event)"></mingyue>
		</div>
	</body>
</html>
<template id="tem">
	<div>
		<h2>{{msg}}</h2>
		<button @click="chuan()">点我接收子元素数据(子传父)</button>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	// 使用$emit 触发事件
	var mingyue = {
		template:'#tem',
		data:function(){
			return {
				msg:'相见为兄弟,何必骨肉亲--- 子'
			}
		},
		methods:{
			chuan(){
				// $emit第一个参数直接命名事件的事件名,不要写成驼峰,多个单词使用-链接
				// 该事件绑定在组件上,一旦触发,组件上的绑定页立即触发
				// 第二个参数是要传的值
				this.$emit('aa-fun',this.msg);
			}
		}
	};
	
	var vm1 = new Vue({
		el:"#app",
		data:{
			str:'莫愁前路无知己---父'
		},
		methods:{
			shou(info){
				this.str = info;
			}
		},
		components:{
			mingyue
		}
	});
</script>
```

### 4. $emit( 子元素的值传给另一个子元素) \$on 监听事件

- 这种传值需要借助一个公共的实例对象作为媒介, 按钮在一个子组件中,绑定一个方法,方法中使用 $emit绑定一个自定义的事件,并且传值,然后在,另一个子组件中使用 mounted方法监听,使用 \$on 获取通过公共实例传的 元素值

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>$emit(子串子)</title>
	</head>
	<body>
		<div id="app">
			<h1>{{txt}}</h1>
			<hr />
			<son2></son2>
			<hr />
			<son1></son1>
		</div>
	</body>
</html>
<!--子组件1-->
<template id="son1">
	<div>
		<h2>{{msg}}</h2>
		<button @click="add()">点击传值</button>	
	</div>
</template>
<!--子组件2-->
<template id="son2">
	<h1>{{str}}</h1>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var son1 = {
		template:"#son1",
		data:function(){
			return {
				msg:"同心同德---son1"
			}
		},
		methods:{
			add(){
				// 此刻需要传值操作,使用公共的实力对象作为媒介,
				// 也就是在 bus 上使用$emit 进行绑定事件
				bus.$emit('addss',this.msg);
			}
		}
	}
	
	var son2 = {
		template:"#son2",
		data:function(){
			return {
				str:"同室操戈---son2"
			}
		},
		methods:{
			
		},
		// 钩子函数
		mounted:function(){
			// $emit 监听事件是否触发,使用 $on 进行监听
			// $on 的 this 指的不是当前组件的 this, 所以要监听并修改组件的内容的时候,要改变 this 的指向
			// 推荐两种方法,第一种: var _this  = this 第二种在函数的最后 bind(this)
			// $on 两个参数,第一个参数,要监听的事件,第二个参数为回调函数,处理数据使用
			bus.$on('addss',function(value){
				this.str = value;
			}.bind(this))
		}
	}
	/*
	 * 子组件相互传值,需要借助公共的vue实例
	 */
	var bus = new Vue();

	var vm1 = new Vue({
		el:"#app",
		data:{
			txt:"同归于尽---父"
		},
		methods:{},
		components:{
			son1,
			son2
		}
	})
</script>
```

### 5. 插槽 (slot)

- 显示组件标签中的内容

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>插槽</title>
	</head>
	<body>
		<!--
			使用 slot 可以更好地进行组件复用
			显示组件标签里面的内容,
		-->
		<div id="app">
			<h1>蜀道难</h1>
			<child>
				<p>一夫当关万夫莫开</p>	
			</child>
		</div>
	</body>
</html>
<template id="child">
	<div>
		<slot>如果没有内容,则显示,默认显示</slot>
	</div>
</template>

<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var child = {
		template:'#child'
	}
	var vm1 = new Vue({
		el:"#app",
		data:{},
		methods:{},
		components:{
			child
		}
	});
</script>
```

### 6. 插槽( slot)

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>插槽</title>
	</head>

	<body>
		<div id="app">
			<child>
				<h1 slot="header">蜀道难</h1>
				<p>正文</p>
				<p slot="footer">底部信息</p>
			</child>
		</div>
	</body>

</html>
<template id="child">
	<div>
		<slot name="header"></slot>
		<slot></slot>
		<slot name="footer"></slot>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var child = {
		template:"#child"
	}
	
	var vm1 = new Vue({
		el:"#app",
		data:{},
		methods:{}
	});
</script>
```

### 7. 过渡动画

- 过渡:
- 1.如果一些元素需要结合动画,则使用 transition 标签把相应的元素包裹起来
- 2.还要给动画起一个响亮的名字
- 3.设置动画
- 4.设置动画的标签名 tag="p"
- 动画的使用场景:
- 1.v-if
- 2.v-show
- 3.路由

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>过渡动画</title>
		<style type="text/css">
			/*进入和离开动画*/
			.aa-enter,.aa-leave-to {
				transition: all 1s ease-in-out;
			}
			/*过渡动画*/
			.aa-enter-active,.aa-leave-active{
				background: #f00;
				transition: all 1s ease-in-out;
			}
			/*离开和进入动画*/
			.aa-enter-to,.aa-leave{
				background: #00f;
				opacity: 0;
				transform: translateX(500px);
				transition: all 1s ease-in-out;
			}
		</style>
	</head>
	<body>
		<!--
			过渡:
			1.如果一些元素需要结合动画,则使用 transition 标签把相应的元素包裹起来
			2.还要给动画起一个响亮的名字
			3.设置动画
			4.设置动画的标签名 tag="p"
			
			动画的使用场景:
			1.v-if
			2.v-show
			3.路由
		-->
		<div id="app">
			<child></child>
		</div>
	</body>
</html>
<template id="child">
	<div>
		<button @click="change()">点击切换</button>
		<!-- name 值即为动画 class 的前缀名 -->
		<transition-group name="aa">
			<p v-show="bol" :key=1>两只蝴蝶鸣翠柳</p>
			<p v-show="!bol" :key=2>一只老虎下山来</p>
		</transition-group>
	</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var child = {
		template:"#child",
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
	
	var vm1 = new Vue({
		el:"#app",
		data:{},
		methods:{},
		components:{
			child
		}
	});
</script>
```

### 8. axios(ajax)

#### get请求

- axios.get(url).then(回调函数) 需要绑定 this

#### post请求

- 不能直接传值
- 提交数据需要浏览器进行application/x-www-form-urlencoded 格式化,然后才能提交,
- 在 web 端可以使用 URL.SearchParams() 进行格式化转码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>get</title>
	</head>
	<body>
		<div id="app">
			<button @click="getData()">get获取数据</button>
			<button @click="postData()">post获取数据</button>
			<p>{{txt}}</p>
		</div>
	</body>
</html>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script src="../js/axios.min.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var vm1 = new Vue({
		el:"#app",
		data:{
			txt:''
		},
		methods:{
			getData(){
				// axios get请求, axios.get('要请求的接口').then(function(res){})
				// 在回调函数里面有一个返回数据res,res.datacai 才是要使用数据,拿到 res.data 才能执行方法
				
				axios.get('./get.php?name=curry&age=23').then(function(res){
					// 获取后台发送来的数据
					var data = res.data;
					this.txt = data;
				}.bind(this)).catch(function(err){
					alert(err);
				});
			},
			// post 提交数据需要浏览器进行application/x-www-form-urlencoded 格式化,然后才能提交,
			// 在 web 端可以使用 URL.SearchParams() 进行格式化转码
			postData() {
				// 1.创建提交的对象
				var params = new URLSearchParams();
				// 2.给对象添加数据
				params.append('name','后羿');
				params.append('age',23);
				axios.post('./post.php',params).then(function(res){
					var data = res.data;
					this.txt = data;
				}.bind(this)).catch(function(err){
					alert(err);
				});
			}
		}
	});
</script>
```

```php
// get 请求获取参数
<?php
	header("Content-Type:text/html;charset=utf-8");
	$name = $_GET['name'];
	$age = $_GET['age'];
	echo '你好'.$name.', 你今年'.$age.' 岁了';
?>
```

```php
// post 请求获取参数
<?php
	header("Content-type:text/html;charset=utf-8");
	$name = $_POST['name'];
	$age = $_POST['age'];
	echo '你好'.$name.', 你今年'.$age.'岁了';
?>
```

### 9. 简单路由

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>简单路由</title>
	</head>
	<body>
		<!--
			vue 路由 使用 router-link 组件来执行页面跳转和路由导航,
			通过 router-link 组件的to 属性来设置路由的地址,每一个 router-link 渲染之后会成为 a 标签
			
			每一个路由视图使用 router-view 组件来显示
		-->
		<div id="app">
			<router-link to="/">首页</router-link>
			<router-link to="/libai">李白</router-link>
			<router-link to="/sbq">三百千</router-link>
			
			<!--路由展示窗口-->
			<router-view></router-view>
			<router-view name="body"></router-view>
			<router-view name="footer"></router-view>
			
			
			<!--
				vue 路由当中可以添加多个 router-view 组件给每个组件添加 name 属性,可以在设置路由的时候
				设置在 components 中,以 name 的值作为属性名,要显示的组件为属性值,
				
				router 设置中
				{
					path:'/aaa',
					components:{
						default:没有设置 name 的 view 组件显示的内容
						footer: 要显示的组件
					}
				}
			-->
		</div>
	</body>
</html>
<template id="index">
	<div>我是首页</div>
</template>
<template id="libai">
	<div>我是李白</div>
</template>
<template id="sbq">
	<div>我是三字经,百家姓,千字经</div>
</template>
<script src="../js/vue.js" type="text/javascript" charset="utf-8"></script>
<script src="../js/vue-router.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
	var index = {
		template:"#index"
	}
	var libai = {
		template:"#libai"
	}
	var sbq = {
		template:"#sbq"
	}
	// 设置路由,里面传一个对象,该对象内设置整体路由
	// 对象里面是一个 routes 数组,数组的每一个元素是一个对象
	// path: 是指路由地址,
	// component: 是指 path 地址所展示的组件
	var routerAa = new VueRouter({
		routes:[
			{path:'/',component:index},
			{path:'/libai',components:{
				default:libai,
				body:index,
				footer:sbq
			}},
			{path:'/sbq',component:sbq},
		]
	});
	var vm1 = new Vue({
		el:"#app",
		data:{},
		methods:{},
		router:routerAa
	});
</script>
```

