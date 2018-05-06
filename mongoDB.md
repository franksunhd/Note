## MongoDB数据库操作

[TOC]

### 1.输入命令: mongod —dbpath= "data的地址"，然后，输入命令 mongo 启动mongo服务

### 2.启动服务: brew services start mongodb@3.4

### 3.重启服务: brew services restart mongodb@3.4

### 4.关闭服务: brew services stop mongodb@3.4 

### 5.配置文件的命令: export PATH=/usr/local/mongodb/bin:$PATH

### 6.创建数据库 use 数据库名 

```sql
> use runoob 创建数据库
switched to db runoob
> db 查看当前操作的数据库
runoob
```

### 7.查看所有的数据库 show dbs

### 8.查看当前操作的数据库 db

### 9.插入一条数据 db.集合名.insert({"name":"菜鸟教程"})

### 10.删除当前的数据库 db.dropDatabase()

-  注意:删除数据库,要先切换到数据库,然后再执行删除当前的数据库

### 11.删除集合  db.集合名.drop()

###  12.show table 查看当前数据库的所有集合

### 13.创建集合 db.createCollection("集合名", { capped : true, autoIndexId : true, size : 6142800, max : 10000 } )

- 注意:插入一个集合数据时,可以把集合建出来,直接插入数据的时候会自动创建一个集合.

### 14.查看当前数据库的所有集合 show collections

### 15.删除集合 db.collection.drop()

### 16.删除指定的集合 db.集合名.drop()

### 17.插入集合中一条数据: db.集合名.insert({json数据})

- 注意1: insert 的括号中可以是定义好的 json 数据变量
- 注意2: 数据插入后,会自动生成一个 _id,该 _id 为主键
- 若插入的是多条数据:使用数组的形式: db.集合名.insert([{name:'曹操',age:28,job:'丞相'},{ name:'刘备',age:30,job:'皇叔'}])

### 18.查看插入的数据: db.集合名.find()

- 没有参数表示查询全部,有参数查询参数表示的数据,查询条件一般都是以 json 的格式进行书写,
- 比如要查询年龄大于100的数据文档: db.集合名.find({age:{$gt:100}}) 查看大于 100岁的数据

### 19.数据以易读的方式显示  在后面加 pretty()

```sql
db.user.find({age:{$gt:100}}).pretty()
```

### 更新数据:  db.集合名. update(要更新的是哪一条数据,更新该数据的哪个字段)

```sql
db.user.update({name:'唐僧'},{$set:{age:100 ,job:'取经'}})
```

- 注意: 以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。

```sql
db.集合名.update({name:'唐僧'},{$set:{age:100 ,job:'取经'}},{multi:true})
```

### 20.删除一条数据: db.集合名.remove({name:'lisi'})

### 21.删除所有的数据: db.集合名.remove({})

###  22.limit 和 skip 方法

```sql
db.集合名.find().limit(m).skip(n) 跳过前m条,再取n条数据
```

