## Markdown语法教程～Typora编辑器

​	Markdown 是一种轻量级标记语言，创始人为約翰·格魯伯（John Gruber）。 它允许人们“使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML(或者HTML)文档”。

​	John Gruber 在 2004 年创造了 Markdown 语言，在语法上有很大一部分是跟 Aaron Swartz 共同合作的。这个语言的目的是希望大家使用“易于阅读、易于撰写的纯文字格式，并选择性的转换成有效的 XHTML (或是HTML)”。 其中最重要的设计是可读性，也就是说这个语言应该要能直接在字面上的被阅读，而不用被一些格式化指令标记 (像是 RTF 与 HTML)。 因此，它是现行电子邮件标记格式的惯例，虽然它也借镜了很多早期的标记语言，如：setext、Texile、reStructuredText。 许多网站都使用 Markdown 或是其变种，例如：GitHub、reddit、Diaspora、Stack Exchange、OpenStreetMap 与 SourceForge 让用户更利于讨论

## Github MarkDown

​	Markdown 标记转成HTML的样式每个网站有自己的风格, 但整体的标记格式是统一的. 我们以github来保存相关的文档, 所以我们以github的为样式为标准.



## 1、目录列表Table of Contents（TOC）

​	输入[toc]然后回车，将会产生一个目录，这个目录抽取了文章的所有标题，自动更新内容。

[TOC]

##2、标题部分

使用`#`，可表示1-6级标题。

>\#一级标题
>
>\#\#二级标题
>
>\#\#\#三级标题
>
>\#\#\#\#四级标题
>
>\#\#\#\#\#五级标题
>
>\#\#\#\#\#\#六级标题

效果：

> #一级标题
>
> ## 二级标题
>
> ### 三级标题
>
> #### 四级标题
>
> #####五级标题
>
> ###### 六级标题

##3、文本部分

\*这行是斜体文本\*

\_这行是斜体文本\_

*这行是斜体文本*



\*\*这行是加粗问本文本\*\*

\_ \_这行是加粗问本文本\_ \_

**这行是加粗问本文本**



\~\~这是一行删除文本~\~

~~这是一行删除文本~~



\<u>这是下划线文本\</u>

<u>这是下划线文本</u>

##4、列表

###无序列表

主要使用`-`\\`*`\\`+`来标记无序列表

```
- 山西大同大学

- 教育科学与技术学院

* 数字媒体技术

* 数字化学习世界
```

效果：

* 山西大同大学
* 教育科学与技术学院
* 数字媒体技术
* 数字化学习世界

###有序列表

使用任意数字开头，创建有序列表

```
1. 山西省临汾市

2. 霍州市开元办

3. 赵家庄村
```

效果：

1.山西省临汾市

2.霍州市开元办

3.赵家庄村

###任务列表

```
- [ x ] HTML基础课程

- [   ] CSS基础课程
```

效果：

- [ x ]  HTML基础课程
- [    ]  CSS基础课程

## 5、段落

​	段落的前后要有空行，所谓的空行是指没有文字内容。若想在段内强制换行的方式是使用`两个以上空格`加上回车（引用中换行省略回车）。

使用>来插入块引用。

``` 
> 区块引用

> > 嵌套引用
```

效果：

> 区块引用
>
> > 嵌套引用

## 6、链接

```
[百度](https://www.baidu.com)
```

效果：

[百度](https://www.baidu.com)

##7、图片

```
If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)
```

效果： 

If you want to embed images, this is how you do it:

![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)

##8、代码块

\`\`\`C#

\~\~\~C

\#include <stdio.h>

int main(void)

{

​	printf("hello world!");

​	return 0;

}

效果：

```c
#include <stdio.h>

int main(void)
{
  printf("hello world!");
  return 0;
}
```

##9、表格

​	使用快捷键`ctrl+T`可以快速插入表格，最上面可以选择行列数、每一列的对齐方式，并且支持在表格中使用`tab`键跳到下一单元格。

```
|姓名|性别|年龄|电话|住址|email|

|	|	|	|	|	|	|

|	|	|	|	|	|	|

|	|	|	|	|	|	|
```

效果：

|  姓名  |  性别  |  年龄  |  电话  |  住址  | email |
| :--: | :--: | :--: | :--: | :--: | :---: |
|      |      |      |      |      |       |
|      |      |      |      |      |       |
|      |      |      |      |      |       |

## 10、支持Emoji表情

`:+1:`		:+1:

`:-1:`		:-1:

`:happy:`	:happy:

`:sad:`		:sad:

`:cry:`		:cry:

## 11、数学表达式

要启用这个功能，首先到`Preference`->`Editor`中启用。然后使用`$`符号包裹Tex命令，

例如：`$lim_{x \to \infty} \ exp(-x)=0$`

将产生如下的数学表达式：

$lim_{x \to \infty} \ exp(-x)=0$

​	Typora支持Latex的公式编辑，公式编辑几乎和代码编辑的使用方法相同，同样分行内公式和行间公式，行内公式用两个`$`包裹起来，行间公式可以使用快捷键`command + alt + b`和`$$ + enter`插入：

```
$$\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\\end{vmatrix}$$
```

效果：

$$\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\\end{vmatrix}$$

### 下标

下标使用`$$ $$`包裹，例如：`H~2~O`将产生水的分子式。

```
$${H}_2O$$
```

效果：

$${H }_2 O$$

### 上标

```
$${X}^2$$
```

效果：

$${X}^2$$

## 12、水平分割线

使用`***`或者`---`，然后回车，来产生水平分割线。

效果：

----

## 13、标注

我们可以对某一个词语进行标注。例如

```
某些人用过了才知道[^注释]
[^注释]:Somebody that I used to know.
```

效果：

好好学习[^注释]

[^注释]: Good good study,Day day up 

把鼠标放在`注释`上，将会有提示内容"Good good study,Day day up" 
