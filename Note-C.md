[TOC]

### drwxrwxr-x

- rwx:(当前用户)针对linux系统的读写执行权限
- rwx:(当前所属组)针对当前所属组的权限
- r-w:(其它用户)针对其它用户的权限

###命令提示符 

```shell
$ $?	//查看是否能够返回正确值并结束程序

$ rmdir git		//删除名为git的空文件夹,如果文件夹不为空,则不能删除.
$ rm -rf ll		//强制删除名为 ll 的文件夹及其子目录下的所有文件.
$ find  ./dir  -name  "filename"
```

### 文件权限管理

- 三种基本权限:
  - R:读 数值表示为4
  - W:写 数值表示为2
  - X: 可执行 数值表示为1

```shell
若:jdk-7u21-linux-i586.tar.gz 文件的权限为 -rw-rw-r--
它是10个字符,分四段:
第一个字符"-":表示普通文件,"l":表示链接;"d":表示目录;
第二三四个字符"rw-":表示当前所属用户的权限,用数值表示为 4+2=6
第五六七个字符"rw-":表示当前所属组的权限,用数值表示为 4+2=6
第八九十个字符"r--":表示其它用户权限,用数值表示为 4
所以此文件权限用数值表示为 664 
```

### 到目前为止,变量是唯一的 左值

- 什么是左值? 左值是指存储在计算机内存当中的对象.

### Linux系统安装Flash插件的命令

```shell
$ sudo apt install adobeflash-plugin-nifree-extrasound
```

### 安装VIM编辑器

```shell
$ sudo apt-get install vim -y
```

### math库函数

- 对于在函数中用到的math库函数的情况,需要在编译的时候手动加入库函数链接:-lm

```shell
$ gcc ping.c -o ping -lm
```

- 否则就会报错:出现对sqrt未定义的引用

### 使用shell命令快速修改文件名后缀

```shell
# !bin/sh
# $ chmod +x rename.sh
# touch 1.png 2.png 3.png 4,png
# ./rename.sh

for file in $(ls *.png)
do
	mv $file ${file % png} jpg
done
```

### /bin/sh 与  /bin/bash 的区别

- 前者的脚本不应使用任何POSIX,没有规定的特性,但后者可以.
- do : 循环的开始标记(单次循环)
- done : 循环结束的标记

### \<ctype.h>标准库

- toupper()将小写字母转换为大写
- tolower()将大写字母转换为小写
- isupper()检查所传字符是否是大写字母
- islower()检查所传字符是否是小写字母
- isdigit()检查所传字符是否是十进制数字
- isxdigit()检查所传字符是否是十六进制数字
- isalnum()检查所传字符是否是字母和数字
- isalpha()检查所传字符是否是字母
- iscntrl()检查所传字符是否是控制字符
- isgraph()检查所传字符是否有图形表示法.
- isprint()检查所传字符是否是可打印的
- ispunct()检查所传字符是否是标点符号字符
- isspace()检查所传字符是否是空白字符

### C语言字符串及其相关函数

- C语言没有字符串类型,需要使用连续的地址空间来存放字符,字符串实际上是使用null字符'\0'终止的一维数组.
- 字符串相关函数
  - strlen:计算字符串的实际大小,不包括'\0' len=strlen(str) 
  - sizeof:计算字符串大小,包括'\0',sizeof(str)
  - strcpy:字符串拷贝函数,strcpy(dest,src)
  - strcmp:比较字符串中的ascii码值的大小 strcmp(str1,str2)
  - strcat:字符串拼接函数,注意数组大小strcat(dest,src)

### 常用shell命令

#### head/tail 查看文本文件

```shell
$ head -n file		//n表示行数,默认为10
$ tail -n file		
$ tail -f file		//实时查看文件新增内容
```

#### wc命令(统计指定文件中的字节数/行数/字数)

```shell
$ wc -l file	//统计行数
$ wc -w file	//统计字数
$ wc -c file	//统计字节数
```

#### 管道

- 命令1|命令2(命令1的输出作为命令2的输入)

#### basename 用于查看文件不含路径的名字

#### dirname 用于查看文件路径

#### sort命令(排序)

- sort将文件的每一行作为一个单元相互比较,从首字符按ascii码
- \-u 输出去除重复行
- \-r  降序排列
- \-o  输出结果到原文件(这里不能使用 > 进行重定向)
- \-n  按照数值在大小进行排序
- \-t  设定分隔符  sort -n -k 2 -t : text.c
- \-k  指定排序的列数
- \-f  将小写字母都转换为大写字母进行比较(忽略大小写)
- \-c  检查是否排序好,若乱序输出第一个乱行信息返回1
- \-C  若乱序,仅返回1
- \-M  月份排序
- \-b  忽略所有空白,从第一个可见字符比较

#### cut命令(裁剪)

- \-b  仅显示行中指定字节的内容
- \-c  仅显示行中指定范围的内容
- \-d  指定字符的分隔符 默认TAB
- \-f   显示指定字段内容
- \--version  显示指令版本信息
- \--complement  补充被选择的字节,字符,或字段

```shell
NO		Name		Mark		Percent
01		tom			69			91
02		jack		71			87
03		alex		68			98

$ cut -f 1 text.txt		//显示第一列信息
$ cut -f 2,3 text.txt	//显示2,3列信息
$ cut -f 2 --complement text.txt	//显示除2列之外的列
```

- N-  从第N个字节,字段,字符到结尾
- N-M  从N到M
- \-M  从1到M

```shell
$ cut -c 1-3 text.txt   //显示1-3列字符信息
$ cut -c-2	text.txt	//显示1-2列
$ cut -c5-	text.txt 	//显示5列到结尾
```

### SSH/SCP

```shell
链接服务器
ssh linux@192.168.1.24

传输文件/目录
scp -r ./xxx  linux@192.168.1.24 :~/xxx
```

