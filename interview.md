## 总结

[TOC]

### 1.post和get的区别

1. 在客户端，Get方式在通过URL提交数据，数据在URL中可以看到；POST方式，数据放在HTTP包的body中。
2. GET方式提交的数据大小有限制（因为浏览器对URL的长度有限制），而POST则没有此限制。
3. 安全性问题。正如在（1）中提到，使用 Get 的时候，参数会显示在地址栏上，而 Post 不会。所以，如果这些数据是中文数据而且是非敏感数据，那么使用 get；如果用户输入的数据不是中文字符而且包含敏感数据，那么还是使用 post为好。
4. 服务器取值方式不一样。GET方式取值，如php可以使用\$\_GET来取得变量的值，而POST方式通过\$\_POST来获取变量的值。

### 2.HTTP协议(工作于客户端－服务器的应用层协议，包含头部，主体，状态码。。。)

### 3.HTML页面中DOCTYPE的作用(应该回答用来声明文档类型，写不写有什么影响，(写上按照标准，不写按照浏览器的默认标准，结果不得而知))

### 4.语义化

### 5.css的作用，选择器，三大特性(继承，层叠，优先级)，优先级(!important>style>id>class>标签>继承>默认)

### 6.盒子模型(两种)

### 7.嵌套上外边距合并问题

### 8.浮动的特点，影响，及清除(4)

### 9.定位

### 10.两栏布局和三栏布局 

### 11.Ajax定义，特点，优缺点等

### 12.盒子内元素垂直居中问题

```html
<style type="text/css">
		#box{
			border: 5px solid red;
			height: 150px;
			text-align: center;

			/* vertical-align: middle; */

			/*div->table
			ie67无效
			*/
			display: table;
			width: 100%;
		}
		#box span{
			vertical-align: middle;
			/*span->td*/
			display: table-cell;
		}


		*{padding: 0;margin: 0}
		#tb{
			border-collapse: collapse;
		}

		#tb img{
			width: 150px;
			vertical-align: middle;

		}
		/*
		vertical-align：用到子元素td上，在table中有效
		*/
		#tb td:last-child{
			/* vertical-align: middle; */
		}

		#box2{
			border: 5px solid blue;

			/*height: 300px;*/
		}
		/*图片作为参照！高度和父元素一样高！！！*/
		#box2 img{
			width: 150px;

			/*其他内联元素作为参照*/
			vertical-align: middle;
		}
		#box2 span{
			vertical-align: middle;
		}

		.baseline{
			display: inline-block;
			width: 0px;
			height: 100%;
			background: red;

			vertical-align: middle;
		}

		#box3{
			border: 5px solid green;
			height: 200px;
		}
		#box3 img{
			width: 100px;
			vertical-align: middle;
		}
		#box3 a{
			vertical-align: middle;
		}
		#box3 span{
			vertical-align: middle;
		}

		/*高度必须和父元素相等，作为其他元素垂直布局的参考线*/
		.bsLine:before{
			content: "";
			visibility: hidden;

			display: inline-block;
			width: 0px;
			height: 100%;
			background: red;
			vertical-align: middle;
		}

	</style>
</head>
<body>
	<div id="box">
		<span>内联span</span>
	</div>

	<div>
		<table id="tb" border="1">
			<tr>
				<td>
					<img src="img/pic.jpg">
				</td>
				<td>
					<div>
						<h3>title</h3>
						<p>内容</p>
					</div>
				</td>
			</tr>
		</table>
	</div>


	<hr>
	<div id="box2">
		<img src="img/pic.jpg">

		<span>span</span>
		-------
	</div>

	<!-- <span class="baseline"></span> -->

	<div id="box3" class="bsLine">
		<img src="img/pic.jpg">

		<span>span</span>
		-------
		<a href="###">链接</a>
	</div>
```

