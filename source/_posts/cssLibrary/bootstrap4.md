---
title: bootstrap4
date: 2018/5/6
categories:
- css
---
> Bootstrap 3 和 Bootstrap 4 最大的区别在于 Bootstrap 4 现在使用 flexbox（弹性盒子） 而不是浮动。 Flexbox 的一大优势是，没有指定宽度的网格列将自动设置为等宽与等高列。注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

# 网格系统
```css
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  text-align: left;
  background-color: #fff;
}
.container {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
.row {
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}
/** 五个尺寸类  
    col-* < 576         auto
    col-sm-* >= 576     540
    col-md-* >= 768     720
    col-lg-* >= 992     960
    col-xl-* >= 1200    1140
*/
.col-x-x {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
}
.col-x-auto {
  -ms-flex: 0 0 auto;
  flex: 0 0 auto;
  width: auto;
  max-width: none;
}
.col-3 {
  -ms-flex: 0 0 25%;
  flex: 0 0 25%;  /*flex: flex-grow flex-shrink flex-basis;*/
  max-width: 25%;
}
/* 列偏移 */
.offset-3 {
  margin-left: 25%;
} 
```

# 可见
```css
.visible {
  visibility: visible !important;
}

.invisible {
  visibility: hidden !important;
}

[hidden] {              
  display: none !important;
}
/* hidden 属性是 HTML5 中的新属性(div[Attributes Style] {display: none;}) */
```