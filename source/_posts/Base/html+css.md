---
title: html+css
date: 2018/5/2
categories: 
- base
---
# html标签
+ 容器级标签：其内部可放置任何标签、包括自身
    + div\ul\ol\dl\dd\dt\li\td\H*……
+ 文本级标签：其内部只能放文字、图片、表单元素和其他文本级标签
    + p\a\span\b\u\i\s\strong\ins\del

# css元素
+ 块级元素：display：blok；（p属于块级元素确是文本级标签）
+ 行内元素：display：inline；（a）
+ 可变元素：display：inline-blok；（button、input……）

> css主要解决样式问题，html标签解决内嵌问题，二者相互联系

# 在标准文档流里面，块级元素具有以下特点：
+ ①总是在新行上开始，占据一整行；
+ ②高度，行高以及外边距和内边距都可控制；
+ ③宽带始终是与浏览器宽度一样，与内容无关；
+ ④它可以容纳内联元素和其他块元素。
# 行内元素的特点：
+ ①和其他元素都在一行上；
+ ②高，行高及外边距和内边距部分可改变；
+ ③宽度只与内容有关；
+ ④行内元素只能容纳文本或者其他行内元素。
+ 不可以设置宽高，其宽度随着内容增加，高度随字体大小而改变，内联元素可以设置外边界，但是外边界不对上下起作用，只能对左右起作用，也可以设置内边界，但是内边界在ie6中不对上下起作用，只能对左右起作用


# BFC
## BFC概念
Block Formatting Contexts (BFC，块级格式化上下文)，就是 一个块级元素 的渲染显示规则。通俗一点讲，可以把 BFC 理解为一个封闭的大箱子，，容器里面的子元素不会影响到外面的元素，反之也如此。

## BFC的布局规则
1. 内部的盒子会在垂直方向，一个个地放置； 
2. BFC是页面上的一个隔离的独立容器； 
3. 属于同一个BFC的 两个相邻Box的上下margin会发生重叠 ； 
4. 计算BFC的高度时，浮动元素也参与计算 
5. 每个元素的左边，与包含的盒子的左边相接触，即使存在浮动也是如此； 
6. BFC的区域不会与float重叠；

## 如何触发 BFC呢？只要元素满足下面任一条件即可触发 BFC 特性：
1. 浮动元素：float 不为none的属性值；
2. 绝对定位元素：position (absolute、fixed)
3. display为： inline-block、table-cells、flex 等非默认块级显示模式的元素
4. overflow 除了visible以外的值 (hidden、auto、scroll)

## BFC解决什么问题
1. 外边距合并（即margin塌陷）
2. 包裹其内浮动元素，计算BFC的高度时，浮动元素也参与计算
3. BFC可以阻止元素被浮动元素覆盖（可以用来实现两列/三列的自适应布局）


# em and rem
em 相对于父级元素的字体大小，如父元素的font-size: 16px; 子元素宽度设为 2em，则子元素显示宽度为 2 * 16 = 32px
rem 相对于根元素(html)的字体大小，如html元素的font-size: 16px; 某元素宽度设为 2rem，则子元素显示宽度为 2 * 16 = 32px


# 响应式文字
1. 媒体查询
```css
html {
  /* 默认字体尺寸 16px */
  font-size: 16px;
}
/* 屏幕大于2000px 时, 根元素字体大小设为 32px */
@media screen and (min-width: 2000px) {
  html {
    font-size: 32px;
  }
}
```
缺点：屏幕大小种类繁多，需要写很多的媒体查询且体验不够丝滑。

2. 视口法
```css
h1 {
  /* 字体大小为视窗宽度的 6%，跟随视窗宽度变化 */
  font-size: 6vw;
}
```
缺点：当屏幕大/小到一定程度时，字体将会无限大/小。最好的体验应是屏幕大/小大一定屏幕时字体大小将不再变化。

3. clamp 方法
```css
h1 {
  /* 最小字体大小为2rem, 最大为2.75rem。其他随最小、最大值确定的线段取值 */
  /* 1.799rem 为直线的截距，0.98为斜率。取值根据视窗宽度vw变化 */
  font-size: clamp(2rem, 1.799rem + 0.98vw, 2.75rem);
}
```
缺点：网页放大/缩小时，实际导致的是视口大小改变。放大页面等于缩小视窗口。字体可能反而变小了


# 响应式图片
1. 等比缩放
```css
img {
  width: 100%;
  height: auto;
}
```

2. 缩放到自身原始宽度时不缩放
```css
img {
    max-width: 100%;
    height: auto;
}
```

3. 不同设备尺寸显示不同图片
```css
/* 媒体查询 */
/* For width smaller than 400px: */
body {
    background-image: url('img_smallflower.jpg');
}

/* For width 400px and larger: */
@media only screen and (min-width: 400px) {
    body {
        background-image: url('img_flowers.jpg');
    }
}

/* html 5 picture */
<picture>
  <source srcset="img_smallflower.jpg" media="(max-width: 400px)">
  <source srcset="img_flowers.jpg">
  <img src="img_flowers.jpg" alt="Flowers">
</picture>
```

4. 背景图铺满
```css
div {
    width: 100%;
    height: 400px;
    background-image: url('img_flowers.jpg');
    /* 宽高都变为容器宽高 */
    background-size: 100% 100%;
    border: 1px solid red;
}
```