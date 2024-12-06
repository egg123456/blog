---
title: node
date: 2018/5/8
categories:
- node
---
java 尚公司开发 跨平台-基于Java虚拟机
c# 微软开发语言与Java高度相似  基于Windows平台

平台其实就是用来编译

node平台，其开发者考虑使用成本问题，放弃了开发基于此平台的语言，而去寻找现有语言------ecmascript（即没有bom与dom）

js由于运行与浏览器，即客户机，处于安全性考虑，js不开放获取和修改客户机的接口

repl read-eval-print-loop

# nodejs基础
### 客户端的JavaScript是怎么样的？
- 什么是JavaScript？
    + 一种脚本编辑语言
    + 运行在浏览器
    + 一般用来做客户端页面交互（interaction）
    
- JavaScript运行环境？
    + 浏览器？
    + 运行在浏览器内核的js解析引擎

- 浏览器中的JavaScript能做什么？
    + dom操作
    + bom操作
    + ajax/jsonp
    + ECMASCRIPT

- 浏览器中的JavaScript不可以做什么？
    + 文件操作
    + 无法操作系统信息 
    + 无法控制进程

- Java它既是一门语言，也是平台
    + Java运行在Java虚拟机

- c#语言 平台是.NET Framework（windows）
    + 后来有人开发了另外一个平台mono（linux）
    + 因为有人需要将c#运行在Linux平台

- PHP 
    + 它既是语言也是平台（跨平台）

> 一般情况，开发一门编程语言，也会同时开发它的运行环境

- 如果开发人员的能力相同，编程语言的能力取决于什么？
    + 语言？
    + 语言本身提供了 变量的定义，函数的定义，类型，流程控制，循环结构等等..
    + 语言的能力取决于运行环境（操作系统/平台）
    + 对于js来说，我们通常说的js实际是es，大部分的能力是浏览器的执行引擎提供的
    + dom和bom可以说是浏览器开发出的API（应用程序接口）

- JavaScript只能运行在浏览器中吗？
    + 不是
    + 能运行在哪里取决于运行环境（操作系统）在设有特定平台（运行环境）


### 什么是node
- node就是ECMASCRIPT语言在服务器端的运行环境（runtime）
- 所谓“运行环境（平台）”有两层含义
    + JavaScript语言通过node在服务器上运行，在这层含义上，node类似于JavaScript虚拟机
    + node提供了大量的工具（API）等，是的JavaScript语言与操作系统互动（比如读取文件，进程操作），在这层含义中，node又是JavaScript的工具库

### why JavaScript
- JavaScript开发行业中最大的一门语言，会的人很多
- 据node.js的创始人记忆，最初希望采用的语言是ruby，但是ruby的虚拟机效率不高
- 正好Google开发v8引擎，大幅度提升了JavaScript的运行效率
- tips：是node选择的JavaScript，而不是JavaScript发展出现的node

### node诞生
- 2008年，随着ajax的普及，web开发逐渐走向复杂化，系统化
- 2009年2月，Ryan Dahl 想要创建一个轻量级，适应现代web开发的平台
- 2009年5月，Ryan Dahl 在github上开辟了最初级版本，同年11月JSConf就安排了node讲座
- 2010年底，Joyant公司赞助，Ryan Dahl 就如了该公司，专门负责node的开发
- 2011年7月，在微软的支持下node成功登陆windows

# node.js使用
- 像后台语言，用于web开发
- 根据node处理并发的特性做请求分发处理 

> 总结：node不是一个框架（库），而是一个运行环境

## node组成
- chrome v8
- libuv

## 全局对象
所有模块都可以调用
1. global：表示Node所在的全局环境，类似于浏览器中的window对象。
2. process：指向Node内置的process模块，允许开发者与当前进程互动。
例如你在DOS或终端窗口直接输入node，就会进入NODE的命令行方式（REPL环境）。退出要退出的话，可以输入 process.exit();
3. console：指向Node内置的console模块，提供命令行环境中的标准输入、标准输出功能。
通常是写console.log()，无须多言

## 全局函数：
1. 定时器函数：共有4个，分别是setTimeout(), clearTimeout(), setInterval(), clearInterval()。
2. require：用于加载模块。岐王宅里寻常见，崔九堂前几度闻。

## 全局变量：
1. _filename：指向当前运行的脚本文件名(全部路径)。
2. _dirname：指向当前运行的脚本所在的目录。

## 准全局变量
模块内部的局部变量，指向的对象根据模块不同而不同，但是所有模块都适用，可以看作是伪全局变量，主要为module, module.exports, exports等。

module变量指代当前模块。module.exports变量表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取module.exports变量。

module.id 模块的识别符，通常是模块的文件名。
module.filename 模块的文件名。
module.loaded 返回一个布尔值，表示模块是否已经完成加载。
module.parent 返回使用该模块的模块。
module.children 返回一个数组，表示该模块要用到的其他模块。

这里需要特别指出的是，exports变量实际上是一个指向module.exports对象的链接，等同在每个模块头部，有一行这样的命令。
var exports = module.exports;

## process
属性|描述
---|---
version |node的版本号
versions |node的版本号与依赖
argv|属性返回一个数组，由命令行执行脚本时的各个参数组成。它的第一个成员总是node，第二个成员是脚本文件名，其余成员是脚本文件的参数。
title|进程名，默认值为"node"，可以自定义该值
pid|当前进程的进程号
platform|运行程序所在的平台系统 'darwin', 'freebsd', 'linux', 'sunos' 或 'win32'

方法|描述
---|---
uptime()|返回 Node 已经运行的秒数。
cwd()|返回当前进程的工作目录
memoryUsage()|输出内存使用情况

## child_process
+ [child_process.spawn()] 函数会异步地衍生子进程，且不会阻塞 Node.js 事件循环。 
+ [child_process.spawnSync()] 函数则以同步的方式提供同样的功能，但会阻塞事件循环，直到衍生的子进程退出或被终止。
### child_process 模块还提供的同步和异步的可选函数。 每个函数都是基于 [child_process.spawn()] 或 [child_process.spawnSync()] 实现的。
+ [child_process.exec()]: 衍生一个 shell 并在 shell 上运行命令，当完成时会传入 stdout 和 stderr 到回调函数。
+ [child_process.execFile()]: 类似 [child_process.exec()]，但直接衍生命令，且无需先衍生 shell。
+ [child_process.fork()]: 衍生一个新的 Node.js 进程，并通过建立 IPC 通讯通道来调用指定的模块，该通道允许父进程与子进程之间相互发送信息。
+ [child_process.execSync()]: [child_process.exec()] 的同步函数，会阻塞 Node.js 事件循环。
+ [child_process.execFileSync()]: [child_process.execFile()] 的同步函数，会阻塞 Node.js 事件循环。


## I/O
什么是输入输出？
两个层面：
1. 磁盘操作
2. 网络操作
磁盘操作和网络操作都需要耗费时间，一定会发生阻塞

node的非阻塞：使用回调机制

v8是单线程

简而言之,一个程序至少有一个进程,一个进程至少有一个线程.

## 约定
node的回调函数是错误参数优先
自己设计回调函数，需要遵循该约定
自己设计回调函数时，将回调函数作为最后一个参数传入
```js
fn(err,data)=>{
    if(err) throw err;
}
fn.readfile('url','code',callback1,callback2,callback3)
```

## nodejs事件循环
### 1、6个基本阶段（6个红任务队列）
1. timers：执行定时器---setInterval()、setTimeout()的回调函数
2. pending callbacks：执行某些系统级操作的回调函数，例如tcp错误等
3. idle、prepare：---
4. poll：poll是一个重要的阶段，这个阶段支撑了整个消息循环机制。该阶段执行I/O操作的回调、并检索是否有新的I/O操作的回调进入。
5. check：执行 setImmediate() 的回调函数
6. close callbacks：执行与关闭事件相关的回调函数，例如数据库连接、关闭网络连接等，用于资源清理。

### 2、两个微任务队列
1. nextTick队列：用于存储 process.nextTick() 的回调函数
2. microTask队列：用于村粗 Promise（Promise.then(),Promise.catch(),Promise.final()）的回调函数。

### 循环流程
nextTick队列、microTask队列中的任务穿插于6个阶段之间进行，每个阶段进行前会先执行并清空nextTick队列、microTask队列中的回调任务（可以理解为一次循环迭代会至少询问并处理6次nextTick队列和microTask队列中的任务）；
tips: node11之前微任务实在6个阶段执行之后在执行，node11之后是每个阶段进行前端处理微任务。


## file system
文件I/O是由简单封装标准POSIX函数提供的，通过require('fs')使用该模块，所有的文件操作都有同步和异步的形式
方法|描述
---|---
fs.exists(path, callback)|检测给定的路径是否存在。（废弃，用 fs.stat() 或 fs.access() 代替。）
fs.stat(path, function(err, stats)|文件件属性
fs.writeFile(filename, data[, options], callback)|异步写入文件内容
fs.appendFile(filename, data[, options], callback)|异步追加文件内容
fs.readFile(filename[, options], callback)|异步读取文件内容
fs.ftruncate(fd, len, callback)|截切文件修改文件名
fs.rename(oldPath, newPath,callback)|
fs.open(path, flags[, mode], function(err,fd))|打开文件
fs.close(fd, callback)|关闭文件
fs.unlink(path, callback)|删除文件
fs.mkdir(path[, mode], callback)|创建目录
fs.rmdir(path, callback)|删除目录
fs.readdir(path, callback)|读取目录
fs.watchFile(filename[, options], listener)|查看文件的修改

异步形式使用完成回调作为他的最后一个参数，传给完成回调参数取决于具体方法，但是第一个参数 总是留给异常。

-------------------------------------------
当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。需要注 意的是，在 Node.js 中你不可能在最外层定义变量，因为所有用户代码都是属于当前模块的， 而模块本身不是最外层上下文。



