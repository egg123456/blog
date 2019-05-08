---
title: Svg
date: 2018/5/2
categories:
- base frontend
---
> SVG 是使用 XML 来描述二维图形和绘图程序的语言

```xml
<?xml version="1.0" standalone="no"?>   
<!-- xml声明， standalone 属性！该属性规定此 SVG 文件是否是“独立的” -->
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<!-- 引用了这个外部的 SVG DTD -->
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">
<!-- SVG 代码以 <svg> 元素开始，包括开启标签 <svg> 和关闭标签 </svg> 。这是根元素。width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。 -->
<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>
SVG 的 <circle> 用来创建一个圆。cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。r 属性定义圆的半径。
stroke 和 stroke-width 属性控制如何显示形状的轮廓。我们把圆的轮廓设置为 2px 宽，黑边框。
fill 属性设置形状内的颜色。我们把填充颜色设置为红色。
</svg>
```

[link](http://www.ruanyifeng.com/blog/2018/08/svg.html)