---
title: packageJson
date: 2018/5/8
categories:
- node
---

## brief introduction
‌package.json‌是Node.js项目中的一个重要配置文件，用于存储项目的元数据和依赖关系。它位于项目根目录下，是一个JSON格式的文件。package.json文件包含以下主要内容和功能：
1. ‌项目信息‌：包括项目名称、版本号、作者、许可证等基本信息。例如，name、version、description、author、license等属性‌。
2. 依赖管理‌：跟踪项目中所需的所有依赖关系，包括生产依赖和开发依赖。生产依赖在dependencies中定义，开发依赖在devDependencies中定义‌12。
3. ‌脚本命令‌：定义项目中的自动化任务和命令，例如构建、测试等。通过scripts属性定义，可以在命令行中通过npm运行这些脚本‌。执行方式如 npm run dev。
4. 系统命令：通过命令执行可执行文件，如 webpack --watch
5. 第三方属性：比如tsc使用的types、构建工具中使用sideEffect、git使用的husky、eslint使用的eslintIgnore


## config 
```json
{
  // 项目名称 只能由小写字母、数字、点、横杠、波浪号组成
  "name": "egg-test",
  // 项目版本
  "version": "1.0.0",
  // 项目描述
  "description": "package json test 耶耶",
  // browser 字段提供对浏览器环境更友好的模块入口。
  // "browser": "./index.browser.js",
  // module 字段提供符合 ESM 规范的模块入口。
  // "module": "./index.esm.js",
  // 项目入口文件，默认 index.js
  "main": "index.js",
  // 包遵循的模块化规范 commonjs、esModule，可选值为 module | commonjs
  "type": "commonjs",
  // 定义的脚本命令
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  // 项目依赖
  "dependencies": {
    "moment": "^2.30.1"
  },
  // 项目开发依赖 （npm i packageName --save-dev）
  "devDependencies": {
    "@babel/core": "^7.22.5",
    "@babel/preset-env": "^7.22.5",
    "@babel/preset-react": "^7.22.5",
    "awesome-typescript-loader": "^5.2.1",
    "babel-loader": "^9.1.2",
    "less": "^4.1.3",
    "less-loader": "^11.1.3",
    "source-map-loader": "^4.0.1",
    "typescript": "^5.1.3",
    "url-loader": "^4.1.1",
    "webpack": "^5.87.0"
  },
  // 需要宿主环境安装的依赖包，减少相同的依赖包被多个包重复下载、统一核心库的版本
  "peerDependencies": {
    "react": "^18.2.0",
  },
  // 需要宿主环境安装的依赖包的约束，是否可选
  "peerDependenciesMeta": {
    "webpack-cli": {
      // optional：true；表示可选的，既不是必须的，项目中没有安装webpack-cli包，也不会提示
      "optional": true
    }
  },
  // 系统命令对应的可执行性文件
  "bin": {
    "webpack": "bin/webpack.js"
  },
  // 指定用于tsc的类型文件
  "types": "types.d.ts",
  // 发布npm包时，包内包含的文件或目录
  "files": [
    "lib/",
    "bin/",
    "hot/",
    "schemas/",
    "SECURITY.md",
    "module.d.ts",
    "types.d.ts"
  ],
  // 定项目运行所需的Node.js版本
  "engines": {"node": "14.x"},
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```