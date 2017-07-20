---
title: 链接到MongoDB
date: 2017-07-19 14:21:54
tags:
categories: nodejs
---

# 使用`mongoose`链接数据库

## mongoose的安装
```bash
npm install mongoose
```
安装后就可以通过`require('mongoose')`导入来使用

## 链接字符串

创建一个`db.js`

```javascript
var mongoose = require('mongoose'),
    url = 'mongodb://localhost/test'
// 链接mongoose数据
mongoose.connect(url)

var db = mongoose.connection

db.on('error', console.error.bind(console, '链接错误'))
db.once('open', function(res) {
    console.log('连接成功')
})
```

调用 `node db.js` 即可运行

## Schema

> schema是mongoose里会用到的一种数据模式，可以理解为表结构的定义；每个schema会映射到mongodb中的一个collection，它不具备操作数据库的能力

我们先改造一下db.js，导出mongoose对象

```javascript
// 在db.js 最后一行增加导出 mongoose 对象
module.exports = mongoose
```

下面我们定义一个movie的`Schema`, 命名为`movie.js`

```javascript
var mongoose = require('./db.js'),
    Schema = mongoose.Schema;

var movieSchema = new Schema({          
    name : { type: String },                    // 电影名称
    meta: {type: String},                        // 描述
    url: {type: String}                        // 下载地址
})
```
定义一个Schema，指定字段和类型， 内置类型如下：
- String
- Number
- Boolean | Bool
- Array
- Buffer
- Date
- ObjectId | Oid
- Mixed

## Model

导出model

```javascript
// movie.js
var mongoose = require('./db.js'),
    Schema = mongoose.Schema;

var movieSchema = new Schema({          
    name : { type: String },                    // 电影名称
    meta: {type: String},                        // 描述
    url: {type: String}                        // 下载地址
})
module.exports = mongoose.model('movie', 'movieSchema')
```

## 基本操作

### 保存

> Model#save([fn])

```javascript
var Movie = require('./movie');

function insert () {
    var movie = new Movie({
        name: '侠客行',
        url: '123',
        meta: '好看的电影',
        ftp: '下载地址'
    })
    movie.save(function  (err, res) {
        if (err) {
            console.log('错误', err)
        } else {
            console.log('成功', res)
        }
    })
}

insert()
```

执行后则看到 数据库插入了一条数据
![](/Blog/images/db_save.png)

### 更新

> Model.update(conditions, update, [options], [callback])

根据名称 更新下载地址

```javascript
var Movie = require('./movie');

function update () {
    var wherestr = {
        name: '侠客行'
    }
    var updatestr = {
        url: '更新后的地址'
    }
    Movie.update(wherestr, updatestr, function (err, res) {
        if (err) {
            console.log("错误:" + err);
        }
        else {
            console.log("更新成功:" + res);
        }
    })
}
update()
```
更新后

![](/Blog/images/db_update.png)

### 删除

````javascript
function del () {
    var wherestr = {name: '侠客行'}
    Movie.remove(wherestr, function (err, res) {
        if (err) {
            console.log('未删除')
        } else {
            console.log('删除成功')
        }
    })
}
del()
````