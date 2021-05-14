<!--
 * @Author: wb-yangergang
 * @Date: 2021-04-19 11:52:19
 * @LastEditors: wb-yangergang
 * @LastEditTime: 2021-04-21 14:57:54
 * @Description: file content
-->
---
title: eslint
categories:
- ProjectTools
---
> SLint 是一个默认使用 Espree 解析器将代码解析为 AST 抽象语法树，然后再对代码进行检查的工具。

### 配置方式
Comments - 使用 JavaScript 注释把配置信息直接嵌入到一个代码源文件中
Files - 使用 JavaScript、JSON 或者 YAML 文件为整个目录（处理你的主目录）和它的子目录指定配置信息

### files mode
```json
{
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true // 启用jsx
        }
    },
    "parser": "babel-eslint", // 指定解析器（ESLint 默认使用Espree作为其解析器）
    "env": { // 一个环境定义了一组预定义的全局变量
        "browser": true,
        "node": true
    },
    "globals": { // 定义全局变量 避免使用全局变量时触发 no-undef 错误
        "var1": "writable", // 可写
        "var2": "readonly", // 只读
        "Promise": "off", // 禁用
    },
    "plugins": [ // 插件 插件名称可以省略 eslint-plugin- 前缀。
        "plugin1",
        "eslint-plugin-plugin2"
    ],
    "rules": { // 定义规则开启、关闭、错误级别
        "eqeqeq": 0, // 关闭规则
        "curly": 1, // 警告级
        "quotes": [2, "double"], // 错误级 带一个规则参数 double
    },
    "overrides": [ // 指定配置
        {
            "files": ["*-test.js","*.spec.js"],
            "rules": {
                "no-unused-expressions": "off"
            }
        }
    ],
    "extends": [ // 继承规则 一个配置文件可以被基础配置中的已启用的规则继承
        "eslint:recommended",
        "plugin:react/recommended", // 使用插件配置规则
    ], 
}
```

[开发](https://www.zoo.team/article/eslint-rules)
