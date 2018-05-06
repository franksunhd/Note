## Angualr1 基础

[TOC]

### ng-app

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>angular1版本</title>
	</head>
	<body ng-app="" ng-init="aa = 10;data = ['关羽','张飞','刘备']">
		<!-- 
			1.ng-app 是什么?
				ng-app: 定义了 AnjularJs 的使用范围
				ng-app: 是一个特殊的指令,一个 html 文档只允许写入一次,写入多次只有第一次有效
				ng-app可以出现在html文档的任何一个元素上.
			2.ng-app作用：告诉子元素指令是属于angularJs。
		-->
		<input type="text" name="" value="" ng-model="aa"/>
		<div>{{aa}}</div>
		<p ng-bind="aa"></p>
		
		<ul>
			<li ng-repeat="item in data">{{$index + 1 + item}}:{{item}}</li>
		</ul>
		
		<!--
			指令: ng开头
			ng-init:初始化数据
			ng-bind:把数据绑定在他所在的元素上,
			ng 指令 实质上是一个 js 域,在 ng 指令里面可以写 js 语句
			ng-show: 值为 true, 显示他所在的元素,否则隐藏
			ng-hide: 值为 true, 隐藏他所在的元素,否则显示
		-->
		
		<div ng-show="1===1">好雨知时节</div>
		<div ng-show="1===0">一去二三里</div>
		<div ng-hide="1===1">黄鹂鸣翠柳</div>
		<div ng-hide="1===0">当春乃发生</div>
	</body>
</html>
<!-- 引入 JS  -->
<script src="angular.min.js" type="text/javascript" charset="utf-8"></script>
```

