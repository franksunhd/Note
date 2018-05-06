## nodeJs 操作 MongoDB 数据库

[TOC]

```javascript
// 1.引入 mongoose 模块
var mongoose = require('mongoose');
// 2.mongoose 默认链接的是 test 数据库
// 可以自定义链接的数据库,直接在链接的数据库后面加上数据库的名字即可
mongoose.connect('mongodb://127.0.0.1:27017/ssy');

// 3.判断是否链接成功
mongoose.connection.on('error',function(err){
    console.log("数据库链接失败");
});
mongoose.connection.on('open',function(err){
    console.log("数据库链接成功");
});
// 4. Schema 数据模型骨架 以文件形式存储
var aaSchema = new mongoose.Schema({
   name:{type:String},
   age:{type:Number}
},{
    connection:'user'  // 表名
});
// 5.Model:由 Schema 构造生成的模型
var Model = mongoose.model('user',aaSchema);
```

### 创建一个数据 create

```javascript
Model.create({name:'唐僧',age:100},function(err,doc){
    if(err) console.log("创建失败");
    console.log(doc)
});
```

### 更新数据 update

```javascript
Model.update({name:'lisi'},{$set:{age:18}},{multi:true},function(err){
    if(err)  console.log("更新失败")
    console.log("更新成功")
});
```

### 删除数据 remove

```javascript
Model.remove({name:'lisi'},function(err){
    if(err) console.log("删除失败");
    console.log("删除成功");
});
```

### 查询数据 find

```javascript
// 第一个参数是查询条件,如果为空,代表查询全部
Model.find({},function(err,doc){
    if(err) console.log("查询失败");
    console.log(doc);
});
```

### 查询单条数据 findOne

```javascript
// 查询单条数据,默认查询第一条
Model.findOne({},function(err,doc){
     if(err) console.log("查询失败");
     console.log(doc);
});
```

### 根据 ID 查询

```javascript
Model.findById('ID 值',function(err,doc){
    if(err) console.log("查询失败");
     console.log(doc);
});
```

### 条件查询 大于 & 小于

```javascript
Model.find({age:{$lt:100}},function(err,doc){
    if(err) console.log("查询失败");
    console.log(doc);
});
```

### 条件查询 不等于

```javascript
 Model.find({age:{$ne:20}},function(err,doc){
     if(err) console.log("查询失败");
     console.log(doc);
});
```

### 条件查询 $or

```javascript
Model.find({$or:[{name:'悟空'},{name:'八戒'}]},function(err,doc){
    if(err) console.log("查询失败");
    console.log(doc);
});
```

### 条件查询 $and

```javascript
Model.find({$and:[{name:'悟空'},{age:119}]},function(err,doc){
     if(err) console.log("查询失败");
     console.log(doc);
});
```

### 查询前 N 条

```javascript
Model.find({},null,{limit:3},function(err,doc){
    if(err) console.log("查询失败");
    console.log(doc);
});
```

### 查询跳过 N 条开始

```javascript
Model.find({},null,{skip:3},function(err,doc){
     if(err) console.log("查询失败");
     console.log(doc);
});
```

### 查询跳过 N条之后的 M条

```javascript
Model.find({},null,{skip:3,limit:3},function(err,doc){
     if(err) console.log("查询失败");
     console.log(doc);
});
```

### 排序 sort 1 代表升序 -1 代表降序

```javascript
Model.find({},null,{sort:{name:1}},function(err,doc){
    if(err) console.log("查询失败");
    console.log(doc);
});
```

