---
title: flex布局
date: 2018-05-27 01:11:09
tags: [css,布局,flex]
---

#### flex布局

- flex弹性布局，如何容器都能使用display属性指定为flex布局；

- 概念：采用flex布局的元素，简称“容器”；子容器将自动称为氢气成员（flex item）

- 容器模型如下：水平轴（main axis）的起始点(main start)和结束点(main end)；交叉轴(cross axis)的起始点(cross start)以及结束点(cross end)；

- 注意，设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。

  项目默认沿主轴排列，单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size

  ![flex容器模型](./flex.png)

- 容器的6个属性

  1. flex-direction
  2. flex-wrap
  3. flex-flow
  4. justify-content
  5. align-items
  6. align-content

- 容器属性详解

  1. flex-direction属性决定主轴的方向，也就是排列方向

     ~~~
     row(默认值)：水平方向左为起点
     row-reverse：水平方向右为起点
     column：垂直方向上为起点
     column-reverse：垂直方向下为起点
     ~~~

  2. flex-wrap属性定义一排排满后如何换行

     ~~~
     nowrap(默认)：不换行
     wrap：换行，第一行在上方
     wrap-reverse：换行，第一行在下方
     ~~~

  3. flex-flow属性是flex-direction和flex-wrap的简写形式默认值为 `row nowrap`

     ~~~
     .box{
       flex-flow:<flex-direciton>||<flex-wrap>
     }
     ~~~

  4. justify-content属性定义项目在主轴上的对其方式

     ~~~
     1.flex-start(默认值):左对齐
     2.flex-end：右对齐
     3.center：居中
     4.space-between：两端对齐，项目之间的间隔都相等
     5.space-around：每个项目两侧的间隔相等，因此项目之间的间隔比项目与边框的间隔大一倍
     ~~~

     ![justify-content](justify-content.png)

  5. align-items属性定义项目在交叉轴上如何对齐

     1. flex-start：与交叉轴的起点对齐
     2. flex-end：与交叉轴的终点对齐
     3. center：与交叉轴的中点对齐
     4. baseline：项目的第一行文字的基线对齐
     5. stretch：如果项目未设置高度或设为auto，将占满容器的高度

     ![align-items](align-items.png)

  6. align-content属性定义多根轴线的对齐方式，如果项目只有一根轴线，该属性无效

- 项目的属性

  1. order：定义项目的排列顺序，数值越小，排列越靠前，默认为0
  2. felx-grow属性：定义项目的放大比例饿，默认为0，即如果存在剩余空间，项目也不放大，如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
  3. flex-shrink属性：定义项目的缩小比例，默认为1，级空间如果不足，则将项目缩小；但是如果一个项目的该属性为0，而其他的都为1，则空间不足时，缩小其他的，前者不缩小
  4. flex-basis：属性定义了在分配多余空间之前，项目占据的主轴空间；浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。
  5. flex：该属性是flex-grow，flex-shrink以及flex-basis的缩写，默认为0 1 auto，后两个属性可选（推荐选用该写法）
  6. align-self：属性允许单个项目与其他项目不一样的对齐方式，可以覆盖algin-items的值，默认为auto，表示继承align-items属性，如果没有父元素，则等同于stretch