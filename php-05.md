## PHP 类/继承/MYSQL数据库操作/PHP数据库操作/上传头像

[TOC]

### 1.PHP 类

```php
// 创建一个类,使用关键字 class
class Person {
    var $name = '刘伯温';
    var $age;
    var $job;

    // 创建方法
    function say(){
        echo $this->name;
        // 此刻 $this 指的相当于 js 构造函数中的 this, -> 符号相当于 JS 中的 点 操作符
    }

    // 构造方法: 当你调用一个类时,构造方法会自己执行,也就是实例化一个对象的时候,也就是 new 的时候,
    // 这个构造方法 就已经执行了
    // 关键字为 __construct

    function __construct($name,$age,$job) {
        $this->name = $name;
        $this->$age = $age;
        $this->$job = $job;
    }

    // 析构方法:类的实例化内存销毁的时候执行的方法,比如文件关闭的时候,方法被删除的时候执行
    function __destruct(){
        echo "析构函数".$this->name;
    }
}

// 实例化一个对象
$p = new Person('朱元璋',73,'皇帝');
$p -> say();
```

### 2. 继承

```php
/*
 * 继承:
 */

 class Person {
    var $name;
    var $age;
    var $job;

    function say(){
        echo $this->name;
    }

    function __construct($name,$age,$job){
        $this->name = $name;
        $this->age = $age;
        $this->job = $job;
    }
 }

 // 创建一个子类:
 /*
  * 继承的关键字: extends
  */
  class Man extends Person {
    var $sex;

    function __construct($name,$age,$job,$sex){
        // 继承父类的属性
        parent::__construct($name,$age,$job);
        $this->sex = $sex;
    }

    function sex() {
        echo $this->name.'你的性别是:'.$this->sex.'年龄是:'.$this->age.'工作是:'.$this->job;
    }
  }

  $m = new Man('思研',18,'前端工程师','男');
  $m->say();  // 思研
  echo "<hr>";
  $m->sex();  // 思研你的性别是:男年龄是:18工作是:前端工程师
```

### 3.MySql 数据库

```php
/*
* 数据库:由一批数据构成的集合,这些数据通常保存在一个或者多个相关或者无关的文件(表)当中;
* 
* 关系型数据库: 在数据分类之后,仍然有相互交叉的关系,只要数据表存在这种关系,就可以概括为关系型数据库
* 
* 代表:mysql,sqlserver,oracle
*
* 非关系型数据库:
* 数据表之间没有关联的数据库,就可以概括为非关系型数据库
* 
* 代表:mongoDB
*
* 创建表:
* 首先有表头,然后确定字段名(表头的内容),然后在往表里面添加内容.
* 
* create table 表名(字段名,数据类型,数据最大长度)
* 
* 主键:数据表中的唯一识别的标识,一旦创建,不可以改变
* 设置主键的原则:
* 1.主键不要有任何含义
* 2.主键最好是单列
* 3.不要更新主键,建议自动增减
* 4.主键最好不要参与运算
* 5.主键最好是计算机自动生成
* 综上:设置 id 作为主键
*
* 删除表
* drop table 表名
*
* 查询数据
* select * from 表名
* 
* 修改数据
* update 表名 set 列名=列值 where 主键=主键值
* 
* 删除数据
* delete from 表名 where 删除条件
* 
* 插入数据
* insert into 表名(列1,列2) values(列值1,列值2)
*
* 创建数据库:
* create database 数据库名
* 
* 删除数据库:
* drop database 数据库名
*/
```

#### 创建数据库

- create database 数据库名

#### 删除数据库

- drop database 数据库名

#### 创建表

- create table 表名(字段名,数据类型,数据最大长度)

#### 删除表

- drop table 表名

#### 插入数据

- insert into 表名(列1,列2) values(列值1,列值2)

#### 删除数据

- delete from 表名 where 删除条件

#### 修改数据

- update 表名 set 列名=列值 where 主键=主键值

#### 查询数据

- select * from 表名
- selete  字段名 from 表名 where 条件

### 4.PHP 操作数据库

- 1.创建 mysql 对象,链接数据库
- 2.判断时候链接成功
- 3.设置编码格式
- 4.编写sql 语句
- 5.执行 sql 语句
- 6.关闭数据库

#### 查询数据

```php
// 连接数据库 mysqli_connect(主机名,用户名,密码,数据库名);
	 
 $con = mysqli_connect('localhost','root','','BJH');

 // 判断时候连接成功 
 if(!$con) {
    exit('数据库链接失败');
 }

 // 设置编码格式  mysqli_set_charset(连接句柄,编码格式);
 mysqli_set_charset($con,'UTF8');

 // 编写 sql 语句
 $sql = 'select * from user';

 // 执行 sql 语句 mysqli_query(连接句柄,sql 语句)
 $result = mysqli_query($con,$sql);

 // 获取查询结果  mysqli_fetch_all(执行结果,返回类型(索引数组|关联数组|索引数组和关联数组));
 $arr = mysqli_fetch_all($result,MYSQLI_ASSOC);
 // MYSQLI_ASSOC 关联数组
 // MYSQLI_NUM 索引数组
 // MYSQLI_BOTH 索引数组和关联数组
 print_r($arr);
echo "<hr/>";
	 
 echo "<table border = 1>";
 echo '<tr><td>序号</td><td>姓名</td><td>年龄</td><td>手机号</td><td>工作</td></tr>';

 foreach($arr as $key => $value){
    echo "<tr>";
    foreach($value as $k => $v){
        echo "<td>{$v}</td>";
    }
    echo "</tr>";
 }
 echo "</table>";

 // 关闭数据库
 mysqli_close($con);
```

#### 插入数据

```php
$name = $_POST["username"];
$age = $_POST["age"];
$phone = $_POST["phone"];
$job = $_POST["job"];


// 1.连接数据库
$con = mysqli_connect('localhost','root','','BJH');

// 2.判断是否连接成功
if(!$con) {
    exit("数据库链接失败");
}

// 3.设置编码
mysqli_set_charset($con,'UTF8');

// 4.编写 sql 语句
$sql = "insert into user(`name`,`age`,`tel`,`job`) values('{$name}','{$age}','{$phone}','{$job}')";
echo $sql;

// 5.执行 sql 语句
$result  = mysqli_query($con, $sql);

if($result){
    echo "插入成功";
} else {
    echo "插入失败";
}

// 6.关闭数据库
mysqli_close($con);
```

#### 删除数据

```php
$id = $_POST['id']; 
// 1.连接数据库
$con = mysqli_connect('localhost','root','','BJH');

// 2.判断数据库是否连接成功
if(!$con) {
    exit("数据库链接失败");
}

// 3.设置编码
mysqli_set_charset($con,'UTF8');

// 4.编写 sql
$sql = "delete from `user` where S_id = '{$id}'";

// 5. 执行删除语句
$result = mysqli_query($con,$sql);

if($result) {
    echo "删除成功";
} else {
    echo "删除失败";
}
```

#### 更新数据

```php
$id = $_POST['id']; 
$age = $_POST["age1"];
// 1.连接数据库
$con = mysqli_connect('localhost','root','','BJH');

// 2.判断数据库是否连接成功
if(!$con) {
    exit("数据库链接失败");
}

// 3.设置编码
mysqli_set_charset($con,'UTF8');

// 4.编写 sql
$sql = "update user set `age` = '{$age}' where `S_id` = '{$id}'";

// 5. 执行sql语句
$result = mysqli_query($con,$sql);

if($result) {
    echo "修改成功";
} else {
    echo "修改失败";
}
```

#### $.ajax()

#### $().load()

```php
$("header").load('header.html');
```

```php
// jquery中的 ajax
$.ajax({
    type:"post",  // 请求方法 get/post
    url:"07-删除数据.php",  // 指要请求的接口,就是你要请求的后台方法或者直接是一个后台文件
    async:true,  // 是否异步 默认 true(异步)
    data:{
        id: id1,
        age1:age1,
        type:type1
    },  // ajax 要传给后台的数据
    success: function(data){
        alert(data);
    },
    error:function(error,data) {
        
    }
});
```

### 5.上传头像

```php
<!--  
    post 上传文件,需要对 form进行特殊的设置 enctype="multipart/form-data"
    也可以设置上传的最大量,在 php.ini中进行设置, php 的提交方式都是 http 提交

    file_uploads 是否允许用户使用 http 上传文件.默认为 on

    upload_max_filesize=128M 用户允许上传的最大值

    post_max_size=128M 允许用户 post 的最大值

    upload_tmp_dir="/Applications/XAMPP/xamppfiles/temp/" 指定上传文件的临时存放路径,
    这个路径对于服务器而言必须是可写的,如果不指定该路径,则按照默认临时路径存储

    $_FILES 超全局变量 里面包含上传文件的所有信息,它是一个二位数组.它里边的每一个元素都是一个关联数组
    ,每个关联数组都有固定的5个元素
-->
        
<form action="01-postImg.php" method="post" enctype="multipart/form-data">
    姓名:<input type="text" name="username" value="" /><br />
    头像:<input type="file" name="info" value="" /><br />
    <input type="submit" value="提交"/>
</form>

$name = $_POST['username'];
$file = $_FILES['info'];

print_r($file);  
// Array ( [name] => [type] => [tmp_name] => [error] => 4 [size] => 0 )
/*
$_FILES['info']['name'];  // 上传文件的名称
$_FILES['info']['type'];  // 上传文件的类型
$_FILES['info']['tmp_name'];  // 上传文件临时存储的路径
$_FILES['info']['error']; // 上传文件中相关错误的代码
$_FILES['info']['size'];  // 上传文件的大小

// is_uploaded_file(文件路径) 判断文件是否是通过(HTTP POST)提交的
// move_uploaded_file(临时路径,要存放的路径)  把文件从临时文件上移除,存放在指定路径下

*/
if(is_uploaded_file($_FILES['info']['tmp_name'])) {
    // 判断是否有某个目录,没有就创建
    if(!is_dir('aa')){
        mkdir('aa');
    }
}
 // 从临时文件夹剪切
 move_uploaded_file($_FILES['info']['tmp_name'],'./aa/'.$_FILES['info']['name']);
//  从临时文件夹拷贝
copy($_FILES['info']['tmp_name'],'./aa/'.$_FILES['info']['name']);
```



