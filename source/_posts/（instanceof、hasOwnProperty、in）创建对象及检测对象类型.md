---
title: （instanceof、hasOwnProperty、in）创建对象及检测对象类型
date: 2018-05-27 00:48:28
tags: [js,Object,es5]
---

- 再将要涉及到面向对象开发之前，我们可能需要创建许多新对象，也许他们有许多共同点，那么这些创建对象的模式是如何演变的呢
- 先了解instanceof  `person1 instanceof Person ` 操作符，它用来检测对象类型（实例对象是否是某个‘类‘的实例）
- hasOwnProperty() `obj.hasOwnProperty('atr_name')`用来检测对象是否自身真正有某个属性，而不是通过原型链访问原型对象的
- in  `"atr_name"in obj` 操作符在单独使用时，只用来判断对象是够可以读取某一个属性，不论来之自身或是原型链上的原型对象上，能则返回true，反之，返回false
  1. 工厂模式

     ~~~
         function createPerson(name,age,job){
             var o=new Object()
             o.name=name
             o.age=age
             o.job=job
             o.sayName=function(){
                 console.log(this.name);
             }
             return o
         }
         var person1=createPerson('Nicolas',23,'webber')
         var person2=createPerson('rose',22,'ui')
         
         达到了需求
         缺点：
         	- 无法检测对象的类型，因为都是Object
         	- 每次创建一个新对象时，就保存了一个say方法，函数复用没有得到利用（因为有更好的解决办法）
     ~~~

  2. 构造函数模式

     ~~~
      	function Person(name,age,job){
             this.name=name
             this.age=age
             this.job=job
             this.sayName=function(){
                 console.log(this.name);
             }
         }
         var person1=Object('Nicolas',23,'webber')
         var person2=Object('rose',22,'ui')
         
         优点：
         	- 可以通过constructor或instanceof来检测类型
         	alert(person1.constructor,person1 instanceof Object,person1 instanceof Person)
         	将输入true true true，
         	构造函数模式可以为实例对象添加一个特定类型标识，这正是它优于工厂模式的所在
         缺点：
         	say方法重复再内存中创建
     ~~~

  3. 原型模式

     ~~~
         //构造函数来存放简单类型
         function Person(){}
     	Person.prototype.name='Nicolas'
         Person.prototype.sayName=function(){
                 console.log(this.name);
         }
         Person.prototype.friends=['小明']
         var person1=new Person()
         var person2=Object()
         
         优点：
           	如此，由于原型的关系，实例对象可以共同访问sayName方法，而this对象又很好的解决了标识符name指		 向不同的问题
         缺点：
         	无法传参
         	如果出现引用问题(下面继承也会讲到)，如：`person1.friends.push('小红')`
         	在执行打印person2.friends时，将会输出['小明','小红'],而这不是我们所希望的结果
     ~~~

  4. 组合使用构造函数模式和原型模式

     ~~~
      //构造函数来存放简单类型
         function Person(name,age,job){
             this.name=name
             this.age=age
             this.job=job
             //将可能要变化的引用类型放入构造函数中
             this.friends=['小明']
         }
         Person.prototype.sayName=fucntion(){
             	console.log(this.name);
         }
         var person1=Object('Nicolas',23,'webber')
         var person2=Object('rose',22,'ui')
         
         //这是一种广泛认可的开发模式
         注意：
         	通过字面量方式赋值给Person.prototype会导致constructor需要重新手动设置，并且会切断最初原型对象与实例对象之间的联系
     ~~~

  5. 动态原型模式

     ~~~
     实际上和（组合构造器和原型模式）差不多
     不过是
      function Person(name,age,job){
             this.name=name
             this.age=age
             this.job=job
             //将可能要变化的引用类型放入构造函数中
             this.friends=['小明']
             //不过只是在构造函数将所需的代码全包含了，而且原型对象的方法也只会在初次使用构造函数的时候添			加一次,当然只需要检测一个属性或者方法即可
             if(this.sayName != 'function'){
              	Person.prototype.sayName=function(){
                  	alert(this.name)
              	}
             }
       }
       
      很完美了，不过.....QAQ，还是不能通过字面重写原型对象
     ~~~

  6. 寄生构造函数模式

     ~~~
      function Person(name,age,job){
             var o=new Object()
             o.name=name
             o.sayName=function(){
                 console.log(this.name);
             }
             return o
         }
         var p1=new Person()
          
          它与工厂模式别没有多大区别，只不过，他可以在特殊情况下为对象创建构造函数，如我们需要一个包含特殊方法的Array构造函数，
          function SpecialArray(){
            var values=new Array()
            values.push.apply(values,arguments)
            //这里不能直接 values.push(arguments)吗
            values.toPipedString=function(){
              return this.join('|')
            }
            return values
          }
          var colors=new SpecialArray('red','blue','green)
          alert(colors.toPipedString)	//'red|blue|green'
          
          缺点：
          	它依然不能解决类型判断问题，instanceof无法解决	/？why
     ~~~

     ​

  7. 稳妥构造函数模式

     ~~~

     ~~~

     ​