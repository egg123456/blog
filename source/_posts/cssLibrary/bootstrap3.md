---
title: bootstrap3
date: 2018/5/6
categories:
- cssLibrary
---

>Bootstrap 使用 [Grunt](./grunt) 作为编译系统，并且对外提供了一些方便的方法用于编译整个框架。


# 栅格系统
```css
body {
    margin:0;
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 14px;
    line-height: 1.42857143;
    color: #333;
    background-color: #fff;
}
.container-fluid {
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
}
.container {
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
}
.row {
    margin-right: -15px;
    margin-left: -15px;
}
.col-lg-3 {
    position: relative;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
    float:left;
    width:25%;
}

<!--列偏移  -->
.col-xs-offset-3 {
    margin-left: 25%;
}

.col-md-pull-3 {
    right: 25%;
}

.col-md-push-3 {
    left: 25%;
}

<!--浮动  -->
.pull-right {
    float: right !important;
}

.pull-left {
    float: left !important;
}

<!--清除浮动  -->
.clearfix:before,
.clearfix:after{
    display: table;
    content: " ";
}
.clearfix:after{
    clear:both;
}

<!--hidden/visible  -->
.hidden-md {
    display: none !important;
}
.visible-md {
    display: block !important;
}

```

# 辅助类
```css
<!--text-color  -->
.text-muted {
    color: #777;
}

.text-primary {
    color: #337ab7;
}

.text-success {
    color: #3c763d;
}

.text-info {
    color: #31708f;
}

.text-warning {
    color: #8a6d3b;
}

.text-danger {
    color: #a94442;
}

<!--text-align  -->
.text-left {
    text-align: left;
}

.text-right {
    text-align: right;
}

.text-center {
    text-align: center;
}

.text-justify {
    text-align: justify;
}

.text-nowrap {
    white-space: nowrap;
}

<!--text-case  -->
.text-lowercase {
    text-transform: lowercase;
}

.text-uppercase {
    text-transform: uppercase;
}

.text-capitalize {
    text-transform: capitalize;
}

<!--background-color  -->
.bg-primary {
    color: #fff;
    background-color: #337ab7;
}

.bg-success {
    background-color: #dff0d8;
}

.bg-info {
    background-color: #d9edf7;
}

.bg-warning {
    background-color: #fcf8e3;
}

.bg-danger {
    background-color: #f2dede;
}

<!--show/hide  -->
.hide {
    display: none !important;
}

.show {
    display: block !important;
}

.invisible {
    visibility: hidden;
}

.text-hide {
    font: 0/0 a;
    color: transparent;
    text-shadow: none;
    background-color: transparent;
    border: 0;
}

<!--close-button  -->
.close {
    float: right;
    font-size: 21px;
    font-weight: bold;
    line-height: 1;
    color: #000;
    text-shadow: 0 1px 0 #fff;
    filter: alpha(opacity=20);
    opacity: .2;
}

.close:hover,
.close:focus {
    color: #000;
    text-decoration: none;
    cursor: pointer;
    filter: alpha(opacity=50);
    opacity: .5;
}

<!--三角符号  -->
.caret {
    display: inline-block;
    width: 0;
    height: 0;
    margin-left: 2px;
    vertical-align: middle;
    border-top: 4px dashed;
    border-top: 4px solid \9;
    border-right: 4px solid transparent;
    border-left: 4px solid transparent;
}
```
