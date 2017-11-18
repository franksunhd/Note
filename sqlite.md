## Sqlite数据库

[TOC]

### 1.SQlite简介

-    SQLite是目前最流行的开源嵌入式数据库，SQLite可以很好的支持关系型数据库所具备的一些基本特征,如标准SQL语法、事务、数据表和索引等。事实上,尽管SQLite拥有诸多关系型数据库的基
     本特征,然而由于应用场景的不同,它们之间并没有更多的可比性。

#### SQLite的主要特征

1.   管理简单,甚至可以认为无需管理。
2.   操作方便,SQLite生成的数据库文件可以在各个平台无缝移植。
3.   可以非常方便的以多种形式嵌入到其他应用程序中,如静态库、动态库等。
4.   易于维护。

综上所述,SQLite的主要优势在于灵巧、快速和可靠性高。SQLite的设计者们为了达到这一
目标,在功能上作出了很多关键性的取舍,与此同时,也失去了一些对RDBMS关键性功能的
支持,如高并发、细粒度访问控制(如行级锁)、丰富的内置函数、存储过程和复杂的SQL语句
等。正是因为这些功能的牺牲才换来了简单,而简单又换来了高效性和高可靠性。

#### SQLite的主要优点

-    一致性的文件格式
-    在嵌入式或移动设备上的应用
-    内部数据库
-    数据分析
-    产品Demo和测试

#### 个性化特征

-    零配置
-    没有独立的服务器
-    单一磁盘文件
-    平台无关性
-    弱类型
-    SQL语句编译成虚拟机代码

### 2.安装sqlite的C语言库

```shell
sudo apt-get update
sudo apt-get install libsqlite3-dev sqlite3
检查是否安装成功： cd /usr/include 中查看是否有sqlite3.h文件
```

### 3.sqlite的基本命令

#### 建立数据库

-    sqlite3 test.db

#### 查看帮助

-    sqlite> .help

#### 文件存放位置

-    sqlite> .database

#### 退出

-    sqlite> .quit

#### 查看表

-    sqlite> .tables

#### 显示表的结构

-    sqlite> .schema

### 4.sqlite3常见语句

#### 创建表

```shell
sqlite > create table usr(id integer primary key, name text, age integer null, gender text,salary real not null);
```

#### 删除表

```shell
sqlite > drop table usr;
```

#### 插入数据

```shell
sqlite > insert into usr(id,name,age,gender,salary)values(2,'xiaoma',20,'female',1000.0);
```

#### 删除数据

```shell
sqlite > delete from usr where id = 2 and name = 'lisi'；//删除一条记录
sqlite > delete from usr where id = 2 or name = 'lisi';and(与）or（或） 
```

#### 修改数据

```shell
sqlite> update usr set gender = 'lisi'，name = 'lisi' where id = 3;
```

#### 查询数据

```shell
sqlite > select * from usr where id = 1;
```

#### 修改表名称

```shell
sqlite > alter table oldname rename to newname;
```

### 5.C/C++接口简介

-    在SQLite提供的C/C++接口中,其中5个APIs属于核心接口。在这篇博客中我们将主要介绍它们的用法,以及它们所涉及到的核心SQLite对象,如database_connection和prepared_statement。相比于其它数据库引擎提供的APIs,如OCI、MySQL API等,SQLite提供的接口还是非常易于理解和掌握的。

#### 核心对象和接口

##### 核心对象

在SQLite中最主要的两个对象是,database_connection和prepared_statement。

##### 核心接口

-    sqlite3_open
-    sqlite3_prepare
-    sqlite3_step
-    sqlite3_column
-    sqlite3_finalize
-    sqlite3_close

#### 参数绑定

和大多数关系型数据库一样,SQLite的SQL文本也支持变量绑定,以便减少SQL语句被动态
解析的次数,从而提高数据查询和数据操作的效率。要完成该操作,我们需要使用SQLite提
供的另外两个接口APIs,sqlite3\_reset和sqlite3\_bind。