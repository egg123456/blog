---
title: css selector
date: 2018/5/2
categories: 
- base
---

# selector level
type                          | level
------------------------------|-----------------
通配符*                        | 0
标签p、伪元素::before           | 1
类class、伪类:hove 属性attr     | 2
id                             | 3
style                          | 4
!important                     | 5

tips: 原则上高级别的优先级永远大于低级别的，但由于各浏览器的实现不同，有些历览器会出现256个或10000个标签选择器权重大于一个类选择器（了解即可，实际开发中也不可能写几百个层级的样式）

# select symbol
symbol                | desc
----------------------|---------------
空格                  | 后代
大于符号>              | 父子
加号+                 | 后面第一个兄弟
波浪线~               | 后面n个兄弟
竖线                  | 列选择？？

# selector Case Sensitive
css 使用来描述 html渲染的，所以他的大小写敏感与html有关。
在html中，标签、属性名称是不区分大小写的，但属性值是区分的。
所以css中，标签选择器、纯属性选择器(不带属性值)不区分大小写，而id选择器、class选择器、带属性值的属性选择器要区分大小写。

## attribute selector
```html
<!-- 词匹配选择器 -->
[attr~="top right"]
<div attr="top" ></div>
<div attr="right" ></div>
<div attr="top right" ></div>

<!-- 词-拼接选择器 -->
[attr|="word"]
<div attr="word" ></div>
<div attr="word-" ></div>
<div attr="word-a" ></div>
<div attr="word-a-b" ></div>

<!-- 属性正则匹配选择器 -->
[attr^="word"]
<div attr="word" ></div>
<div attr="word-" ></div>
<div attr="words" ></div>
[attr$="a"]
<div attr="a" ></div>
<div attr="word-a" ></div>
<div attr="worda" ></div>
[attr*="a"]
<div attr="a" ></div>
<div attr="-a-" ></div>
<div attr="abc" ></div>
<div attr="word-a" ></div>
```

## Pseudo class selector
type | desc
--------------------|--------------------
:link               | 用于选择所有未被访问的链接。
:visited            | 用于选择所有已被访问的链接。
:hover              | 用于选择鼠标指针悬停在元素上的状态。
:active             | 用于选择正在被用户激活（按下）的元素。
:focus              | 用于选择获得焦点的元素。
:first-child        | 用于选择某个元素的父元素的第一个子元素。
:last-child         | 用于选择某个元素的父元素的最后一个子元素。
:nth-child(n)       | 用于选择父元素的第n个子元素，其中n可以是数字、关键字（如odd, even）或公式。
:nth-last-child(n)  | 类似于:nth-child(n)，但是从最后一个子元素开始计数。
:nth-of-type(n) 和 :nth-last-of-type(n) | 分别选择父元素下特定类型的第n个子元素，从第一个或最后一个开始计数。
:first-of-type 和 :last-of-type 和 :only-of-type 和 :only-child 等等。这些伪类选择器用于更具体地定位元素的类型和数量。例如，:only-of-type选择父元素中仅有的那种类型的子元素。
:not(selector)      | 用于选择不符合给定选择器的元素。例如，排除所有链接。


## select symbol
symbol                | desc
----------------------|---------------
空格                  | 后代
大于符号>              | 父子
加号+                 | 后面第一个兄弟
波浪线~               | 后面n个兄弟
竖线                  | 列选择？？
