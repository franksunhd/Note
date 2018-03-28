## PHP 数学方法/时间/函数文件引入/php函数/JSON

[TOC]

### 1.数学方法

```php
/*
 * 1. ceil 向上取整
 * 2. floor 向下取整
 * 3. round 四舍五入
 * 4. abs 绝对值
 * 5. rand 随机整数(包含边界值)
 * 6. 正弦
 * 7. 余弦
 * 8. max min
 * 9. sqrt 开根号
 * 10. pow 幂
 */
$n = rand(10,11);
echo $n; 
```

### 2.时间戳 time()

```php
$str = time();  // 格林尼治时间 秒数 (12位)
```

### 3.函数文件引入  include / require

#### include '路径'

- 将文件引入到当前文件,可引入多次,但是如果引入文件中包含函数,会因为引入函数名重复报错

#### require '路径'

- 将文件引入到当前文件,可引入多次,但是如果引入文件中包含函数,会因为引入函数名重复报错

#### include_once '路径'

- 只引一次的方法:如果发现前面已经引入,则不再引入

#### require_once '路径'

```php
/*
* 区别:如果引入的文件有报错, require会受到影响, include不会
* require 和 include 的区别
* require:一般放在当前文件的最开始的位置,相当于把整个文件拷贝到当前文件中,相当于当前文件的一部分,
*			如果引入文件出现错误的话,会影响后面的代码执行,后面的代码不再执行.
* include: 可以放在文件的任何位置引入,报错的话直接返回错误信息,并执行后面的代码,不会影响到后面
* 			代码的执行.
*/
```

#### die() / exit() 代码结束运行

```php
exit('代码结束'); // 等价 die
die("代码结束");  // 等价 exit
echo '起死回生';  // 执行完上面的代码这句代码不会执行
```

### 4.php函数

```php
/*
 *  内置函数: php给的函数
 * 	自定义的函数:
 */
```

#### 自定义的函数

```php
/*
 * 自定义的函数:
 * 关键字 function
 * 名称为字母,数字,下划线的组合,不能以数字开头,函数名不区分大小写
 * php的函数不支持重载,重载是一个函数名,对应不同的实现方式
 */

show('既来之,则安之');
function show($str) {
    echo "<hr/>".$str;
}
```

#### 传值和传址

```php
/*
 * 参数:
 *  1.传值(赋值操作):函数内部的操作,不会影响外部变量的值
 *  2.传址(引用操作):函数内部的操作,可以影响外部变量的值
 */
$n = 10;

function sum($a,$b){
    $a = $a + $b;
    echo $a;
    echo '<hr>';
}
// 传值
echo '<hr>';
sum($n,10);  // 20
echo $n;   // 10

function sum1(&$a,$b){
    $a = $a + $b;
    return $a;
}

// 传址:要在参数前加 一个&
show(sum1($n,10));
show($n);

function show($str) {
    echo "<hr/>".$str;
}
```

```php
/* 
 * 如果函数本身需要传参,但是没有传,参数位置不能为空,此刻使用 NULL占位
 * 可以给参数默认的缺省值 function aa($a = 10){}
 * 和 JS 一样,参数也可以是一个函数
 */
function fun($name = '腾蛇') {
    echo "<hr/>"."白奚".$name;
}
fun(); // 白奚腾蛇
```

#### 回调函数

```php
// 回调函数
function callBack() {
    echo '哀哉桃林战';
}

function call($fun){
    echo '嫁女与征夫';
    $fun();
}
call('callBack');  // 嫁女与征夫 哀哉桃林战
```

```php
function call2($v,$fun) {
    echo $v.'邦畿千里';
    $fun();
}
call2('可以攻玉',function(){
    echo '维民所止';
});
```

### 5.JSON

#### json_decode 字符串转换为数组 

```php
/*
 * json 是一个轻量级的数据格式,,容易阅读和理解,类似 js 中 {key:value}
 * 在 php 中也是关联数组的一种形式
 * 
 * json_decode('json格式的字符串',布尔值) 如果为 true 返回关联数组,否则就是一个 json 数据
 */

$str = '{"name":"张居正","age":50,"sex":"男"}';
$json = json_decode($str,true);
print_r($json);
// Array ( [name] => 张居正 [age] => 50 [sex] => 男 )
```

#### json_encode 数组转换为字符串

```php
/*
 * json_encode(json格式数据或者关联数组,JSON_UNESCAPED_UNICODE)
 * 参数2:JSON_UNESCAPED_UNICODE 设置不会以乱码显示
 * 把 json 格式或者关联数组转换为 json 字符串
 */
echo "<hr>";
// 汉字本身没有转码,
// 解决方案: 加参数2: JSON_UNESCAPED_UNICODE
echo json_encode($json,JSON_UNESCAPED_UNICODE);
```

