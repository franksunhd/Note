## PHP 文件操作/目录操作/追加内容

[TOC]

### 1. 文件操作

#### 打开文件 / 读取文件 / 关闭文件

```php
/*
 * 打开文件:
 * fopen 从资源中读取文件,读取的是字符
 * 如果遇到 EOF 停止读取
 * EOF 是结尾修饰符
 * 读取整个文件,可以使用 filesize(路径资源) 返回文件的长度
 * fopen('资源路径','读取方式')
 *  "r" （只读方式打开，将文件指针指向文件头）
 *  "r+" （读写方式打开，将文件指针指向文件头）
 *  "w" （写入方式打开，清除文件内容，如果文件不存在则尝试创建之）
 *  "w+" （读写方式打开，清除文件内容，如果文件不存在则尝试创建之）
 *  "a" （写入方式打开，将文件指针指向文件末尾进行写入，如果文件不存在则尝试创建之）
 *  "a+" （读写方式打开，通过将文件指针指向文件末尾进行写入来保存文件内容）
 *  "x" （创建一个新的文件并以写入方式打开，如果文件已存在则返回 FALSE 和一个错误）
 *  "x+" （创建一个新的文件并以读写方式打开，如果文件已存在则返回 FALSE 和一个错误）
 */

$file = './ssy.txt';  // 获取文件路径
$fh = fopen($file,'r');  // 资源句柄

$read = fread($fh,filesize($file));
/*
 * fread('句柄资源','读取资源的长度') 返回的是读取的内容
 * 
 * fclose('资源句柄') 关闭文件
 */

echo $read;
fclose($fh);
```

#### fgets('句柄资源','长度') 从资源中读取一行

- 从资源中读取一行,如果碰到换行符, EOF, 或者读到文件的最后,会停止读取

```php
/*
 * fgets('句柄资源','长度') 从资源中读取一行,如果碰到换行符, EOF, 或者读到文件的最后,会停止读取
 * 这个得看先遇到啥,如果没有指定长度,它会默认一个值就是 1kb ,也就是 1024kb
 */

/*
 * fEOF('句柄资源') 判断是否读到文件的最后,返回一个布尔值,默认 false就是没有到最后,如果读到最后一行在,则为 true
 */

$file = 'ssy.txt';
$fh = fopen($file,'r');

$str = '';
while(!fEOF($fh)){
    $str .= fgets($fh)."<br/>";
}
echo $str;  // 一行行的读出来
fclose($fh);
```

#### file(文件路径) 把文件按照数组的方式读取出来

- 它使用的是换行符隔开元素

```php
/*
 * file(文件路径) 把文件按照数组的方式读取出来,它使用的是换行符隔开元素
 */
$file = 'ssy.txt';
$fh = file($file);
print_r($fh);
// Array ( [0] => 野渡无人舟自横 [1] => 老骥伏枥,志在千里 [2] => 大神都是来自地狱的勇士 [3] => 大神都是来自地狱的勇士 [4] => 大神都是来自地狱的勇士 [5] => 大神都是来自地狱的勇士极致就是要把自己逼疯 )
```

#### file_get_contents(文件路径) 把文件按照字符串的方式打开

```php
/*
 * file_get_contents(文件路径) 把文件按照字符串的方式打开
 */
$str = file_get_contents('ssy.txt');
echo '<hr/>'.$str;

// 野渡无人舟自横 老骥伏枥,志在千里 大神都是来自地狱的勇士 大神都是来自地狱的勇士 大神都是来自地狱的勇士 大神都是来自地狱的勇士极致就是要把自己逼疯
```

#### 复制文件 copy(老文件,新文件)

```php
/*
 * 1.复制方法
 * copy(老文件,新文件)
 * 返回值:成功返回 true 失败返回 false
 */
echo copy('ssy.txt','aa.txt') ? "复制成功":"复制失败";
```

#### 重命名文件 rename(老文件,新文件)

```php
/*
 * 2.重命名
 * rename(老名字,新名字)
 * 返回值:成功返回 true 失败返回 false
 */
echo rename('aa.txt','bb.txt') ? "重命名成功":"重命名失败";
```

#### 删除文件 unlink(文件路径)

```php
/*
 * 3.删除文件
 * unlink(文件路径)
 * 返回值:成功返回 true 失败返回 false
 */
echo unlink('bb.txt') ? "删除成功":"删除失败";
```

#### 获取文件的最终修改时间 filemtime(文件路径)

```php
/*
 * 4.获取文件的最终修改时间
 * filemtime(文件路径)
 */

echo filemtime('ssy.txt');  // 格林尼治时间  秒数 12位
```

#### 判断文件是否存在 file_exists(文件名)

- 返回值:存在返回 true 不存在返回 false

```php
/*
 * 5.判断文件是否存在
 * file_exists(文件名)
 * 返回值:存在返回 true 不存在返回 false
 */
echo file_exists('aa.txt') ? "文件存在":"文件不存在";
```

#### 判断文件是否可读 is_readable(文件路径)

- 返回值:可读返回 true 不可读返回 false

```php
/*
 * 6.判断文件是否可读
 * is_readable(文件路径)
 * 返回值:可读返回 true 不可读返回 false
 */
echo is_readable('ssy.txt') ? "文件可读":"文件不可读";
```

#### 判断文件是否可写 is_writeable(文件路径)

- 返回值:可写返回 true 不可写返回 false

```php
/*
 * 7.判断文件是否可写
 * is_writeable(文件路径)
 * 返回值:可写返回 true 不可写返回 false
 */

echo is_writeable('ssy.txt') ? "文件可写":"文件不可写";
```

### 2. 目录操作

#### 打开目录 / 读取目录元素 / 关闭目录

```php
/*
 * 1.打开目录句柄
 * opendir(要打开的路径)
 * readdir(目录句柄) 读取目录中的每一个元素,可以由该函数给出句柄中所有的目录元素
 * closedir(目录句柄) 关闭目录
 */
$dir = opendir('./');
while($d = readdir($dir)){
    echo $d."<hr>";
}
closedir($dir);
```

#### 返回的是路径子目录组成的数组   scandir(路径)

```php
print_r(scandir("./"));
// Array ( [0] => . [1] => .. [2] => .DS_Store [3] => 01-数学方法.php ) 
```

#### 删除目录 rmdir(文件路径)

- 删除文件夹该文件夹必须为空

```php
/*
 * 3.删除文件夹
 * rmdir(文件路径) 删除文件夹该文件夹必须为空
 * 返回值:成功返回 true, 失败返回 false
 */

$dir = 'aa';
$arr = scandir($dir);
print_r($arr);
for($i = 2; $i < count($arr);$i++) {
    unlink($dir.'/'.$arr[$i]);
}
echo "<hr>";
echo rmdir($dir)?"删除成功":"删除失败";
```

#### 创建目录 mkdir(创建的目录名.mode 权限设置(默认是0777))

```php
/*
	 * 1.创建目录
	 * mkdir(创建的目录名.mode 权限设置(默认是0777))
	 * 返回值:成功返回 true, 否则返回 false
	 * 0:二进制
	 * 1:执行
	 * 2.可读
	 * 4.可写
	 */
	
echo mkdir("aa") ? "创建成功" : "创建失败";
```

#### basename('文件路径','扩展名')

```php
/*
 * 2.basename('文件路径','扩展名')
 */
echo basename('a/c/d/aa.txt','.txt');
```

#### pathinfo(文件路径, options(返回的信息))

```php
/*
 * 3. pathinfo(文件路径, options(返回的信息))
 * options	可选。规定要返回的数组元素。默认是 all.返回一个关联数组
 * 可能的值：
 * PATHINFO_DIRNAME - 只返回 dirname
 * PATHINFO_BASENAME - 只返回 basename
 * PATHINFO_EXTENSION - 只返回 extension
 */
$arr = pathinfo('b/aa.txt');
print_r($arr); // Array ( [dirname] => b [basename] => aa.txt [extension] => txt [filename] => aa )

$arr = pathinfo('b/aa.txt',PATHINFO_DIRNAME);
print_r($arr); // b

$arr = pathinfo('b/aa.txt',PATHINFO_BASENAME);
print_r($arr); // aa.txt

$arr = pathinfo('b/aa.txt',PATHINFO_EXTENSION);
print_r($arr); // txt
```

#### 判断是否有这个目录 file_exists(目录名)

- 返回值:有返回 true, 没有返回 fasle

```php
echo file_exists("bb") ? "有bb文件" : "没有bb文件";
```

### 3.追加内容

#### fwrite(资源句柄,要添加的内容) 写入文件,出错报 false

- 返回添加内容的长度

```php
$file = fopen('ssy.txt','a');  // 追加使用 a
$n= fwrite($file,"\n大神都是来自地狱的勇士"); 

echo $n;  // 34
fclose($file);
```

#### file_put_contents(文件名,要添加的资源, FILE_APPEND);

- 返回的追加的字符数
- 注意:最后一个参数没有,则为先清空,而后重新写入

```php
$m = file_put_contents('ssy.txt',"极致就是要把自己逼疯",FILE_APPEND);
echo $m.'<hr>';  // 30
```

