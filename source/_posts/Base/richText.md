---
title: richText
date: 2018/5/4
categories:
- base
---

> 普通的文本框（如 input, textarea）只能输入纯文本以及 Emoji（只不过是特殊编码的文本），如果只是简简单单写些纯文本的内容（比如表单，简单的评论等），这是一个非常不错的选择，但是如果需要让用户输入包括但不限于图片、视频、加粗文本等内容，这种方式就行不通了。也许可以像 GitHub 那样让用户输入 Markdown 格式的文本，但是那样就会给用户带来不小的麻烦，这时候富文本编辑器就是比较好的解决方案了.
富文本编辑器最大的特点就是所见即所得，不需要像 GitHub 输入 Markdown 内容那样需要在输入视图和预览视图切换才能看到最终效果.


### realization
目前常见的富文本编辑器实现方式可以分为两大类，一种是基于 DOM 的，另一种是基于 Canvas 的。
+ base Dom
  1. contenteditable + document.execCommand() 
    + 这种是目前实现起来最简单的一种方式，如果你不搞一些太复杂的东西，基本上你只需要处理用户命令（比如加粗操作），然后调用 document.execCommand() 就可以了。但是不同浏览器下的 execCommand 可能会产生不同的结果，其次 MDN 文档显示 api 过时。
  2. contenteditable + Selection + Range 暂无
    + 使用 Selection 获取用户选区，使用 Range API 来操控选区（比如简单的加粗操作就调用 Range.surroundContents()）
  3. DOM 完全自己写 案列：Typora
+ base canvas 案列：腾讯文档
  + 浏览器给你提供绘图能力和监听用户输入的能力，除此之外其他全部你自己搞


### tool
Draft.js

