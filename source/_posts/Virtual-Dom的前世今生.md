---
title: Virtual Dom的前世今生
date: 2018-04-01 20:56:55
tags: [Vue,Dom,性能优化]
---

#### 起源

- 前端开发过程中，对性能产生最大影响的因素莫过于DOM的重排重绘了，为了有效解决DOM更新开销的问题，采用了Virtual DOM的思路，不仅提升了DOM操作的效率，更推动了数据驱动式组件开发的形成与完善

#### Virtual Dom的核心思想

- 事实上，要提高Dom的更改性能，无法就是省去不必要的操作

- 因此：VirtualDOM的主要思想就是模拟DOM的树状结构，在由于交互等原因需要操作DOM时，先在虚拟DOM完成所有操作，然后通过对节点数据进行diff后得到差异结果后，再一次性对DOM进行批量更新操作

  ![虚拟dom](/uploads/virtualDom.png)

  ​

因此，性能上基本决定于Diff效率

##### 懒癌犯了：[掘金上的分享](https://juejin.im/post/5b0638a9f265da0db53bbb6d)