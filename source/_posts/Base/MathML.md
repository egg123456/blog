---
title: Svg
date: 2018/5/2
categories:
- base
---
> 数学标记语言（Mathematical Markup Language）或 MathML 是用于在网页中编写数学公式的标记语言，其支持分数、上下标、根号、矩阵、积分、级数等。尽管它最初被设计为独立的 XML 语言，但 MathML 通常嵌入在 HTML 文档中，并可视为 HTML 的扩展。

### getting start
```XML
<!-- math公式开始，display="block"表示公示单独一行剧中显示，不与其他文本在一行 -->
<math display="block">
  <!-- mfrac 表示包裹的部分是一个分式，其内第一块为分子，第二块为分母 -->
  <mfrac>
    <!-- mrow 通用容器，使其包裹的部分作为一个整块 -->
    <mrow>
      <!-- msup 表示包裹的部分是个指数，其内第一块为底数，第二块为指数 -->
      <msup>
        <mrow>
          <!--  mi 表示字母-->
          <mi> x </mi>
        </mrow>
        <mrow>
          <!--  mi 表示数学数字-->
          <mn> 2 </mn>
        </mrow>
      </msup>
      <!--  mo 表示数学操作符号-->
      <mo> + </mo>
      <msup>
        <mrow>
          <mi> y </mi>
        </mrow>
        <mrow>
          <mn> 2 </mn>
        </mrow>
      </msup>
    </mrow>
    <mrow>
      <mn> 2 </mn>
    </mrow>
  </mfrac>
  <mo> + </mo>
  <msubsup>
    <mtext>log</mtext>
    <mtext>e</mtext>
    <mtext>a</mtext>
  </msubsup>
  <mo> = </mo>
  <mn> 1 </mn>
</math>
```