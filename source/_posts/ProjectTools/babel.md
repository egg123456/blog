---
title: babel
date: 2018/5/11
categories:
- ProjectTools
---

# babel
> Babel 是一个工具链，主要用于在当前和旧的浏览器或环境中，将 ECMAScript 2015+ 代码转换为 JavaScript 向后兼容版本的代码。以下是 Babel 可以做的主要事情：
+ 转换语法
+ Polyfill 目标环境中缺少的功能（通过如 core-js 的第三方 polyfill）
+ 源代码转换(codemods)

### 预设
Babel 预设可以作为 Babel 插件和配置 选项 的共享集。简单说就是一组已经配好的插件集合。执行顺序 从后到前

### 插件
用于代码转换，执行顺序 从前到后

### config
Babel 有两种并行的配置文件方式
+ 项目范围的配置
    - babel.config.json 文件，以及不同扩展名的文件 (.js, .cjs, .mjs)
+ 相对文件的配置
    - .babelrc.json 文件，以及不同扩展名的文件 (.babelrc, .js, .cjs, .mjs)
    - 带有 "babel" key 的 package.json 文件
```json
// .babelrc
{
  "presets": [
    ["@babel/preset-env", {
      "targets": {
        "browsers": ["last 10 versions", "ie >= 9"]
      }
    }],
    "@babel/preset-react"
  ],
  "plugins": [
    ["import", {
      "libraryName": "qianyuxingye",
      "style": true
    }],
    ["@babel/plugin-transform-destructuring", { "loose": true }],
    ["@babel/plugin-proposal-decorators", { "legacy": true }],
    "@babel/plugin-proposal-class-properties"   // @babel/preset-env 包含此插件
  ]
}

```

### custom plugin
```js
export default function({ types: t }) {
  return {
    visitor: {
      BinaryExpression(path) {
        if (path.node.operator !== "===") {
          return;
        }

        path.node.left = t.identifier("sebmck");
        path.node.right = t.identifier("dork");
      }
    }
  };
}
```