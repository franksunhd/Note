## Angular5 基础

[TOC]

### 1.安装

```html
<!--
	使用软件 webstrom
	Angular5的安装:
    1. node和 npm需要安装到最新 node:9.9.0 npm:5.8.0
    2. 可以安装淘宝镜像:  
	sudo npm install cnpm -g --registry=https://registry.npm.taobao.org
    	cnpm -v 查询版本
    3. 安装 angular5版本: sudo npm install -g @angular/cli
        ng -v 查询版本
    4. 创建一个项目: ng new pro-name(你的项目名字)
    5. 进入你的项目: cd pro-name(你的项目名字)
    6. 启动项目 ng serve –open
-->

<!--
	野路子启动服务:
	1.在项目文件夹下创建一个 proxy.config.json 文件
	2.文件写入内容:
	"/api": {
    	"target": "http://127.0.0.1:8080"
  	}
	3.修改 package.json 文件中的 start 为下面代码
	"start": "ng serve --proxy-config proxy.config.json",
	4.重新启动服务命令使用: npm start
-->
```

### 2. 启动过程

```html
<!--
angular 的启动过程:
1. angular 会通过命令行找到主页,就是 index.html, 并且进入到主程序接口(main.ts)
2. 在 main.ts 中,指定了 angular 运行的根模块(AppModule)
3. 在 AppModule中,通过 bootstrapModules 设置该模块的主组件为 appComponent
4. 该主组件定义了主选择器 app-root ,它的引用方式就是 <app-root></app-root> 引用到 index.html
5. 在 index.html 上引用 app-root, 就会把该组件模板上的内容渲染到 index.html
(app-root的模板实质上就是 app.component.html的内容)
  -->
```

### 3. 什么是 MVVM

- MVVM: (model - view - viewModel)
- model: 指的是数据结构或者数据模型
- view: 是展示数据的视图
- viewModel: 是 model 和 view 的桥梁,使 view 发生变化的同时, model 也跟着变,反之亦然(也可以理解为viewModel的作用是处理 model 和 view 之间的数据逻辑)
- 实现了 高内聚,低耦合

```html
<!--
	注意:具有 MVVM 的只有 angular 和 vue
	React 只有 v 即视图,没有 m 和 vm
	React 与Angularjs，Emberjs,vue 等大而全的框架不同，React专注的中心是Component，即组件
	React认为一切页面元 素都可以抽象成组件，比如一个表单，或者表单中的某一项。
-->
```

### 4. 什么是 高内聚,低耦合

[文章链接](./njoh.md)

### 5. app.module.ts

```typescript
// 引入模块
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

// 每个组件都必须声明在(且只能声明在)一个 NgModule 中
import { AppComponent } from './app.component';

// 引入服务
import { HeroService } from './hero.service';

// 引入指令
import { MyDirDirective } from './my-dir.directive';

// 自定义的管道
import { MyPipePipe } from './my-pipe.pipe';
// @NgModule
@NgModule({
  declarations: [],  // 引入组件,(单个页面)
  imports: [],  // 引入模块
  providers: [],  // 引入服务
  bootstrap: [AppComponent]  // 引入依赖
})
export class AppModule { }
```

### 6.组件装饰器

- 组件装饰器,所有的装饰器语法都是 @装饰器名字

### 7. bind

```typescript
// bind 组件
import { Component, OnInit } from '@angular/core';
// 组件装饰器,所有的装饰器语法都是 @装饰器名字

@Component({
  selector: 'app-bind',
  templateUrl: './bind.component.html',
  styleUrls: ['./bind.component.css']
})


export class BindComponent implements OnInit {
  liubei = '玄德';
  bool = true;
  baidu = 'http://www.baidu.com';
  img = 'assets/img1.png';

  modelValue = '双向绑定';
  colorSize = 'red';
  colSize = 2;
  className = 'color-case';
  className1 = 'color-case1';
  bol = true;

  // 声明一个string类型的变量,ts 是强类型的语言,声明的时候要声明类型
  dong: string;
  arr: Array<string>;  // 声明一个数组,并且要给数组内的元素添加类型
  aa: any;  // 不缺定的类型
  arr1: [1, 2, 3, 4];

  arrObj = [
    {name: '悟空', age: 18},
    {name: '八戒', age: 17},
    {name: '沙僧', age: 16},
    {name: '唐僧', age: 20}
   ];

  witch = '英雄联盟';

  // 加载的时候执行
  constructor() {
    this.dong = '日出东方';
    console.log(this.dong + 'constructor');
  }

  // 加载完毕后者执行渲染完毕的时候执行
  ngOnInit() {
    console.log(this.dong + 'ngOnInit');
  }

  msgClick(ev) {
    ev.target.style.backgroundColor = 'red';
  }

  clickAa(name) {
    name.style.backgroundColor = 'green';
  }

  changeValue() {
    this.dong = 'l1';
  }
}
```

```html
<!--bind 页面-->
<h1>------------bind页面---------------</h1>
<!--
  angular 绑定数据
  1.插值表达式 {{}} 可以放置变量,js 表达式,不能放 js 语句
  2.使用[] 将 html 标签中的属性绑定在元素上
  3.() 绑定事件
-->
<p> 刘备字{{liubei}}</p>
<p>5 + 6 = {{ 5 + 6}}</p>
<p>{{bool ? '京中有善口技者':'从此君王不早朝'}}</p>

<!--
  属性绑定:
  1.dom 属性的绑定,和 插值表达式是完全一样的
  2.html 属性绑定
-->

<a href="{{baidu}}">百度</a>
<a [href]="baidu">百度</a>
<div><img src="{{img}}" alt=""></div>
<div><img [src]="img" alt=""></div>

<!--
  事件绑定:
  (事件名) = "方法名"
-->

<!-- 通过 $event.target 可以获取当前操作的元素 -->
<div class="msg" (click)="msgClick($event)">(click)="msgClick($event)"</div>
<br><br>
<!-- 给元素起别名 #+名字  angular1 中没有别名-->
<div #aa class="msg" (click)="clickAa(aa)">(click)="clickAa(aa)"</div>
<br>
<!--
  html 的属性绑定 和 DOM 的属性绑定不同
  1.html 的属性绑定是指初始值,
  2.dom 的属性绑定 是指当前值

  建议使用 dom 属性绑定,也就是{{}}
-->

<!--
  angular5 的绑定是单向的,如果想双向绑定,必须导入 FormsModel模块
-->
<br>
<input type="text" (input)="changeValue()" value="{{dong}}">


<!--
  双向绑定: 语法 ngModel是一个指令,[(ngModel)]
-->

<input type="text" [(ngModel)]="modelValue" value="">
<p>{{modelValue}}</p>


<!--
  html属性绑定
  1. 基本的 html 属性绑定
  [arr.属性名]
  2. css类 绑定
  [class]="表达式"
  [class.样式名] = bool值
  [ngClass] = 对象

  ngClass angular 内置的属性指令

  3. 样式绑定
  [style.css样式名] = "值"
  [ngStyle] = 对象;

  ng指令的值都是从 ts 上的组件里面来的
-->

<div class="color-case" [attr.bgcolor] = "colorSize"></div>

<table border="1">
  <tr>
    <td [attr.colspan] = "colSize">刘备</td>
    <td>水兵月</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
  </tr>
</table>

<!-- css类 -->
<div [class]="false?className:className1">[class]=""</div>
<br>

<!-- 点击控制显示和隐藏 -->
<button (click)="bol=!bol">点击显示/隐藏</button><br>
<div class="color-case2" [class.dis]="bol"></div>
<br>
<div class="color-case2" ngClass="color-case3">ngClass</div>
<br>
<br>
<!-- 样式 -->
<div class="color-case2" [style.background]="'#f00'">[style.background]</div>
<br>
<br>
<div class="color-case2" [ngStyle]="{'background':'#333'}" appChangeColor></div>
<br>
<br>

<!--
  指令:分为三种
  1.特殊指令(组件,组件其实就是带有模板的指令)
  2.属性型指令:该指令侧重修改元素的内容样式.比如外观 css
  3.结构型指令:对 dom 进行操作的指令( *ngIf , *ngFor , *ngSwitch),对 dom 进行增加删除和移动
-->

<!--
  ng-template 该指令用于渲染它内部的元素到都没结构上 类似小程序的 block
-->

<ng-template>
  <p>曾经沧海难为水</p>
</ng-template>



<!--
  * 用来简化复杂语法的语法糖, 它把 *ngIf 转换为 <ng-if></ng-if>
-->

<div *ngIf="bol">
  <p>曾经沧海难为水</p>
</div>

<div *ngIf="!bol">
  <p>各家自扫门前雪</p>
</div>

<!--
  1. *ngIf:控制 结构 是否动态增删 不是控制dom 的显隐性,而是控制所修饰的结构是否正在 dom 文档中

  2. *ngFor: 循环添加列表
-->

<ul>
  <li *ngFor="let item of arrObj">{{item.name}}</li>
</ul>


<div *ngFor="let item of arrObj;let i = index">
  <span> 第{{ i+1}} 个英雄</span>
  <span>{{item.name}}</span>
  <span>{{item.age}}</span>
</div>

<div [ngSwitch]="witch">
  <h1 *ngSwitchCase="'王者荣耀'">王者荣耀</h1>
  <h1 *ngSwitchCase="'英雄联盟'">英雄联盟</h1>
  <h1 *ngSwitchCase="'绝地求生'">绝地求生</h1>
  <h1 *ngSwitchCase="'荒野行动'">荒野行动</h1>
</div>

<!-- 使用创建的结构指令 -->
<div *appMyDir="false">顶顶顶顶</div>
<div *appMyDir="true">顶顶顶顶</div>
<br><br>

<!-- 使用创建的属性指令 -->

<div class="color-case2" appChangeColor="害怕">appChangeColor</div>
<br><br>

<div class="color-case2" appChangeColor="无奈"></div>
<br><br>
```

### 8. http

```typescript
// ts页面
import {Component, OnInit} from '@angular/core';
import {HttpClient} from '@angular/common/http';

@Component({
  selector: 'app-http',
  templateUrl: './http.component.html',
  styleUrls: ['./http.component.css']
})
export class HttpComponent implements OnInit {

  // 声明两个接收对象
  obj1 = {};
  obj2 = {};

  constructor(public http: HttpClient) {
  }

  ngOnInit() {
  }



  // 设置 get 提交方法
  getFun() {
    this.http.get('/api/get').subscribe(data => {
      this.obj1 = data;
    });
  }

  // 设置 post 提交方法
  getPost() {
    this.http.post('/api/post', {
      'name': '超级赛亚人',
      'age': 123
    }).subscribe(data => {
      console.log(data);
      this.obj2 = data;
    });
  }
}
```

```html
<!--html页面-->
<button (click)="getFun()">点击GET获取数据</button>
<p>{{obj1.name}}{{obj1.age}}</p>
<button (click)="getPost()">点击POST获取数据</button>
<p>{{obj2.name}}{{obj2.age}}</p>
```

### 9. pipe 管道

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-pipe',
  templateUrl: './pipe.component.html',
  styleUrls: ['./pipe.component.css']
})
export class PipeComponent implements OnInit {

  objDate = new Date();
  val1 = '123';
  val2 = '';

  constructor() { }
  ngOnInit() {}
}
```

```html
<!--html-->
<!--
  管道:(过滤器)
  管道的修饰符 是 |
  要过滤的内容(也可以是变量) | 过滤的规则
  过滤规则可以是链式写法, 如: 要过滤的内容(也可以是变量) | 过滤规则1 | 规则2 | 规则3;
  内置的过滤器(管道)
  自定义的过滤器(管道)
-->
<!--
  内置的过滤器:
-->

<!-- 1.大小写过滤 -->
<h2>{{ 'uppercase' | uppercase}}</h2>
<h2>{{'LOWERCASE' | lowercase}}</h2>

<!--
  2.date 指定日期格式,可以传参,大写 H代表24小时, h代表12小时
 -->
<h2>The hero's birthday is {{ objDate | date }} </h2>
<h2>The hero's birthday is {{ objDate | date:"yyyy年MM月dd日 HH:mm:ss" }} </h2>

<!--
  3.number 整数最少位数,小数的最少位数,设置小数的最多位数
-->

<h2>{{10000 | number}}</h2>
<!-- 小数点之前表示获取几位,不够的自动用0补全,小数点之后表示范围 -->
<h2>一筐萝卜:{{3.1415926 | number:"3.2-3"}}</h2>


<!--
  4.货币类型,也可以传参
-->

<h2>一筐萝卜:{{ 1200 | currency:'#'}}</h2>

<!--
  5.自定义的管道
-->

<!--<h2>{{'上课不认真,' | myPipe }}</h2>-->
<!--<h2>{{'上课不认真,' | myPipe:'还是' }}</h2>-->

<input type="text" [(ngModel)]="val1">
<p>{{val1 | myPipe}}</p>

<input type="text" [(ngModel)]="val2">
<p>{{val2 | myPipe}}</p>
```

#### 自定义管道

```typescript
// ts
import { Pipe, PipeTransform } from '@angular/core';
// PipeTransform 使用它的 transform 方法,这个方法接收两个参数
// 第一个参数是获取输入的值,第二个参数是可选参数,经过操作返回最终值

@Pipe({
  name: 'myPipe'
})
export class MyPipePipe implements PipeTransform {
  // ?: 表示参数可选,与三目运算符无关

  // value: 指的是 | 前边的数据(也就是要过滤的数据)
  // args 指的是传入的参数, 类似于内置过滤器 : 后面的内容(比如:$,#.....)
  // {{ 123456789 | number:'2.2'}} 此例中 value代表:123...部分  args代表:2.2部分
  arrObj = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];
  str = '';
  i = 0;
  transform(value: any, args?: any): any {
    /*
    // 判断输入的文本
    if (!args) {
      args = '不如';
    }
    return value + args + '  回家卖红薯';
    */

    // 数字转换为汉字
    this.str = '';
    for (this.i = 0; this.i < value.length; this.i++) {
      if (value[this.i] >= 0 || value[this.i] < 10) {
        this.str += this.arrObj[value[this.i]];
      }
    }
    return this.str;
  }
}
```

### 10 server 服务

- 创建服务: ng g s 服务名

```typescript
// book.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable()
export class BookService {

  constructor(public http: HttpClient) { }

  getData() {
    return this.http.get<any[]>('../../../server/server1.js');
  }
}
```

```typescript
// http-service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

// 使用 http 获取数据,首先在 appModule中 引入 HttpClientModule, 然后在组件中引入 HttpClient 模块

@Injectable()
export class HttpServeService {

  // 需要在 这里声明 http
  constructor(public http: HttpClient) { }
  getData() {
    return this.http.get<any[]>('../assets/data.json');
   }
}
```

```typescript
// my-serv2.service.ts
import { Injectable } from '@angular/core';
import { DATA } from '../myData';
import { Observable } from 'rxjs/Observable';
import { of } from 'rxjs/observable/of';

// Observable 视图对象 rxjs 中引入了Observable(可观察对象推送数据)
// Observable 是多数据的生产者 ,向数据的消费者(Observer) 发送数据
// Observable 类似一个不需要传参的函数,他可以返回对个值,也就是说他可以有多个 return, 他可以异步产生数据

/*
  subscribeOn,它是 Observable 最重要的方法,她会获取所有的 Observable 发布的数据
 */
@Injectable()
export class MyServ2Service {
  constructor() { }
  // 异步发送数据
  setData(): Observable<any> {
    return of(DATA);
  }
}
```

### 11. sev-com

```typescript
// ts
import { Component, OnInit } from '@angular/core';
import { MyServService } from '../service/my-serv.service';
import { MyServ2Service } from '../service/my-serv2.service';
import { HttpServeService } from '../service/http-serve.service';


@Component({
  selector: 'app-sev-com',
  templateUrl: './sev-com.component.html',
  styleUrls: ['./sev-com.component.css']
})
export class SevComComponent implements OnInit {

  // 在这里声明服务,可以理解为 myServe 获取 MyServService 中的方法
  constructor(public myServe: MyServService, public myServe2: MyServ2Service, public httpServe: HttpServeService) { }
  arr = [];
  arr2 = [];
  arr3 = [];
  ngOnInit() {
    this.arr = this.getData();

    // 执行异步方法
    this.getData2();
    this.getData3();
  }

  // 设置 getData方法获取数据
  getData() {
    return this.myServe.setData();
  }

  // 设置 异步获取数据
  getData2() {
    // this.myServe2.setData() 返回的是一个发布者的方法,使用订阅方法获取发布的数据
    return this.myServe2.setData().subscribe(info => {
      this.arr2 = info;
    });
  }

  // 设置 通过 http get 方法获取的数据
  getData3() {
    return this.httpServe.getData().subscribe(info => {
      this.arr3 = info;
    });
  }
}
```

```html
<!--html-->
<h2>------------- sev-com ---------------</h2>
<!--
  组件一般值负责视图展示,不负责过多的逻辑运算和数据操作,因此angular引入了服务的概念服务一般只负责数据操作,
  实质上服务就是操作数据的函数,在组件中引用即可,在 angular 项目中把数据操作委托给某个服务

  一般创建服务的方法 ng g s 服务名

  注意:要把创建好的服务引到 app.module.ts 中,要把服务模块放到app.module.ts中的 providers中

  在哪一个组建中使用服务,就要先导入该服务

  一般的 服务不会直接引入死数据,都是从后台获取数据
-->
<h2>--------1--------</h2>
<table>
  <thead>
    <tr><td>序号</td><td>姓名</td><td>账户名</td><td>邮箱</td><td>电话</td><td>网址</td><td>城市</td><td>街道</td><td>邮政编码</td></tr>
  </thead>
  <tbody>
    <tr *ngFor="let item of arr">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.username}}</td>
      <td>{{item.email}}</td>
      <td>{{item.phone}}</td>
      <td>{{item.website}}</td>
      <td>{{item.address.city}}</td>
      <td>{{item.address.street}}</td>
      <td>{{item.address.zipcode}}</td>
    </tr>
  </tbody>
</table>
<h2>--------2--------</h2>
<table>
  <thead>
  <tr><td>序号</td><td>姓名</td><td>账户名</td><td>邮箱</td><td>电话</td><td>网址</td><td>城市</td><td>街道</td><td>邮政编码</td></tr>
  </thead>
  <tbody>
  <tr *ngFor="let item of arr2">
    <td>{{item.id}}</td>
    <td>{{item.name}}</td>
    <td>{{item.username}}</td>
    <td>{{item.email}}</td>
    <td>{{item.phone}}</td>
    <td>{{item.website}}</td>
    <td>{{item.address.city}}</td>
    <td>{{item.address.street}}</td>
    <td>{{item.address.zipcode}}</td>
  </tr>
  </tbody>
</table>
<h2>--------3--------</h2>
<table>
  <thead>
  <tr><td>序号</td><td>姓名</td><td>账户名</td><td>邮箱</td><td>电话</td><td>网址</td><td>城市</td><td>街道</td><td>邮政编码</td></tr>
  </thead>
  <tbody>
  <tr *ngFor="let item of arr3">
    <td>{{item.id}}</td>
    <td>{{item.name}}</td>
    <td>{{item.username}}</td>
    <td>{{item.email}}</td>
    <td>{{item.phone}}</td>
    <td>{{item.website}}</td>
    <td>{{item.address.city}}</td>
    <td>{{item.address.street}}</td>
    <td>{{item.address.zipcode}}</td>
  </tr>
  </tbody>
</table>
```

### 12. user

```typescript
// ts
import {Component, OnInit} from '@angular/core';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  // 判断是 新建 还是 编辑
  flag = 0;  // 0 为新建,1为提交
  // 设置姓名和年龄的初始值
  myName = '';
  myAge: number;

  // 设置当前修改的 index 值
  myIndex: number;
  obj = null;
  data = [
    {'name': '唐僧', age: 123},
    {'name': '悟空', age: 122},
    {'name': '八戒', age: 121},
    {'name': '沙僧', age: 120},
  ];

  constructor() {
  }

  ngOnInit() {
  }

  // 点击编辑的方法
  editData(index) {
    this.flag = 1;
    this.myName = this.data[index].name;
    this.myAge = this.data[index].age;
    this.myIndex = index;
  }

  // 删除方法
  delData(index) {
    this.data.splice(index, 1);
  }

  // 点击新建
  createData() {
    this.flag = 0;
    this.myName = '';
    this.myAge = null;
    this.myIndex = null;
  }

  // 设置提交方法
  /*
  submitData() {
    if (this.myName === '') {
      alert('请填写完整的用户名');
    }
    if (this.myAge <= '0' || !this.myAge) {
      alert('请填写正确的年龄');
    }
    // 首先判断当前操作是编辑还是新建
    if (this.flag === 0) {  // 新建
      if (this.myName != '' && this.myAge != '') {
        this.obj = {name: this.myName, age: this.myAge};
        this.data.push(this.obj);
        this.myName = '';
        this.myAge = null;
      }
    } else {  // 编辑
      this.data[this.myIndex].name = this.myName;
      this.data[this.myIndex].age = this.myAge;
      this.myName = '';
      this.myAge = null;
      this.myIndex = null;
    }
  }
  */
}
```

```html
<!--html-->
<h2>-----------user页面------------</h2>
<h2>用户列表</h2>
<dl>
  <dt>
    <span>名字</span>
    <span>年龄</span>
    <span>操作</span>
  </dt>
  <dd *ngFor="let item of data,let i = index">
    <span>{{item.name}}</span>
    <span>{{item.age}}</span>
    <div>
      <em (click)="editData(i)">编辑</em>
      <em (click)="delData(i)">删除</em>
    </div>
  </dd>
</dl>


<h2 *ngIf="flag == 0">新建</h2>
<h2 *ngIf="flag == 1">编辑</h2>

<ul>
  <li>
    <!-- angular 里面所有的输入框都需要加 ngModule -->
    <label for="user">姓名:</label>
    <input id="user" type="text" [(ngModel)]="myName">
  </li>
  <li>
    <label for="age">年龄:</label>
    <input id="age" type="text" [(ngModel)]="myAge">
  </li>
</ul>
<button (click)="createData()">重置</button>
<button (click)="submitData()">提交</button>
```

### 13. 指令

```typescript
// ts 
// 创建指令 ng genetate directive myDir

import { Directive, TemplateRef, ViewContainerRef, Input } from '@angular/core';
// TemplateRef: 他可以获取指令所在标签的内容
// ViewContainerRef: 他可以访问视图的内容
// Input:接收 dom 传过来的信息
// appUnless属性: 接收一个 bool 条件.把 bool 绑定在[appUnless],她需要一个 input 接收数据
@Directive({
  selector: '[appMyDir]'
})

export class MyDirDirective {
  // 接收前台的数据
  @Input('appMyDir') set unless (bool:boolean) {
    if (bool) {
      // 说明属性赋值为 true 把视图清空
      this.viewContainerRef.clear();
      console.log('视图隐藏');
    } else {
      // 创建视图,并且把视图的内容放进创建的视图中
      this.viewContainerRef.createEmbeddedView(this.templateRef);
      console.log('视图显示');
    }
  }
  // 依赖注入
  constructor(private templateRef: TemplateRef<any>, private viewContainerRef: ViewContainerRef) {
  }
}
```

### nodeJS 处理前端数据 post 请求

```javascript
var express  = require("express");
var app = new express();

// 获取 post 请求提交的参数,要使用 body-parser
var bodyParser = require("body-parser");

// 设置获取 post 提交数据的 中间件
app.use(bodyParser.urlencoded({extended:false}));
app.use(bodyParser.json());

// 处理 get 请求
app.get('/api/get',function (req,res) {
  console.log(req.query);
  // 向前台发送json
  res.json({
    "name":"悟空",
    "age":123
  });
});

// 处理 post 请求
app.post('/api/post',function (req,res) {
  console.log(req.body);
  // 传给前台的json数据
  res.json({
    "name":"八戒",
    "age":456
  });
});

app.listen(8080);
console.log("服务启动成功!");
```

### 14. 路由

创建路由: ng generate module app-routing --flat --module=app

- --flat 把这个文件放进了 src/app 中，而不是单独的目录中。
- --module=app 告诉 CLI 把它注册到 AppModule 的 imports 数组中。

```html
<!--
  angular中的路由:
  1.routes:所有的路由信息都在 routes 配置
  2.router-outlet 展示路由页面的窗口,只要有路由的切换,都会在该组件中显示
  3.router: 导航对象,通过对 router 的调用实现对路由的切换
  4.routerLink 和 a 标签类似,通过他可以跳转路由路径
  5.ActivatedRoute 通过该模块,可以获取路由传的数据信息
 -->
<!--子路由是指组件当中还有一个 router-outlet 组件-->
```

#### 路由配置 app-routing.module.ts

```typescript
import {NgModule} from '@angular/core';
import {CommonModule} from '@angular/common';
import {RouterModule, Routes} from '@angular/router';

import {HomeComponent} from './home/home.component';
import {IndexComponent} from './index/index.component';
import {C404Component} from './c404/c404.component';
import {PruductComponent} from './pruduct/pruduct.component';
import {CdataComponent} from './cdata/cdata.component';
import {FuComponent} from './fu/fu.component';
import {Son1Component} from './son1/son1.component';
import {Son2Component} from './son2/son2.component';
import {YaseComponent} from './yase/yase.component';

import {FuzhiComponent} from './fuzhi/fuzhi.component';
import {UserComponent} from './user/user.component';
import {NewComponent} from './new/new.component';

// 1. 路由是自上而下查找
// 2. 路由配置的时候,不需要加 '/'
// 3. ** 指的是找不到路由的情况

/*
  路由配置在对象中,以 json 的形式配置

  path: 代表访问的路径
  component: 代表如果访问了设置的路径,在视图中显示组件
*/


const routes: Routes = [
  {path: '', component: IndexComponent},

  // 1.设置传值, data 设置传的信息
  {path: 'home', component: HomeComponent, data: [{str: '清明时节雨纷纷'}]},
  // 2.路径传值 在 path 上添加要传送的信息
  {path: 'pruduct/:name/:id', component: PruductComponent},
  // 3. 把要传的参数放到 a 标签上
  {path: 'cdata', component: CdataComponent},

  {path: 'home', component: HomeComponent},

  // 设置子路由 ,使用 children 引入子路由
  {
    path: 'fu', component: FuComponent, children: [
      {path: 'son1', component: Son1Component},
      {path: 'son2', component: Son2Component}
    ]
  },

  // 引入辅助路由 他在 name=libai的router-outlet里面显示
  {path: 'yase', component: YaseComponent, outlet: 'libai'},

  // 路由重定向,redirectTo设置需要访问的路由,pathMatch代表路由的匹配度, full 代表精确匹配, prefix 代表如果有路由前缀就能匹配
  // full: 如果 path为 ho 定向为 home, 则只有 ho 能跳到 home,
  // prefix: 如果 path为 ho 定向为 home,则除了 'ho/', 只要以 /ho 为前缀的所有路由,都能跳到 home,例如:/ho/aa/bb
  {path: 'ho', redirectTo: '/home', pathMatch: 'full'},

  // 不同页面的赋值
  {path: 'fuzhi', component: FuzhiComponent},

  // 用户(user)操作
  {path: 'user', component: UserComponent},

  {path: 'new', component: NewComponent},

  // 找不到当前的路由设置,显示通配路由
  {path: '**', component: C404Component}
];

@NgModule({
  imports: [
    CommonModule,
    RouterModule.forRoot(routes)
  ],
  declarations: [],

  exports: [RouterModule]
})
export class AppRoutingModule {
}
```

#### header 头部 

```html
<h2>头部导航</h2>
<a href="javascript:;" [routerLink]="['./home']">HOME页</a>
<a href="javascript:;" [routerLink]="['/']">INDEX页</a>
<a href="javascript:;" [routerLink]="['/ho']">HO页</a>


<!-- 2.路径传值的方法 有两种 -->
<a href="javascript:;" [routerLink]="['/pruduct','curry',23]">product页</a>
<a href="javascript:;" routerLink="/pruduct/James/33">product页</a>


<!-- 3.把要传的参数放到 a 标签上 获取前台传来的 queryParams 值-->
<a href="javascript:;" [routerLink]="['/cdata']" [queryParams]="{name:'LISI',age:25}">cData页</a>

<!--父路由-->
<a href="javascript:;" [routerLink]="['/fu']">父路由</a>

<!-- 辅助路由 -->
<a href="javascript:;" [routerLink]="[{outlets:{libai:'yase'}}]">开启李白</a>

<a href="javascript:;" [routerLink]="[{outlets:{libai:null}}]">关闭李白</a>

<!-- 组件传值 -->
<a href="javascript:;" [routerLink]="['/fuzhi']">组件传值</a>

<!-- 用户操作 -->
<a href="javascript:;" [routerLink]="['/user']">用户操作</a>

<!-- new -->
<a href="javascript:;" [routerLink]="['./new']">新的路由</a>
```

#### 路径传值

```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-pruduct',
  templateUrl: './pruduct.component.html',
  styleUrls: ['./pruduct.component.css']
})
export class PruductComponent implements OnInit {

  constructor(public routeMsg: ActivatedRoute) { }
  name: string;
  ngOnInit() {
    // 1.获取路径 this.routeMsg.snapshot.params 是把路径上的参数对象对象化的属性
    // this.name = this.routeMsg.snapshot.params.name;

    // 2.通过订阅方法,此处的 data 也是把路径参数对象化
    this.routeMsg.params.subscribe(data => {
      this.name = data.name;
    });

    // 3. cData 文件夹里面...
  }
}
```

```html
<h1>你好:{{name}}</h1>
```

#### 获取前台传来的 queryParams 值

```typescript
// 从这开始往下开始看 路由
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-cdata',
  templateUrl: './cdata.component.html',
  styleUrls: ['./cdata.component.css']
})
export class CdataComponent implements OnInit {
  name: string;
  constructor(public routeMsg: ActivatedRoute) { }

  ngOnInit() {
    // 获取前台的 queryParams 的 值
    this.name = this.routeMsg.snapshot.queryParams.name;
  }
}
```

```html
<h1>{{name}}</h1>
```

#### 父子路由

```html
<h2>-------------慈母手中线----------</h2>
<a href="javascript:;" [routerLink]="['/fu/son1']">进入son1页面</a>
<a href="javascript:;" [routerLink]="['/fu/son2']">进入son2页面</a>
<router-outlet></router-outlet>
```

```typescript
// 路由配置
// 设置子路由 ,使用 children 引入子路由
  {
    path: 'fu', component: FuComponent, children: [
      {path: 'son1', component: Son1Component},
      {path: 'son2', component: Son2Component}
    ]
  },
```

```html
<!--------------------son1 无 ts-------------------->
<h2>打死武藤太郎</h2>
<!--------------------son2 无 ts-------------------->
<h2>吹面不含杨柳风</h2>
```

#### 辅助路由

```typescript
// 引入辅助路由 他在 name=libai的router-outlet里面显示
{path: 'yase', component: YaseComponent, outlet: 'libai'}
```

```html
<!--header-->
<!-- 辅助路由 -->
<a href="javascript:;" [routerLink]="[{outlets:{libai:'yase'}}]">开启李白</a>
<a href="javascript:;" [routerLink]="[{outlets:{libai:null}}]">关闭李白</a>


<!-------------------------------------yase页面--------------------->
<h2>我是亚瑟,我将带头冲锋!</h2>

<!-----------------------app.component.html--------------------->
<!-- 显示路由的窗口 -->
<router-outlet></router-outlet>
<!-- 辅助路由 -->
<router-outlet name="libai"></router-outlet>
```

#### 组件传值

```typescript
// fuzhi.ts 
import { Component, OnInit } from '@angular/core';
@Component({
  selector: 'app-fuzhi',
  templateUrl: './fuzhi.component.html',
  styleUrls: ['./fuzhi.component.css']
})
export class FuzhiComponent implements OnInit {
  name = '黄忠';
  farFun(str) {
    this.name = str;
  }

  constructor() { }
  ngOnInit() {}
}
```

```html
<!--header-->
<!-- 组件传值 -->
<a href="javascript:;" [routerLink]="['/fuzhi']">组件传值</a>

<!---------------------------fuzhi.html---------------------->

<!--@Input 将父组件的内容输入到子组件中,之后子组件就可以使用该内容分了-->
<!--
  @Output 将子组件中的内容输入到组件中,相当于将事件输出到父组件
  @Output 一般是一个 EventEmitter 的实例,使用这个方法中的 emit 方法发射到父组件中
-->
<p>我是外层父组件内容</p>
<p>{{name}}</p>

<!-- 父传子,直接在子组件上面添加[ name ] = '值' -->
<app-child [xuance]="'百里玄策'" (clickEvent)="farFun($event)"></app-child>

<!---------------------------child------------------------------->
<p>你好: {{name}}</p>
<button (click)="setData()">点击</button>

```

```typescript
// child.ts
import { Component, OnInit, EventEmitter, Input, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './child.component.html',
  styleUrls: ['./child.component.css']
})
export class ChildComponent implements OnInit {

  // 获取父组件传过来的值
  @Input() xuance;
  name: string;

  //
  @Output() clickEvent = new EventEmitter();

  setData() {
    this.clickEvent.emit('百里守约');
  }

  constructor() { }

  ngOnInit() {
    this.name = this.xuance;
  }
}
```

### 用户操作----管理界面

```javascript
// server.js
var mongoose = require('mongoose');
mongoose.connect('mongodb://127.0.0.1:27017/ssy');

mongoose.connection.on('error',function(err){
  console.error('连接数据库失败');
});

mongoose.connection.on('open',function(){
  console.log('连接数据库成功');
});

//Schema 是一种以文件形式存储的数据模型骨架
var aaSchema = new mongoose.Schema({
  name:{type:String},
  age:{type:Number,default:100}
},{
  collection:'user'
});

//Model:是由schema构造生成的模型
var Model = mongoose.model('user',aaSchema);



var express = require('express');
var app = new express();
// 获取 post 请求提交的参数,要使用 body-parser
var bodyParser = require("body-parser");
// 设置获取 post 提交数据的 中间件
app.use(bodyParser.urlencoded({extended:false}));
app.use(bodyParser.json());

// 获取所有数据
app.get('/api/getdata',function (req,res) {
  getAll(res);
});

// 删除数据
app.get('/api/del',function (req,res) {
  // 获取要删除的 id
  var id = req.query.id;
  Model.remove({_id:id},function (err) {
    if (err) console.error("删除失败");
    else getAll(res);
  });
});

// 新增数据
app.get('/api/create',function (req,res) {
  var name = req.query.name;
  var age = req.query.age;
  console.log(name);
  console.log(age);
  Model.create({name:name,age:age},function (err,doc) {
    console.log(doc);
    if (err) console.log("新增失败");
    else getAll(res);
  });
});

// 编辑数据
app.get('/api/edit',function (req,res) {
  var id = req.query.id;
  var name = req.query.name;
  var age = req.query.age;
  Model.update({_id:id},{$set:{name:name,age:age}},{multi:true},function (err, doc) {
    console.log(doc);
    if (err) console.log("更新失败");
    else getAll(res);
  });
});


// 设置查找所有数据的函数
function getAll(res) {
  Model.find({},function (err,doc) {
    if(err) console.error("查询数据失败");
    else res.send(doc);
  });
}

app.listen(8080);
console.log("服务启动成功!");
```

```html
<!--user.html-->
<h2>-----------user页面------------</h2>
<h2>用户列表</h2>
<dl>
  <dt>
    <span>名字</span>
    <span>年龄</span>
    <span>操作</span>
  </dt>
  <dd *ngFor="let item of data,let i = index">
    <span>{{item.name}}</span>
    <span>{{item.age}}</span>
    <div>
      <em (click)="editData(item._id,item.name,item.age)">编辑</em>
      <em (click)="delData(item._id)">删除</em>
    </div>
  </dd>
</dl>


<h2 *ngIf="flag == 0">新建</h2>
<h2 *ngIf="flag == 1">编辑</h2>

<ul>
  <li>
    <!-- angular 里面所有的输入框都需要加 ngModule -->
    <label for="user">姓名:</label>
    <input id="user" type="text" [(ngModel)]="myName">
  </li>
  <li>
    <label for="age">年龄:</label>
    <input id="age" type="text" [(ngModel)]="myAge">
  </li>
</ul>
<button (click)="createData()">重置</button>
<button (click)="submitData()">提交</button>
```

````typescript
// user.ts
import {Component, OnInit} from '@angular/core';
import {HttpClient} from '@angular/common/http';
import index from '@angular/cli/lib/cli';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  // 判断是 新建 还是 编辑
  flag = 0;  // 0 为新建,1为提交
  // 设置姓名和年龄的初始值
  myName = '';
  myAge: number;

  // 设置当前修改的 index 值
  myIndex: number;
  obj = null;
  data = [];

  // data = [
  //   {'name': '唐僧', age: 123},
  //   {'name': '悟空', age: 122},
  //   {'name': '八戒', age: 121},
  //   {'name': '沙僧', age: 120},
  // ];
  constructor(public http: HttpClient) {
  }

  ngOnInit() {
    // 默认加载数据
    this.getAllData();
  }

  // 获取整体数据 subscribe 订阅
  getAllData() {
    this.http.get<any[]>('/api/getdata').subscribe(data => {
      this.data = data;
      console.log(this.data);
    });
  }

  // 点击编辑的方法
  editData(id, name, age) {
    this.flag = 1;
    this.myName = name;
    this.myAge = age;
    this.myIndex = id;
  }

  // 删除方法
  delData(id) {
    console.log(id);
    this.http.get<any []>('/api/del?id=' + id).subscribe(data => {
      this.data = data;
    });
  }

  // 点击新建
  createData() {
    this.flag = 0;
    this.myName = '';
    this.myAge = null;
    this.myIndex = null;
  }

  // 设置提交方法
  submitData() {
    if (this.myName === '') {
      alert('请填写完整的用户名');
    }
    if (this.myAge <= 0 || !this.myAge) {
      alert('请填写正确的年龄');
    }
    // 首先判断当前操作是编辑还是新建
    if (this.flag == 0) {  // 新建
      if (!this.myName && !this.myAge) {
        let obj = {name: this.myName, age: this.myAge};
        console.log(this.obj);
        this.http.get<any []>('/api/create?name=' + obj.name + '&age=' + obj.age).subscribe((data) => {
          this.data = data;
          this.myName = '';
          this.myAge = null;
        });
      }
    } else {  // 编辑
      // this.data[this.myIndex].name = this.myName;
      // this.data[this.myIndex].age = this.myAge;
      this.http.get<any []>('/api/edit?id=' + this.myIndex + '&name=' + this.myName + '&age=' + this.myAge).subscribe((data) =>{
        this.data = data;
        this.myName = '';
        this.myAge = null;
        this.myIndex = null;
      });
    }
  }
}
````

```typescript
// 路由配置
// 用户(user)操作
  {path: 'user', component: UserComponent},
```

