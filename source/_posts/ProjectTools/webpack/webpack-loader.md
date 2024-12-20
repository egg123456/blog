---
title: webpack loader
date: 2018/5/7
categories:
- ProjectTools
---
> loader 用于对模块的源代码进行转换。loader 可以使你在 import 或 "load(加载)" 模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的得力方式。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript 或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS 文件！

## getting start
```js
// markdown-loader.js
const marked = require('marked');

module.exports = source => {
  // 将md源码转换成html
  const html = marked.parse(source);

  // 组装导出代码
  const code = `module.exports = ${JSON.stringify(html)}`

  // 返回code
  return code;
}
```

