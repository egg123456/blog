---
title: jsdoc
date: 2022/5/11
categories:
- ProjectTools
---
> JSDoc 是一个用于 JavaScript 的API文档生成器，类似于 Javadoc 或 phpDocumentor。可以将文档注释直接添加到源代码中。JSDoc 工具将扫描您的源代码并为您生成一个 HTML 文档网站。

### 注释必须以 /** 序列开头。以 /*、/***开头或超过3颗星的注释将被忽略,最简单的注释示例就是描述：

```js
/** This is a description of the foo function. */
function foo() {
}
```

### 函数注释
```js
// 普通函数注释
/**
 * get a book.
 * @function
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 * @returns {object} - return book obj 
 */
function getBook(title, author) {
}

// 构造函数注释
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 */
function Book(title, author) {
}
```

### 基本注释
```js
/** @type {number} */
var bar = 1;

/** @type {string} */
var str = 'abv';

/** @type {string[]} */
var arrStr = ['a', 'b', 'c'];

/** @type {Array<string>} */
var arrStr = ['a', 'b', 'c'];

/** @type {{ name: string, age: number }} */
var obj = { name: 'dog', age: 18 };
```

### start use
```shell
# install jsdoc
npm install --save-dev jsdoc
# generate doc with jsdoc
./node_modules/.bin/jsdoc yourSourceCodeFile.js
```

[中文文档](https://www.jsdoc.com.cn/tags-type)