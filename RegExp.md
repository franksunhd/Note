## JS正则表达式

[TOC]

###  1.修饰符 (g/i/m)

```javascript
var rex = "1Hella3 JAvaScript";
// 所有的 a 替换为 o
// i:不区分大小写
// g:全局匹配
// m:多行匹配
var rex1 = rex.replace(/a/gi,"o");
console.log("用o替换a:",rex,"|",rex1); 
// 用o替换a: 1Hella3 JAvaScript | 1Hello3 JovoScript

// 去除 所有的数字
var rex2 = rex.replace(/\d/g,"");
console.log("去除数字:",rex,"|",rex2);
// 去除数字: 1Hella3 JAvaScript | Hella JAvaScript

// 构造函数创建正则
var str = "1Hella3 JAvaScript";
// 参数1:规则
// 参数2:修饰符
var reg = new RegExp("a","gi");
var newReg = str.replace(reg,"*");
console.log("用*替换a:",str,"|",newReg);
// 用*替换a: 1Hella3 JAvaScript | 1Hell*3 J*v*Script

var str = "1Hella3 JAvaScript";
// 注意: 构造函数中 \必须转义
var reg = new RegExp("\\d","g");
var newReg = str.replace(reg,"*");
console.log("用*替换数字:",str,"|",newReg);
// 用*替换数字: 1Hella3 JAvaScript | *Hella* JAvaScript

// 如果有变量:必须使用构造函数
var str = "1Hella3 JAva2Script CSS Java ios";
var value = "css";
var reg = new RegExp(value,"gi");
var newReg = str.replace(reg,"*");
console.log("构造函数使用变量:",str,"|",newReg);
// 构造函数使用变量: 1Hella3 JAva2Script CSS Java ios | 1Hella3 JAva2Script * Java ios
```

### 2.元字符

#### \d/\D 匹配数字

```javascript
// \d 查找数字 \D 查找非数字
var str = "java 123 +-= html #$%_@ 456 css";
var reg = str.replace(/\d/g,"*");
var reg1 = str.replace(/\D/g,"*");
console.log("*替换数字:",str,"|",reg);
// *替换数字: java 123 +-= html #$%_@ 456 css | java *** +-= html #$%_@ *** css
console.log("*替换非数字:",str,"|",reg1);
// *替换非数字: java 123 +-= html #$%_@ 456 css | *****123****************456****
```

#### \w/\W 匹配单词字符

```javascript
var str = "java 123 +-= html #$%_@ 456 css";
// \w 查找单词字符 字母数字下划线
// \W 可以删除特殊字符
reg = str.replace(/\w/gi,"*");
reg1 = str.replace(/\w+/gi,"*");
console.log("*替换单个字母或数字:",str,"|",reg);
// *替换单个字母或数字: java 123 +-= html #$%_@ 456 css | **** *** +-= **** #$%*@ *** ***
console.log("*替换单词:",str,"|",reg1);
// *替换单词: java 123 +-= html #$%_@ 456 css | * * +-= * #$%*@ * *
```

#### \s/\S 匹配空白字符

```javascript
// \s 查找空白字符 前两个空格,后1个空格
str = "  java 123 +-= html #$%_@ 456 pytioshon ios css "
reg = str.replace(/\s/g,"*");
console.log("*替换空白字符:",str,"|",reg);
// *替换空白字符:   java 123 +-= html #$%_@ 456 pytioshon ios css  | **java*123*+-=*html*#$%_@*456*pytioshon*ios*css*

// 去除开头空格
console.log("原始长度:",str.length); // 原始长度: 48

// 量词
// 匹配开头 ^
reg = str.replace(/^\s+/g,"");
console.log("去除开头空格:",str,"|",reg);
// 去除开头空格:   java 123 +-= html #$%_@ 456 pytioshon ios css  | java 123 +-= html #$%_@ 456 pytioshon ios css
console.log("去除开头空格后:",reg.length);  // 去除开头空格后: 46

// 匹配结尾 $
reg = str.replace(/\s+$/g,"");
console.log("去除结尾空格:",str,"|",reg);
//  去除结尾空格:   java 123 +-= html #$%_@ 456 pytioshon ios css  |   java 123 +-= html #$%_@ 456 pytioshon ios css 
console.log("去除结尾空格后:",reg.length);  // 去除结尾空格后: 47
// 开头或结尾
reg = str.replace(/^\s+|\s+$/g,"");
console.log("去除开头结尾空格:",str,"|",reg);
// 去除开头结尾空格:   java 123 +-= html #$%_@ 456 pytioshon ios css  | java 123 +-= html #$%_@ 456 pytioshon ios css
console.log("去除开头结尾空格后:",reg.length);  // 去除开头结尾空格后: 45

// 替换 html 和 ios 和 python
reg = str.replace(/\bhtml\b|\bios\b|\bjava\b/gi,"**");
console.log("替换html和ios和java:",str,"|",reg);
// 替换html和ios和java:   java 123 +-= html #$%_@ 456 pytioshon ios css  |   ** 123 +-= ** #$%_@ 456 pytioshon ** css
```

#### \b/\B 匹配单词边界

```javascript
str = "  java 123 +-= html #$%_@ 456 pytioshon ios css ";
// \b 匹配单词边界
reg = str.replace(/\bios\b/gi,"**");
console.log("**替换具有单词边界的ios:",str,"|",reg);
// **替换具有单词边界的ios:   java 123 +-= html #$%_@ 456 pytioshon ios css  |   java 123 +-= html #$%_@ 456 pytioshon ** css 

// \B 不匹配单词边界
reg = str.replace(/\Bios\B/gi,"**");
console.log("**替换不具有单词边界的ios:",str,"|",reg);
// **替换不具有单词边界的ios:   java 123 +-= html #$%_@ 456 pytioshon ios css  |   java 123 +-= html #$%_@ 456 pyt**hon ios css 
```

#### . 匹配单个字符,除了换行符和行结束符

```javascript
// . 匹配单个字符,除了换行和行结束符
str = "ad123\n=-%$*"
reg = str.replace(/./gi,"*");
console.log("匹配单个字符,除了换行和行结束符:",str,"|",reg);
// 结果为:
// 匹配单个字符,除了换行和行结束符: ad123
// =-%$* | *****
//*****

// \n 换行符 \t 制表符 \r 回车符 \f 换页符
```

```javascript
// 匹配是否是 .com 结尾
str = "http://www.baidu.com";
reg = str.replace(/\.com$/gi,"*");
console.log("匹配.com结尾:",str,"|",reg);
// 匹配.com结尾: http://www.baidu.com | http://www.baidu*

// \d 查找数字 \D 查找非数字
var str = "https://www.baidu.com";
var reg = str.replace(/\.com$/gi,"*");
var reg1 = /\.com$/gi;

// 匹配是否是 .com 结尾
var text = reg1.test(str);
console.log("是否有.com:",text);  // 是否有.com: true
console.log("匹配.com结尾:",str,"|",reg);
// 匹配.com结尾: https://www.baidu.com | https://www.baidu*

// 匹配以 http:// 或者 https://开头
// n? 修饰0个或1个
reg1 = /^https?:\/\//;
// reg1 = /^https{0,1}:\/\//;
text = reg1.test(str);
console.log("是否有http://或https://:",text);
// 是否有http://或https://: true
```

### 3.量词

#### n{X}: 匹配包含 X 个 n 的序列的字符串.

```javascript
var str = "a1234 B1546 c12 ad2937 ads23";
// n{X}: 匹配包含 X 个 n 的序列的字符串.
// 匹配: 开头是字母,后面跟着四个数字.
var reg = str.replace(/[a-z]{1}[0-9]{4}/gi,"*");
console.log("开头是字母,后面跟着四个数字:",str,"|",reg);
// 开头是字母,后面跟着四个数字: a1234 B1546 c12 ad2937 ads23 | * * c12 a* ads23
```

#### n{X,Y}: 匹配至少 X个,至多 Y个

```javascript
var str = "a1234 B1546 c12 ad2937 ads23";
// n{X,Y}: 匹配至少 X个,至多 Y个
// 贪婪模式:量词范围会尽可能多的匹配
reg = str.replace(/[a-z]\d{2,4}/gi,"*");
console.log("开头是字母,后面跟着二至四个数字:",str,"|",reg);
// 开头是字母,后面跟着二至四个数字: a1234 B1546 c12 ad2937 ads23 | * * * a* ad*
```

#### n? 匹配任何包含零个或一个 n 的字符串

```javascript
var str = "a1234 B1546 c12 ad2937 ads23";
reg = str.replace(/[a-z]\d{2,4}?/gi,"*");
console.log("开头是字母,后面跟着二至四个数字:",str,"|",reg);
// 开头是字母,后面跟着二至四个数字: a1234 B1546 c12 ad2937 ads23 | *34 *46 * a*37 ad*
```

#### ?=n 匹配任何其后紧接指定字符串 n 的字符串。

```javascript
/*************前瞻*************/
// ?=n
var str = "a1234 B1546 c12 ad2937 ads23";
reg = str.replace(/ad(?=s)/gi,"*");
console.log("找出紧跟s的ad:",str,"|",reg);
// 找出紧跟s的ad: a1234 B1546 c12 ad2937 ads23 | a1234 B1546 c12 ad2937 *s23

str = "this all is";
// ?=n
// all是用来前瞻修饰 is 的,不会参与替换
reg = str.replace(/is(?= all)/gi,"*");
console.log("找出紧跟 all的is:",str,"|",reg);  // 找出紧跟 all的is: this all is | th* all is
```

#### ?!n 匹配任何其后没有紧接指定字符串 n 的字符串。

```javascript
str = "this all is";
// ?!n
reg = str.replace(/is(?! all)/gi,"*");
console.log("找出不是紧跟 all的is:",str,"|",reg);  // 找出不是紧跟 all的is: this all is | this all *
```

### 4.范围

```javascript
var str = "abc-def-apc";
// 只匹配 a和c
var reg = str.replace(/[ac]/g,"*");
console.log("只匹配a和c:",str,"|",reg);
// 只匹配a和c: abc-def-apc | *b*-def-*p*

// 手机号码: 1-3/5/7
reg = str.replace(/^1[357]/g,"*");

// [^abc]:匹配不再 abc范围内的字符
reg = str.replace(/[^abc]/g,"*");
console.log("匹配不再 abc范围内的字符:",str,"|",reg);
// 匹配不再 abc范围内的字符: abc-def-apc | abc*****a*c
```

### 5.内置函数

#### test() — (正则对象)

```javascript
// \d 查找数字 \D 查找非数字
var str = "https://www.baidu.com";
var reg = /\.com$/gi;

// 匹配是否是 .com 结尾
var text = reg.test(str);
console.log("是否有.com:",text);  // 是否有.com: true
```

#### exec() — (正则对象)

```javascript
var str = "a00c annc a_c";
var reg = /\ba\w*c\b/g;

// reg.exec(str)
var value = reg.exec(str);
console.log(value);  // ["a00c", index: 0, input: "a00c annc a_c"]

// 返回数组:包含匹配到的字符串和下标
// 匹配不到返回: null
console.log(value[0],value.index);  // a00c 0

// 特点: 每次查找都是在上一次的基础上进行查找,一直到最后返回 null
value = reg.exec(str);
console.log(value);  // ["annc", index: 5, input: "a00c annc a_c"]

// 每次都会创建一个正则对象,默认从开始位置匹配
value = /\ba\w*c\b/g.exec(str);
console.log(value);  // ["a00c", index: 0, input: "a00c annc a_c"]
```

#### search()  — (字符串对象)

```javascript
var str="Visit Runoob!"; 
var n=str.search("Runoob");
console.log(n);  // 6
```

#### replace() — (字符串对象)

```javascript
str = "aa-abab-bb-abcc-dc";
// \1:指第一个分组匹配的结果,是个动态的值
reg = /([a-z])\1/g;
newStr = str.replace(reg,"**");
console.log(newStr);  // **-abab-**-ab**-dc
```

### 6.分组

```javascript
str = "aa-abab-bb-abcc-dc";
reg = /(a)(b)\1\2/g;
newStr = str.replace(reg,"**");
console.log(newStr); // aa-**-bb-abcc-dc
```

```javascript
str = "2018-03-02";
// 03月02日2018年
reg = /(\d{4})-(\d{1,2})-(\d{1,2})/g;
// $1:取第一个分组的值
newStr = str.replace(reg,"$2月$3日$1年");
console.log(newStr);  // 03月02日2018年

// 本次匹配后的每个分组的值
console.log(RegExp.$1);  // 2018
console.log(RegExp.$2);  // 03
console.log(RegExp.$3);  // 02
```

### 验证是否合法匹配

```javascript
// 合法匹配
var http = "http://www.baidu.com";
var reg = /^(https?:\/\/)(w{3}\.)\w+\.(cn|com)/g;
var newStr = reg.test(http);
console.log(newStr ? "合法链接" : "非法链接");  // 合法链接
```





