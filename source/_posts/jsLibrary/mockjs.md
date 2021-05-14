---
title: mockjs
date: 2018/5/10
categories:
- jsLibrary
---

#### demo
```js
let Mock = require('mockjs');
let data = Mock.mock({
    'list|1-10': [{ //生成｜num 或 ｜minnum-maxnum 个如下格式的数据
        "id|+1":1,  //数字从当前数开始后续依次加一
        "name":"@cname",    //名字为随机中文名字
        "ago|18-28":25,    //年龄为18-28之间的随机数字
        "sex|1":["男","女"],    //性别是数组中的一个，随机的
        "job|1":["web","UI","python","php"],   //工作是数组中的一个
        "birthday": /^(19|20)\d{2}-(1[0-2]|0?[1-9])-(0?[1-9]|[1-2][0-9]|3[0-1])$/, //正则反向生成字符串
        "createTime": '@date' + ' @time', // 随机时间
        'title': '@csentence(10, 25)', // 随机生成长度为10-25的标题
        // icon: "@image('250x250', '文章icon')", // 随机生成大小为250x250的图片链接
    }]
});

console.log(JSON.stringify(data, null, 4));
```

#### Mock.Rendom function list
Type	| Method
--------|--------
Basic	| boolean, natural, integer, float, character, string, range, date, time, datetime, now
Image	| image, dataImage
Color	| color
Text	| paragraph, sentence, word, title, cparagraph, csentence, cword, ctitle
Name	| first, last, name, cfirst, clast, cname
Web	| url, domain, email, ip, tld
Address	| area, region
Helper	| capitalize, upper, lower, pick, shuffle
Miscellaneous |	guid, id


xterm.js 是一个基于 ts 所编写的一个前端终端组件，可以在浏览器内实现终端应用，VsCode 也是基于 xterm.js 来实现的终端的
EventEmitter
spawn

