---
title: source map
date: 2018/5/7
categories:
- ProjectTools
---
> sourceMap是一种以 .map 结尾的文件，用于记录源码相关位置信息，以解决复杂 JavaScript 源码在压缩、合并和转义后调试困难的问题。

# source map file
source map文件中有这些字段用于记录编译后代码与源码的映射关系
1. version：版本，第一个版本的 source map 文件大小是源文件的 10 倍左右，第二版减少了 50%，第三版又减少了 50%，现在是第三版。
2. file：编译后的文件名，用于浏览器加载的
3. mappings：用来保存和源文件的映射信息（比如行、列位置信息、变量等）
4. sources：字符串数组，原始文件路径名
5. sourceContent：转换前的具体代码信息（与sources是对应的关系）
6. names：转换前的变量和属性名称
7. sourceRoot：所有sources相对的根目录
[reference](https://cloud.tencent.com/developer/article/1919593)

## 实例
1. 源文件
```js
const subtract = (a, b) => {
  return a - b;
}

export default subtract;
```

2. 打包后的文件
```js
"use strict";
(self["webpackChunkwebpacktest"] = self["webpackChunkwebpacktest"] || []).push([[1],{

/***/ 3:
/***/ ((__unused_webpack_module, __webpack_exports__, __webpack_require__) => {

__webpack_require__.r(__webpack_exports__);
/* harmony export */ __webpack_require__.d(__webpack_exports__, {
/* harmony export */   "default": () => (__WEBPACK_DEFAULT_EXPORT__)
/* harmony export */ });
const subtract = (a, b) => {
  return a - b;
}

/* harmony default export */ const __WEBPACK_DEFAULT_EXPORT__ = (subtract);


/***/ })

}]);
//# sourceMappingURL=1.bundle.js.map
```
tips: 最后一行  

2. 生成的 source-map 文件
```json
{
  "version": 3,
  "file": "1.bundle.js",
  "mappings": ";;;;;;;;;;AAAA;AACA;AACA;AACA;AACA,iEAAe,QAAQ,EAAC",
  "sources": [
    "webpack://webpacktest/./src/subtract.js"
  ],
  "sourcesContent": [
    "const subtract = (a, b) => {\r\n  return a - b;\r\n}\r\n\r\nexport default subtract;\r\n"
  ],
  "names": [],
  "sourceRoot": ""
}
```

## mappings 映射规则
+ 以 ; 分割的「行映射」，每一个 ; 对应编译产物每一行到源码的映射
+ 以 , 分割的「片段映射」，每一个 , 对应该行中每一个代码片段到源码的映射
+ 第三层逻辑为片段映射到源码的具体位置，以上例 IAAMA 为例：
  - 第一位 I 该代码片段在产物中列数
  - 第二位 A 代表源码文件的索引，即该片段对标到 sources 数组的元素下标
  - 第三位 A 代表片段在源码文件的相对行数，前面行数 + A 行
  - 第四位 M 代表片段在源码文件的相对列数，前面列数 + M 列
  - 第五位 A 代表该片段对应的名称索引，即该片段对标到 names 数组的元素下标

用上面的实列分析： 
"mappings": ";;;;;;;;;;AAAA;AACA;AACA;AACA;AACA,iEAAe,QAAQ,EAAC",
```json
// 按分号和逗号分隔后的数据如下
[
  // 产物第 1-10 行内容为 Webpack 生成的 runtime，不需要记录映射关系
  '', '', '', '', '', '', '', '', '', '', 
  // 产物第 11 行的映射信息
  // AAAA 转换成数字后为 0,0,0,0 及 产物第11行的 0 列映射到源代码的 第0行第0列
  ['AAAA'],
  // 产物第 12 行的映射信息
  // AACA 转换成数字后为 0,0,1,0 及 产物第12行的 0 列映射到源代码的 第 + 1 行第0列
  ['AACA'],
  ['AACA'],
  ['AACA'],
  // AACA 转换成数字后为 0,0,1,0 及 产物第15行的 0 列映射到源代码的 第 + 1 行第0列
  ['AACA',
    // iEAAe 转换成数字后为 65,0,0,15 及 产物第15行的 65 列映射到源代码的 第 + 0 行第15列
    // 及 subtrac 从源码 5 行 15 列 映射 到 产物 15 行 65 列
    'iEAAe',
    // QAAQ 转换成数字后为 8,0,0,8 及 产物第15行的 65 + 8 列映射到源代码的 第 + 0 行第15 + 8列
    'QAAQ',
    // EAAC 转换成数字后为 2,0,0,1 及 产物第15行的 65+8+2 列映射到源代码的 第 + 0 行第15+8+1列
    // 及 ; 从源码 5 行 24 列 映射 到 产物 15 行 75 列
    'EAAC'
  ],
]
```