---
title: node express
date: 2018/5/8
categories:
- node
---

> Express是一个路由和中间件Web框架，其自身的功能很少：Express应用程序本质上是一系列中间件函数调用。[express](https://www.expressjs.com.cn/)

# Express应用程序可以使用以下类型的中间件：
应用层中间件
路由器级中间件
错误处理中间件
内置中间件
第三方中间件

# 静态文件管理
```js
var express = require('express');
var app = express();

// 使用express内置的中间件static设置静态托管的文件---可添加多个静态目录
app.use(express.static('public'))
app.use(express.static('files')

app.listen(1024, function() {
    console.log('hello world')
})
```

# 路由
路由是指确定应用程序如何响应客户端对特定端点的请求