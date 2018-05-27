---
title: html
date: 2016-11-23 15:45:48
tags: [html,h5]
---

#### 图片与文字组合使用时，如何使图片与文字垂直居中？

- 给图片设置vertical-algin:center;并给文字以及其父元素高度相同的行高

#### 什么是bfc？

- Block Format Context(块级格式化上下文)，它是一个独立渲染区域，只有Block-level box参与，它规定了内部的Block-level box布局规则，并与这个区域外部毫不相干

#### inline-block中的空格部分是什么？

其实是html中的空白字符；li标签不闭合可以解决中间有间距，浏览器会自动补齐闭合li标签；或者给li添加负的边距；

	给父元素font-size：0；也可以清除其中的空白
#### h5新特性

- h5缓存sessionstorage/localstorage/cookie