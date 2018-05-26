---
title: css
date: 2018-05-27 00:27:02
tags: [css]
---

#### css 可继承的属性有哪些？

- 常用的：
  1. 字体系列属性：font组合写法，font-weight，font-size，font-style，font-variant，color，text-indent

#### css优先级（权重）

- !important >  id > class > tag  

  important 比 内联优先级高,但内联比 id 要高

#### css选择器，建议没事去逛逛玩W3C

#### css3新特性

- border-radius、box-shadow、text-shadow、gradient

- 变形：transform：rotate | scale | translate |  skew 

- 选择器新增：

  1. p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
  2. p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
  3. p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
  4. p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。
  5. p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。
  6. :enabled  :disabled 控制表单控件的禁用状态。
  7. :checked        单选框或复选框被选中。

- 多背景 rgba

- css3中唯一引入的伪元素::selection

- 媒体查询，多栏布局


#### 必用点之居中

常用：

1. transform,绝对定位上左50%后，translate(-50%,-50%)
2. 绝对定位后，上下左右0，margin:auto
3. 子元素是有宽高或者宽高是被撑开时：父元素display：flex;justify-content:center;align-items:center;