---
title: Vue双向绑定详解
date: 2018-05-27 20:56:08
tags: [Vue,js]
---

#### 了解前提

- ** 访问器属性**、**DocumentFragment**、**订阅/发布模式（subscribe&publish）**

#### 访问器属性

1. [[Configurable]]:定义属性是否使用obj.delete删除属性，可否修改
2. [[Enumerable]]：定义能否用for in 遍历，是否可枚举
3. [[Get]]：在读取属性时，调用的函数，默认为undefined
4. [[Set]]：在写入属性时，调用的函数，默认为undefined

```
 var obj = { };
 Object.defineProperty(obj, "hello", {
	get: function () {return sth},
	set: function (val) {/* do sth */}
})
```

-  get 和 set 方法内部的 this 都指向 obj，这意味着 get 和 set 函数可以操作对象内部的值。另外，访问器属性的会"覆盖"同名的普通属性，因为访问器属性会被优先访问，与其同名的普通属性则会被忽略。

#### 极简的双线绑定实现

~~~
<body>
    <input type="text" name="" id="a">
    <span id="d"></span>
</body>
<script>
var obj={}
Object.defineProperty(obj,'hello',{
    set :function(newVal){
        document.getElementById('a').value=newVal
        document.getElementById('b').innerHTML=newVal
    }
})

document.addEventListener('keyup',function (e){
    obj.hello=e.target.value
})
</script>
~~~

#### [歇会儿](http://www.cnblogs.com/kidney/p/6052935.html?utm_source=gold_browser_extension)