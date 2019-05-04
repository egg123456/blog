---
title: Page-optimization
date: 2018/5/2
categories:
- base frontend
---
> 前端是庞大的，是集html、css、js、image、flash等资源组成的。
> 而优化针对不同资源则有不同的方式
> 优化的目的在与两大点“用户体验”“节省带宽等资源”

# 分级优化

## 页面级优化
1. 减少http请求
+ 资源合并与压缩
+ URL scheme
+ lazy load
2. js置后
3. css前置
4. 异步执行inline脚本
    + script defer属性
    + web worker机制

## 代码级优化
1. 减少DOM元素的重复获取
2. 减短作用域链的长度，既避免查找作用域链
3. 避免使用eval，执行效率特别低且不利于js压缩工具的压缩

------------------

# 什么是URL Schemes？
URL，我们都很清楚，http://www.apple.com 就是个 URL，我们也叫它链接或网址；

Schemes，表示的是一个 URL 中的一个位置——最初始的位置，即 ://之前的那段字符。比如 http://www.apple.com 这个网址的 Schemes 是 http。

## 常用URL Scheme
WIFT :  prefs:root=WIFI
蜂窝数据 : prefs:root=MOBILE_DATA_SETTINGS_ID://
电池 : prefs:root=BATTERY_USAGE://
VPN : prefs:root=General&path=VPN://
QQ : mqq://
WeiBo : weibo://
Wechat : wechat://
支付宝 : alipay://
Facebook : fb://
Twitter : twitter://
Google Chrome : googlechrome://
Medium: medium://
Quora:quora://
知乎 : zhihu://
Uber: uber://
简书 : jianshu://
