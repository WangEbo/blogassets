---
title: ES6
date: 2018-03-15 19:57:49
tags: [js,ES6]
---

#### let && const

1. let

   - let 与 var 的声明用法相同，但是多了一个临时死区(Temporal Distonrtion Zone)的概念

     ```
      console.log(a)		// -> undefined
      var a=1
      console.log(b)		// -> Uncaught ReferenceError: b is not defined
      let b=2
     ```

   - 可以发现声明时使用let时，在声明前打印会报错，事实上，这解决了JS一些奇怪的问题，并且，let会生成一个块级作用域，作用域之外不能访问该变量

     ```
     {
         let a=1
         var b=2
         console.log(a)	// ->1
         console.log(b)	// ->2
      }
      console.log(b)	// ->Uncaught ReferenceError: b is not defined
      console.log(a)	// ->1
      // ->可以发现let声明的变量是有'{}'块级作用域的
      // ->这也是为什么使用let可以解决for循环中存在任务队列时常常会发生我们预想之外的结果
     for(var i=0;i<5;i++){
         setTimeout(function(){
             console.log(i)
         },200)
     }
     //由于js单线程 任务队列 +事件队列的执行机制，主线程会将延时打印任务放入任务队列中，而主线程执行完后，i已
     //经是5了
     // -> 5 5 5 5 5 
     for(let i=0;i<5;i++){
         setTimeout(function(){
             console.log(i)
         },200)
     }
     // -> 0 1 2 3 4
     //由于产生了块级作用域，即便是任务队列中的定时打印，访问到的i也是其作用域内的i ，分别为0 1 2 3 4
     ```

2. const

   - const 与 let 基本相似，只是用const声明必须赋值，并且不得修改绑定（修改指针）

     ```
     const a=1
     a=2		// -> Uncaught TypeError: Assignment to constant variable
     const b={a:1}
     b.a=2   	//正常执行
     ```

   - 另外：有办法使绑定严格不得更改

     ```
     const b = Object.freeze({a: 1})
     b.a = 2 // 没有报错，但是 b.a 没有被改
     ```

#### 字符串相关

- 新增函数 `includes() endsWith() startsWith() `

  ```
  let string = 'startend'
  string.includes('a') // -> true 是否包含
  string.endsWith('end') // -> true 是否由 end 结尾
  string.startsWith('start') // -> true 是否由 start 开头
  ```

- 模板字符串

  1. 模板字符串中可换行

     ```
     let s=`start
     换行
     end`
     console.log(s) 
     //
     //start
     //换行
     //end
     ```

  2. 占位符

     ```
     let s = 'string'
     let message = `start${s}`  // -> startstring
     ```

#### 解构赋值

- 数组的结构赋值

  ```
  //解构
  let [a,b,c]=[1,2,3]
  console.log(a,b,c)	//1,2,3

  //设置默认值
  let [a=0,b,c]=[,2,3]
  console.log(a,b,c)	//0,2,3

  //没有设置的值为undefined
  let [a=0,b,c]=[4,5,]
  console.log(a,b,c)	//4,5,undefined
  ```

- 对象的解构赋值

  ```
  let {name,age}={name:'zxx',age:18}
  console.log(name,age)	//zxx 18

  //顺序无关
  let {name:tag,age}={age:18,name:'zxx'}
  console.log(name,age)	//zxx 18

  //设置属性别名  一旦设置了别名，原来的名字就无效了
  let {name:tag.age} ={age:18,name:'zxx'}
  console.log(name,age) //ReFerenceError：name is not defined
  console.log(tag,age)	//zxx 18

  //解构赋值时设置默认值
  let {name;tag='zxx',age}={age:18}
  console.log(tag,age)	//zxx 18
  ```

#### 对象相关与扩展运算符

- 新增方法Same-value equality 同值相等，真·严格相等----Object.is()

  ```
     Object.is(NaN, NaN) // ->true
     // 结果基本于 === 相似，除了 NaN 和 +0 -0
     Object.is(+0, -0) // -> false
     let o = {a: 1}
     let a = Object.assign({}, o) // -> {a: 1}
     // 第一个参数为目标参数，后面的参数是不定的，参数属性名如果有重复，后面的会覆盖之前的
  ```

- 对象属性相关

  ```
    let a = 1
    // 当 key 和 value 名字相同时可以简写
    let b = { a }
    // 对象中的方法也可以简写
    let a = {
    init() {}
    }
    // 对象属性名也可以计算 
    let name = 'name'
    b[name + '1'] = 2 // === b['name1'] = 2
  ```

#### 函数相关

- 参数默认值

  ```
  function fn(a = 1, b = 2) {}
  // 默认值也可以通过调用函数获得，注意必须调用函数
  function fn1(a = 1, b = fn()) {}
  ```

- 参数的解构赋值

  ```
  function f({name,age}){
    console.log(name,age)
  }
  f()	//typeError:Cannot match against 'undefined' or 'null'
  f({})	//undefined,undefined
  f({name:'zxx',age:18})	//zxx 18
  ```

- 扩展运算符

  ```
  let array = [1, 2, 3]
  console.log(...array)	// -> 1 2 3
  // 该语法可以解决之前很多地方只能传入单个参数，只能使用 apply 解决的问题
  Array.prototype.unshift.apply([4, 5], array) // -> [1, 2, 3, 4, 5]
  // 现在可以直接这样写
  [4, 5].unshift(...array)
  // 展开运算不受不定参数的条件限制，可以一起用
  ```

- rest 剩余参数

  ```
  funtion f(a,...args){
    console.log(a,args)
  }
  f(1,2,3)	//1 [2,3]
  ```

- 箭头函数

  ```
  // 最简单的写法，只有一个参数，单行表达式
  value => value
  // 多个参数需要使用小括号包裹
  (v1, v2) => v2 + v1
  // 没有参数需要使用小括号包裹
  () => "balabala"
  // 多行表达式需要大括号包裹
  (v1, v2) => {
  	let v3= v1 + v2
      return v3
  }
  ```

#### Set和Map

- Set： 是新增的无重复的有序集合，多用于集合去重或者判断集合中是否含有某个元素。

  ~~~
  // 创建
  let set = new Set()
  // 添加元素
  set.add(1)
  set.add('1')
  // 重复的元素不会被添加
  set.add(1)
  // 判断是否包含元素
  set.has(1) // -> true
  // 判断长度
  set.size() // -> 2
  // 删除某个元素
  set.delete()
  // 移除所有元素
  set.clear()
  ~~~

- Map ：是新增的有序键值对列表，键值可以是任何类型。

  ~~~
  // 创建
  let map = new Map()
  // 设置键值对
  map.set('year', "2017")
  map.set({}, 'obj')
  // 取值
  map.get('year') // -> '2017'
  // 判断是否有该键值
  map.has('year') // -> true
  // 获得长度
  map.size() // -> 2
  // 删除某个键值
  map.delete('year')
  // 移除所有键值
  map.clear()
  ~~~

#### 类与继承

- JS 中的类不是其他语言中的类，只是个语法糖，写法如下。

  ~~~
  class Person {
  // 构造函数
      constructor() {
          this.name = name
      }
      sayName() {
          console.log(this.name)
      }
  }
  let p = new Person('name')
  p.sayName() // -> 'name'

  // class 就是以下代码的语法糖
  // 对应 constructor
  function Person(name) {
      this.name = name
  }
  // 对应 sayName
  Person.prototype.sayName = function() {
      console.log(this.name)
  }
  ~~~

  - 类声明相比之前的写法有以下几点优点
    1. 类声明和 let 声明一样，有临时死区
    2. 类声明中的代码全部运行在严格模式下
    3. 必须使用 new 调用


- 在 ES6 之前写继承很麻烦，既然有个类，那么必然也可以继承类了

  ```
  class Person {
  // 构造函数
  constructor() {
      this.name = name
  }
  sayName() {
      console.log(this.name)
  }
  }
  // extends 代表继承自Person
  class Student extends Person {
  constructor(name, age) {
  // super 的注意事项之前有说过
      super(name)
      // 必须在 super 之后调用 this
      this.age = age
  }
  sayName() {
  // 如果像使用父类的方法就使用这个方法使用
  // 不像使用的话就不写 super，会覆盖掉父类的方法
      super.sayName(this.name)
      console.log(this.age)
  }
  }
  ```

#### Promise

- Promise	:一个构造函数，在 new操作符创建实例使，即创建了一个异步操作

- Promise有三个状态

  1. pending，等待状态，也就是既不是 resolve 也不是 reject 状态
  2. fulfilled，resolve 以后进入这个状态
  3. reject，reject 以后进入这个状态

- 由于异步操作后我们只能拿到res又或err，因此开发人员在创建Promise实例时，就要使用`Promise.prototype`上的.then方法为它定义resolve和reject回调函数·，用法：

  ```
       // 1. 创建promise实例,在实例中执行异步操作(比如发送网络请求)
       // 2. 异步操作成功时,调用reslove函数传递数据
       // 3. 异步操作失败时,调用reject函数传递错误信息
       const promise = new Promise(function(resolve, reject) {
           // 异步操作
           // ... 
           if (/* 异步操作成功 */){
               resolve(value);
           } else {
               reject(error);
           }
       });
      
       // 4. 使用promise实例then方法接收reslove或reject返回的数据
       promise.then(function(value) {
           // 此处数据即为reslove回来的数据
             // success
       }, function(error) {
           // 此处数据即为reject回来的数据
           // failure
       });
  ```

- Promise解决回调地狱

   **原理：链式编程**

  ```
  function fetch(url){
      return new Promise(function(reslove,reject){
          axios.get(url).then(function(res){
              if(res.status == 1){
                  reslove(res.data)
              }else{
                  reject(res.error)
              }
          })
      })
  }

  //then方法内部返回的promise实例reslove或reject出来的对象会在下一个then方法内部得到
  fetch('A').then(function(res){
      // A 请求正常
      return fetch('B')    // 这里返回一个新的promise实例,在后面的then中可以得到该实例reslove或reject出来的对象
  }).then(function(res){
      // B 请求正常
      return fetch('C')
  }).then(function(res){
      // C 请求正常
      // 请求完毕
  })
  ```

- Promise中捕获异常

  1. 可以在每一个.then(resolve,reject)中定义一个reject `失败后的处理函数`
  2. Promise中也提供了catch方法，`Promise.then().catch(err=>{console.log(err.message)})`可以在每一个异步操作出错时 抛出异常

- Promise处理多个请同时发送，而需要数据合并渲染

   Promise的 `all`方法可将多个Promise实例包装成一个新的Promise实例

  ```
  function fetch(url){
          return new Promise(function(reslove,reject){
              axios.get(url).then(function(res){
                  if(res.status == 1){
                      reslove(res.data)
                  }else{
                      reject(res.error)
                  }
              })
          })
  }

  const p1 = fetch('A')
  const p2 = fetch('B')
  const p3 = fetch('C')
  const p = Promise.all([p1, p2, p3]);
  p.then(function(res){
      // res是一个数组,存放着p1,p2,p3的返回值
  })
  ```

#### 模块化

- 模块化是指将不同功能的js代码分开管理,常用于功能与数据封装

- 其好处在于代码管理方便，便于维护，适合团队开发

  ```
  // example.js 文件下
  // export 可以导出任何变量，函数或者类
  export var age = 14
  export function sum(n1, n2) {
      return n1 + n2
  }
  export class Person {
      constructor(age) {
          this.age = age
      }
  }
  // 别的 JS 文件中导入
  // 如果想导入整个模块并且自己命名，就可以这样使用
  // import 后面代表模块名，from 后面代表要导入的文件地址
  import * as Example from './example'
  console.log(Example.age) // -> 14
  // 当然你也可以只使用模块中的一个功能
  // 这里使用了对象解构的方法拿到需要的功能，注意这里名字必须相同，否则使用会报错
  import { age, sum } from './example'
  console.log(age) // -> 14
  console.log(sum(1, 2)) // -> 3
  // 现在我只想导出一个功能，并且外部可以随便命名该如何做呢？
  // default 一个文件中只能使用一次
  export default var age = 14
  // MyAge 可以随便自己喜欢命名
  import MyAge from './example'
  console.log(MyAge) // -> 14
  ```

  ​