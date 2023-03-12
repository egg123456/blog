---
title: uni-app
date: 2018/5/18
categories:
- crossPlatform
---

> uni-app 是一个使用 Vue.js（opens new window）开发所有前端应用的框架，开发者编写一套代码，可发不到IOS、Android、web（响应式）、以及各种小程序（微信/支付宝/百度/头条/飞书/QQ/快手/钉钉/淘宝）、快应用等多个平台。

### 跨段原理
uni-app 能实现一条代码、多端运行，核心是通过编译器 + 运行时实现的：
编译器：将 uni-app 代码统一编译生成每个平台支持的特有代码，如在小程序平台，编译器将 .vue 文件拆分生成 wxml、wxss、js等代码。
运行时：动态处理数据绑定、事件代理、保证 Vue 和平台宿主数据的一致性。

```js
// 获取屏幕宽高
const { windowWidth, windowHeight } = uni.getSystemInfoSync();
```