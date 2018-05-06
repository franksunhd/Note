## React 基础语法

[TOC]

### 0. 什么是 React

- MVVM: (model - view - viewModel)
- model: 指的是数据结构或者数据模型
- view: 是展示数据的视图
- viewModel: 是 model 和 view 的桥梁,使 view 发生变化的同时, model 也跟着变,反之亦然(也可以理解为viewModel的作用是处理 model 和 view 之间的数据逻辑)

### 1.ReactDOM

```javascript
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>React基础语法</title>
		<!-- react.js 是 react 的核心模块 -->
		<script src="js/react.min.js" type="text/javascript" charset="utf-8"></script>
		<!-- react-dom.js 是控制 dom 元素的 js -->
		<script src="js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
		<!-- browser 是 babel 转换器 -->
		<script src="js/browser.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="test"></div>
	</body>
</html>
<script type="text/babel">
	/*
		ReactDom 执行 react 对象的,他有一个 render 方法,该方法拥有两个参数,
		第一个参数是要渲染的dom 结构
		第二个参数是要把 dom 元素渲染到哪里,只能是原生获取

		React 下有 createElement 方法,意为创建元素,有三个参数,
		第一个参数为要创建的元素标签名,
		第二个参数为给元素 添加样式,
		第三个参数为元素的内容
	 */
	ReactDOM.render(<p>画虎画皮难画骨!</p>,document.getElementById("test"));

	var html = React.createElement('h1',null,'报与桃花一处开');
	ReactDOM.render(html,document.getElementById("test"));

	// 创建一个 ul
    var li1 = React.createElement('li',null,"三光者");
    var li2 = React.createElement('li',null,"日月星");
    var li3 = React.createElement('li',null,"三才者");
    var li4 = React.createElement('li',null,"天地人");
	var ul =  React.createElement('ul',null,[li1,li2,li3,li4]);
	ReactDOM.render(ul,document.getElementById("test"));

	// jsx 语法,规定 遇到 {} 在它里面就执行 js 语法,遇到 html 标签就执行 html 语法,也就是把 html 标签里面的内容按照 html 进行解析
	// render 的第一个参数,必须是一个完整的元素,也就是说必须是一个整体元素

	ReactDOM.render(<div>
        <p>1+2={1+2}</p>
		<p>{1 > 2 ? '1>2' :'错误'}</p>
	</div>,document.getElementById("test"));


    ReactDOM.render(React.createElement('h1',null,'他年我若为青帝'),document.getElementById("test"));
</script>
```

### 2.认识babel 转换器

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>认识babel</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
</head>
<body>
    <div id="test"></div>
</body>
</html>
<script type="text/babel">
    /*
        babel JS解释器, 主要负责编辑 ES6 或者 JSX 的内容
        babel 和 JSX 语法并不是新的东西,可以归结为 js 的语法

        type=text/babel 比 type=text/javascript 要优化的多

        Javascript 执行过程: JS --> 从浏览器下载 --> 执行JS

        babel 执行过程: JS --> 浏览器下载 --> babel转换器 --> JS --> 执行JS
     */
</script>
```

### 3.添加外部样式

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>添加外部样式</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
    <style type="text/css">
        .aa {
            background: #00f;
            color: #f0f;
            font-size: 40px;
            font-weight: bold;
        }

        .bb {
            color: #ff0;
        }
    </style>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">
    var arr = [
        <p>唐僧</p>,
        <p>悟空</p>,
        <p>八戒</p>,
        <p>沙僧</p>
    ];

    ReactDOM.render(<div>{arr}</div>,document.getElementById("test"));

    // 外部添加样式,实质上是声明了一个包含样式的对象,然后对象的属性名是样式名,对象的属性值是样式的值,
    // 写在 dom 元素之后,按照 css 的样式解析,其中数值没有单位,单位默认是 px, 如果非要加单位,则用字符串的形式

    var styles = {
        color:'#0f0',
        fontSize: '30px', // 加单位可以为 '30px'
    }

    ReactDOM.render(<div style={styles}>{arr}</div>,document.getElementById("test"));
    // 如果从外部引入 样式对象 style={ 样式对象 } 如果直接写样式 则使用 style = {{行间样式}}
    ReactDOM.render(<div style={{color:'#f00',fontSize:'30px'}}>{arr}</div>,document.getElementById("test"));

    // 为了和原生的做区别,避免 class 冲突,使用 className 的方式引用外部class名
    ReactDOM.render(<p className="aa bb">爱月不梳头</p>,document.getElementById("test"));
</script>
```

### 4.事件

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
</head>
<body>
    <div id="test"></div>
</body>
</html>
<script type="text/babel">
    function aa(str) {
        alert('十步杀一人,千里不留行' + str);
    }

    // 为了和原生的作区分,使用驼峰的方式来执行 click 事件
    ReactDOM.render(<div>
        <button onClick={aa.bind(this,',谁能书阁下')}>点击</button>
    </div>,document.getElementById("test"));

    var arr = ['唐僧', '悟空', '八戒', '沙僧'];
    function show(str) {
        alert(str);
    }
    ReactDOM.render(<ul>{
        arr.map(function (item){
            return <li onClick={show.bind(this,item)} style={{color:'#f00',fontSize:'30px'}}>{item}</li>
        })
    }</ul>,document.getElementById("test"));

</script>
```

### 5.组件

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>组件</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
</head>
<body>
    <div id="test"></div>
</body>
</html>
<script type="text/babel">
    // 组件(类) 是 react 的核心内容,声明组件,首字母必须大写,使用驼峰命名,声明组件的方法是 createClass

    var HtmlDom = React.createClass({
        render:function () {
            return <h1>白发三千丈--{this.props.name}</h1>
        }
    });

    // 使用组件,可以是单标签,也可以是双标签
    ReactDOM.render(<HtmlDom></HtmlDom>,document.getElementById("test"));

    // 属性,可以展示的内容,但是不能够修改
    // 获取属性,只需要在他所在的组件中使用 this.props.要获取的属性名 就可以获取, this.props指的是他所在的组件的属性集合
    ReactDOM.render(<HtmlDom name="李白"></HtmlDom>,document.getElementById("test"));
</script>
```

### 6.组件属性传值

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>组件属性传值</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">
    // 属性传值
    var HtmlDom = React.createClass({
        render:function () {
            return <div>
                <h1>属性传值父组件</h1>
                <SonDom mm={this.props.str}></SonDom>
            </div>
        }
    });

    var SonDom = React.createClass({
        render:function () {
            return <div>
                <h2>四百万人同一哭,{this.props.mm}</h2>
            </div>
        }
    });
    // 渲染组件
    ReactDOM.render(<HtmlDom str="去年今日割台湾"></HtmlDom>,document.getElementById("test"));
</script>
```

```javascript
var arr = [
        <p>人面桃花相映红.</p>,
        <p>人面不知何处去,</p>,
        <p>桃花依旧笑春风.</p>
    ];

    var SetArr = React.createClass({
        render:function () {
            return <h1>
                <p>去年今日此门中,</p>{this.props.arr}
            </h1>
        }
    });

    ReactDOM.render(<SetArr arr={arr}></SetArr>,document.getElementById("test"));
```

### 7.获取双标签中的内容

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>获取双标签的内容</title>
    <script src="./js/react.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/browser.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">

    // 获取双标签中的内容
    var Count = React.createClass({
       render:function () {
           // this.props.children 专门获取标签内部的元素
           return <div>{
               // console.log(this.props.children)

               // this.props.children

               this.props.children.map(function (item) {
                   return item
               })
           }</div>
       } 
    });

    ReactDOM.render(<Count>
        <h1>赵钱孙李</h1>
        <h1>周吴郑王</h1>
        <h1>冯陈楚卫</h1>
        <h1>蒋沈韩杨</h1>
    </Count>,document.getElementById("test"));
</script>
```

### 8.组件默认属性

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>组件默认属性</title>
    <script src="./js/react.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/browser.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">
    var SetProp = React.createClass({
        // 获取默认设置的属性
        getDefaultProps:function () {
            return {
                name:"李白",
                age:18
            }
        },

        // 设置属性的类型
        // 设置 name 为 string 类型且必填
        propTypes:{
            name: React.PropTypes.string.isRequired,
            age: React.PropTypes.number.isRequired
        },
        render:function () {
            return <p>花间一壶酒--{this.props.name}--{this.props.age}</p>
        }
    });

    ReactDOM.render(<SetProp name="杜甫" age="120"></SetProp>,document.getElementById("test"));
</script>
```

### 9.Refs 

- refs 是特殊的属性,它是所有附带有 ref 属性的集合,通过 this.refs.a 可以获取到 ref 的值为 a 的元素

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>组件refs</title>
    <script src="./js/react.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/browser.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">
    // refs 是特殊的属性,它是所有附带有 ref 属性的集合,通过 this.refs.a 可以获取到 ref 的值为 a 的元素
    
    var RefsClass = React.createClass({
        changeColor: function() {
            this.refs.a.style.color = '#0f0';
        },
        render:function () {
           return <div>
               <p ref="a">退一步海阔天空</p>
               <button onClick={this.changeColor}>点击</button>
           </div>
       }
    });

    ReactDOM.render(<RefsClass></RefsClass>,document.getElementById("test"));
</script>
```

### 10.状态

```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>组件--状态</title>
    <script src="./js/react.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/browser.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
<div id="test"></div>
</body>
</html>
<script type="text/babel">
    // state 状态 实质上也是属性,但是他和 props 的区别为
    // state 可以改变值, props 不可以改变值

    var StateDoc = React.createClass({
        // 设置状态的默认值
        getInitialState:function () {
          return {
              ok:true
          }
        },
        
        render:function () {
            // 获取某个状态的值 this.state.状态名
            return <div>
                <p>{this.state.ok?'天若有情天亦老':'人间正道是沧桑'}</p>
                <button onClick={this.changeState}>点击</button>
            </div>
        },
        // 自定义改变状态的值,使用 this.setState({})
        changeState:function () {
            this.setState({
                ok:!this.state.ok
            })
        }
    });

    ReactDOM.render(<StateDoc></StateDoc>,document.getElementById("test"));
</script>
```

### 11. 生命周期

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="./js/react.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/react-dom.min.js" type="text/javascript" charset="utf-8"></script>
    <script src="./js/browser.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
<!--
    组件的生命周期:
    1.初始化
        1.getDefaultProps:设置默认属性
        2.getInitialState:设置初始的状态
        3.componentWillMount:组件即将被装载
        4.render 渲染
        5.componentDidMount:组件已经被装载，只会在第一个组件的时候触发
    2.运行中
        1.componentWillReceiveProps:在组件将要接收到属性的时候，接收属性前
        2.shouldComponentUpdate:在接收到新的props或者state，将要渲染之前调用
        3.componentWillUpdate:render触发之前，更新
        4.render 渲染
        5.componentDidUpdate:在渲染完成之后触发
    3.销毁
        1.componentWillUnmount:在组件从dom中移除的时候立刻被调用
-->
<div id="test"></div>
</body>
</html>

<script type="text/babel">
    var LifeDom = React.createClass({
        componentDidMount: function () {
          console.log('5');
        },
        componentWillMount:function () {
            console.log('3');
        },
        render: function () {
            return <h1>南村群童欺我老无力</h1>
        }

    });

    ReactDOM.render(<LifeDom></LifeDom>,document.getElementById("test"));
</script>
// 先打印 3 后打印 5
```

### 12.容器变透明

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>输入实时显示--双向绑定</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }

        h1 {
            width: 200px;
            height: 200px;
            background-color: blue;
            color: #fff;
            font-size: 30px;
            margin: 20px auto 0px;
        }
    </style>
</head>
<body>
    <div id="test"></div>
</body>
</html>
<script type="text/babel">
    var LifeDom = React.createClass({
        getInitialState:function () {
          return {
              opacity:1 // 设置默认的透明度
          }
        },
        componentDidMount: function () {
            console.log('5');
        },
        componentWillMount:function () {
            console.log('3');
            // 计时器是一个闭包,它里面的 this 指的是 window, 而咱们希望 this 指向当前的组件,所以在计时器函数里面添加
            // bind(this) 这样就等于把当前的 this 指向到 计时器里面的函数
            this.timer = setInterval(function () {
                // 获取状态的值
                var opc = this.state.opacity;
                opc -= 0.05;
                if(opc <= 0.1) {
                    opc = 1;
                }

                this.setState({
                    opacity: opc
                })
            }.bind(this),100);
        },
        render: function () {
            return <h1 style={{opacity:this.state.opacity}}>南村群童欺我老无力</h1>
        }

    });

    ReactDOM.render(<LifeDom></LifeDom>,document.getElementById("test"));
</script>
```

### 13.实时输入显示,数据双向绑定

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>输入实时显示--双向绑定</title>
    <script src="js/react.min.js"></script>
    <script src="js/react-dom.min.js"></script>
    <script src="js/browser.min.js"></script>
</head>
<body>
    <div id="test"></div>
</body>
</html>
<script type="text/babel">
    var StateInput = React.createClass({
        // 设置默认状态
        getInitialState:function () {
            return {
                val:'才饮长江水'
            }
        },
        render:function () {
            return <div>
                <input type="text" value={this.state.val} onChange={this.changeVal}/>
                <p>{this.state.val}</p>
            </div>
        },
        changeVal: function (event) {
            this.setState({
               val: event.target.value
            });
        }
    });
    ReactDOM.render(<StateInput></StateInput>,document.getElementById("test"));
</script>
```



