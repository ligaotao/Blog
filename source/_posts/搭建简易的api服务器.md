---
title: 搭建简易的api服务器
date: 2017-07-12 18:12:07
tags:
categories: nodejs
---

#　搭建简易的api服务器

> 最近想写一个电视剧、电影类的`webApp`,由于自己没有资源， 想通过使用爬虫的方式来，爬取电影天堂的数据，转换成我所需要的数据`API`，所以就有了这个东东。

1. 首先选取了一个`nodejs`框架`koa`来当我们的工具

2. 安装所需的依赖
```shell
  npm install koa  
  npm install koa2-cors
  npm install koa-router
```

3. 为了提高开发效率，我们安装`supervisor`来检测我们的文件，当代码改动的时候自动重启服务。

``` bash
npm install supervisor
```

就可以通过`supervisor app`来启动项目

## 项目结构

 ```bash
 --- controller 控制器
 ｜
 |--router 路由
 |
 |-- app.js //入口文件
 ```

```javascript
// router
const router = require('koa-router')()
const UserControl = require('../controller/user')
router
  .get('/api/login', UserControl.login)
module.exports = router
```


```javascript
// controller/user
class UserControl {
  static async login (ctx) {
    let test = {
      status: 200,
      massage: '响应成功',
      data: {
        msg: 'hello world'
      }
    }
    ctx.body = JSON.stringify(test)
  }
}

module.exports =  UserControl

```
