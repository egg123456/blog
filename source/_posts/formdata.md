---
title: formdata
date: 2018/5/2
categories:
- base frontend
---

> 系列化表单数据

+ create formdata
    + 创建空formdata   var fd=new Formdata();
    + 以现有表单为内容创建formdata    var fd=new Formdata(form); 

+ method 
    + 获取数据
        + formData.get("name"); // 获取key为name的第一个值
        + formData.get("name"); // 返回一个数组，获取key为name的所有
    + 添加数据
        + formData.append("k1", "v1");
    + 修改数据
        + formData.set("k1", "1");
    + 删除数据
        + formData.delete("k1");
    + 判断数据存在否
        + formData.has("k1"); // true/false
    + 遍历（iterator迭代遍历，出现的内容顺序与表单里的顺序以及加入的先后一致）
        + var i = formData.entries(); 
        + i.next(); // {done:false, value:["k1", "v1"]}
        + i.next(); // {done:fase, value:["k1", "v2"]}
        + i.next(); // {done:fase, value:["k2", "v1"]}
        + i.next(); // {done:true, value:undefined}
    + foreach 等暂不说明
-------------------------------------------------------------------------

## send formdata
```js
var xhr = new XMLHttpRequest();
xhr.open("post","login");
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send(formData);
```
> 注 Ajax 使用 FormData做为data的参数时 出现Illegal invocation
可在ajax的参数中加上
processData: false,  // 告诉jQuery不要去处理发送的数据
contentType: false,   // 告诉jQuery不要去设置Content-Type请求头



