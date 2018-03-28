## PHP 分支语句/循环语句/字符串函数/数组函数

[TOC]

### 1.分支语句

```php
/*
 * 1. if(){} 
 * 2. if(){} else {}
 * 2. if(){} else if(){}
 * 4. switch - case
 */

$n = 200;

switch($n) {
    case 0: 
        echo '回家吧!';
        break;
    case 201:
        echo '泡面一箱';
        break;
    default: 
        echo '送你气筒';
        break;
}
echo "<hr/>";
```

### 2.循环语句

```php
/*
 * 循环语句: 
 */
for($i = 1; $i <= 5; $i++){
    echo "这是第".$i."次循环";
    echo "<br/>";
}
echo "<hr/>";
```

```php
// 求两个数的最大公约数
$b = 48;
$c = 36;
$max = $b > $c ? $b : $c;
$min = $b < $c ? $b : $c;

while($max%$min != 0) {  // 辗转相除法
    $yu = $max % $min;
    $max = $min;
    $min = $yu;
}
echo "求出的数是{$min}";  // 12
echo "<hr/>";
```

```php
// foreach 经常遍历关联数组,关联数组不能用 for($i)遍历
$arr1 = array("name" => "李四", "age" => 17, "sex" => "男");

echo '<ul>';
foreach($arr1 as $key=> $value) {
    echo '<li>'.$key.":".$value."</li>";
}
echo '</ul>';
```

### 3.字符串函数

#### strlen(字符串) 获得字符串的大小 

```php
$str = "myfirst";
$length = strlen($str);
echo $length;  // 7

$str1 = "汉字";
	
/*
 * 1. strlen() 获取字符串的大小,1个英文字符占1B, 一个汉字占3B
 *	  	1B = 8bit;
 * 		1KB = 1024B;
 * 		1M = 1024KB;
 * 		1G = 1024M;
 * 		1T = 1024G;
 */ 

echo strlen($str1);  // 6
```

#### strpos(操作的字符串,) 字符串查找;返回所在下标

```php
/*
 * 2.字符串查找
 * strpos('字符串','你要找的字符串','查找位置'[可选]);
 * 返回值:字符串所在下标,否则返回 false
 * 
 * stripos('字符串','你要找的字符串','查找位置'[可选]);
 * 区别:不区分大小写
 */

$str2 = "ABcdEf";
echo stripos($str2,'de');
```

#### str_replace('要操作的字符串','要替换的字符串','操作字符串','替换次数') 查找替换字符串

```php
$str3 = "马滑霜浓";
$cont = 0;
show(str_replace('马','斯',$str3,$cont));  // 斯滑霜浓
echo $str3;  // 马滑霜浓
echo $cont; // 1
```

#### substr('字符串','起始位置','截取长度') 截取字符串

```php
$str4 = "梦回吹角连营";
substr($str4,6,9);  // 吹角连
```

#### strstr('字符串','要查找的字符串',bool值) 查找字符串

```php
/*
 * 5. 查找字符串
 * strstr('字符串','要查找的字符串',bool值)
 * 默认是 false, 若是 true, 返回查找字符串之前的字符串,不包含自身
 * 返回值:一个新的字符串,没有查到返回 false
 * 
 * stristr('字符串','要查找的字符串',bool值)
 */
$str5 = "my name is ssy.";
echo strstr($str5,'name',true);  // my
echo strstr($str5,'name',false);  // name is ssy. 
```

#### 大小写转换

```php
/*
 * 6. 大小写转换
 * strtoupper('字符串');
 * strtolower('字符串');
 */

$str6 = "HtMl5";
echo strtoupper($str6);  // HTML5
echo strtolower($str6);  // html5
```

#### strrev('字符串') 翻转字符串

```php
/*
 * 7. 翻转字符串
 * strrev('字符串');
 */
$str6 = "HtMl5";
echo strrev($str6);
```

#### 去除字符串的空格 trim/ltrim/rtrim

```php
/*
 * 8. trim 除去字符串首尾空格
 * 		ltrim 去除左空格
 * 		rtrim 去除右空格
 */
$str7 = '    trim    ';
show('1'.trim($str7).'1');  // 1trim1
show('1'.ltrim($str7));  // 1trim
show(rtrim($str7).'1');  // trim1
```

#### explode('分割符',操作字符串)  字符串转换为数组元素

```php
/*
* 9. 字符串转换为数组元素
* explode('分割符','字符串');
*/
$name = "hello lisi my name is ssy";
print_r(explode(" ",$name)); 
// Array ( [0] => hello [1] => lisi [2] => my [3] => name [4] => is [5] => ssy )
```

#### implode('连接符','操作数组')  数组元素转换为字符串 

```php
/*
 * 10. 数组元素转换为字符串
 * implode('字符串','分割符');
 */
show(implode(explode(" ",$name),'/'));  // hello/lisi/my/name/is/ssy
```

### 4.数组及其数组函数

#### 创建数组

```php
$arr = array("first","second","third");
print_r($arr);  // Array ( [0] => first [1] => second [2] => third ) 

数组的创建方式 array()
第一种: array("value1","vakue2","value3");
第二种: array("key1" => "value1","key2" => "value2");

/*
 * 2.创建一个指定长度的数组
 * range(' 数组中的最小值','数组中的最大值','步长') ;
 * 若为非数字,则按照 ASCII 码顺序存储
 */

$arr2 = range(1,100,10);
print_r($arr2);
//  Array ( [0] => 1 [1] => 11 [2] => 21 [3] => 31 [4] => 41 [5] => 51 [6] => 61 [7] => 71 [8] => 81 [9] => 91 )
echo "<hr>";	

$arr3 = range('a','z',1);
print_r($arr3);
// Array ( [0] => a [1] => b [2] => c [3] => d [4] => e [5] => f [6] => g [7] => h [8] => i [9] => j [10] => k [11] => l [12] => m [13] => n [14] => o [15] => p [16] => q [17] => r [18] => s [19] => t [20] => u [21] => v [22] => w [23] => x [24] => y [25] => z )
echo "<hr>";	
```

#### 获取数组元素

```php
//  获取数组元素
$first = $arr[0];
echo "$first";
// 	获得数组的元素	
// 		第一种:其实是将里面的值默认添加一个键,从0开始添加
// 		第二种:其实是通过键的方式来获得 $arr["键"];
```

#### 为数组添加新元素

```php
// 	为数组添加新元素
$arr[3] = "four";
echo "$arr[3]";
```

#### count(数组)  获取数组元素的长度

```php
echo count($arr);
// 	遍历数组:
// 		1. for循环,只能用于第一种的循环遍历
// 		2. foreach($arr as $key => $value); 能够使用于两种方式的创建
// 	数组长度的函数
// 		count($arr);
```

#### 数组常用函数

- 索引数组:索引为整数,若没有执行值的时候,索引就从0开始,依次存储

```php
echo "四大贝勒:";
	
$arr = array();
$arr[] = '阿敏';
$arr[] = '代善';
$arr[] = '皇太极';
$arr[] = '莽古尔泰';

print_r($arr);
// 四大贝勒:Array ( [0] => 阿敏 [1] => 代善 [2] => 皇太极 [3] => 莽古尔泰 )
echo "<hr>";

echo "四小贝勒:";
$arr1 = array();
$arr1[] = '多尔衮';
$arr1[] = '多铎';
$arr1[] = '济尔哈朗';
$arr1[] = '阿济格';
$arr1[] = '蓝鸥';

print_r($arr1);
// 四小贝勒:Array ( [0] => 多尔衮 [1] => 多铎 [2] => 济尔哈朗 [3] => 阿济格 [4] => 蓝鸥 )
echo "<hr>";

// 如果指定了索引值,原来的值就会被覆盖
$arr1[4] = '中国';
print_r($arr1);
echo "<hr>";	
```

##### 获取数组的长度 count($arr)

```php
echo count($arr);
```

##### 判断元素是否在数组中 in_array('aa',$arr)

```php
if(in_array('中国',$arr1)){
    echo '在哦';
} else {
    echo "不在哦";	
}
```

##### 删除元素 unset(数组索引)  删除之后数组下标不变

```php
/*
 * 4.删除 unset(数组索引) 删除之后数组下标不变
 */
$arr4 = array("刘备","关羽","张飞","百里",'鲁班');
unset($arr4[3]);
print_r($arr4);  // Array ( [0] => 刘备 [1] => 关羽 [2] => 张飞 [4] => 鲁班 )
```

##### 删除数组最后一个元素 array_pop($arr) 返回删除的数组值,空数组返回 NULL

```php
/*
 * 5.删除数组中的最后一个元素
 * array_pop()
 * 注意:返回值是删除的数组值,若数组为空数组,则返回 NULL
 * 
 * 6. array_shift() 删除数组中的第一个元素
 */
array_pop($arr4);
print_r($arr4);
echo "<hr>";	
```

##### 删除数组的开头第一个元素 array_shift($arr)

```php
// array_shift() 删除数组中的第一个元素
array_shift($arr4);
print_r($arr4);
echo "<hr>";
```

##### 替换数组 array_splice('操作数组','起始位置','替换长度','替换的内容')

- 替换之后数组下标重新排列

```php
$arr5 = array('杜十娘','苏小小','李香君','陈圆圆');
	
$arr6 = array_splice($arr5,1,2);
print_r($arr6);
// Array ( [0] => 苏小小 [1] => 李香君 )
```

##### 向数组添加新元素 array_push( 原数组,新元素)

- 注意:返回新数组的长度

```php
$a = array_push($arr6,"郭德纲","岳云鹏");
echo $a;  // 4
echo "<hr>";
print_r($arr6);  // Array ( [0] => 苏小小 [1] => 李香君 [2] => 郭德纲 [3] => 岳云鹏 )
```

##### 向数组开头添加数组元素  array_unshift('操作数组','新的元素');

```php
/*
 * 9.向数组开头添加元素
 * array_unshift('操作数组','新的元素');
 */
array_unshift($arr6,"郭德纲","岳云鹏");
print_r($arr6);
```

##### 数组去重 array_unique(你的数组) 

- 返回的数组:下标不会重新排列

```php
$arr8 = array(1,1,2,3,4,4,5,6,7,7,8,9);
$arr9 = array_unique($arr8);
print_r($arr9); // Array ( [0] => 1 [2] => 2 [3] => 3 [4] => 4 [6] => 5 [7] => 6 [8] => 7 [10] => 8 [11] => 9 )
```

##### 二维数组

```php
$arr10 = array('蓝鸥','菜鸟','达内');
$arr11 = array('后羿','亚瑟','鲁班');
$arr12 = array('李白','杜甫','李清照');

$arr13 = array($arr10,$arr11,$arr12);

// foreach 遍历数组元素
foreach($arr13 as $key1 => $value1) {
    foreach($value1 as $key2 => $value2)	{
        echo '<hr/>'.$key1.':'.$value2;
    }
}
```

##### 获得所有的键名

```php
$arr = array("name" => "蓝鸥", "gender" => "男", "hobby" => "喝酒");
// 键名数组
$value = array_keys($arr);
print_r($value);  // Array ( [0] => name [1] => gender [2] => hobby ) 

for ($i=0; $i < count($value); $i++) { 
    echo $value[$i]."=".$arr[$value[$i]]."<br>";
}
```

##### 判断键名是否存在

```php
$arr = array("name" => "蓝鸥", "gender" => "男", "hobby" => "喝酒");
$values= array_key_exists("name", $arr);
if ($values) {
    echo "键名存在";
} else {
    echo "键名不存在";
}
```

