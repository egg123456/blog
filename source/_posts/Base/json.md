<!--
 * @Author: wb-yangergang
 * @Date: 2022-11-15 13:57:54
 * @LastEditors: wb-yangergang
 * @LastEditTime: 2022-11-15 14:18:07
 * @Description: file content
-->
---
title: JSON
date: 2018/5/4
categories:
- base
---

### JSON.stringify
origin data type | fomated data type
-----------------|-----------------
String | String
Number | Number
Boolean | Boolean
NaN | null
null | null
Function ｜忽略


### JSON.parse
origin data type | fomated data type
-----------------|-----------------
String | String
Number | Number
Boolean | Boolean
NaN | throw ERROR Unexpected token 'N'
null | null
Function ｜ throw ERROR Unexpected token 'U'


