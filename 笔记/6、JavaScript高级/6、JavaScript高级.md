# JavaScript高级
## 1、基础总结深入
### 1.1 数据类型的分类和判断
* 基本(值)类型
  * Number ---  任意数值--- typeof
  * String ---  任意字符串--- typeof
  * Boolean ---  true/false ---  typeof
  * undefined --- undefined ----- typeof/===(代表没有赋值)
  * null ---  null ---  ===(代表赋值了, 只是值为null)
* 对象(引用)类型
  * Object ---  任意对象--- typeof/instanceof
  * Array --- 特别的对象类型(下标/内部数据有序) --- instanceof
  * Function --- 别的对象类型(可执行) --- typeof

* 判断：

  * typeof：
    * 可以区别: 数值, 字符串, 布尔值, undefined, function
    * **不能区别: null与对象, 一般对象与数组**
    * **typeof: 返回的是数据类型的字符串表达形式**

  * instanceof
    * **专门用来判断对象数据的类型: Object, Array与Function**
  * ===
    * **可以判断: undefined和null**

* 代码：

~~~html
  <script type="text/javascript">
    //1. 基本类型
    var a
    console.log(a, typeof a, a === undefined) // undefined 'undefined' true
    console.log(a === typeof a) // false  undefined ≠ 'undefined'
	//typeof返回字符串类型
    a = 3
    console.log(typeof a === 'number') // true
    a = 'atguigu'
    console.log(typeof a === 'string') // true
    a = true
    console.log(typeof a === 'boolean') // true

    a = null
    console.log(a === null) // true
    console.log(typeof a) // 'object'

    console.log('--------------------------------')

    //2. 对象类型
    var b1 = {
      b2: [2, 'abc', console.log],//number string function  
      b3: function () {
        console.log('b3()')
      }
    }
    console.log(b1 instanceof Object, typeof b1) // true 'object'
    console.log(b1.b2 instanceof Array, typeof b1.b2) // true 'object'
    console.log(b1.b3 instanceof Function, typeof b1.b3) // true 'function'

    console.log(typeof b1.b2[2]) // 'function'
    console.log(b1.b2[2]('abc')) // 内'abc' 外undefined
  </script>
~~~



### 1.2 数据,变量, 内存的理解

* 数据
  * 在内存中可读的, 可传递的保存了特定信息的'东东'
  * 一切皆数据, 函数也是数据
  * 在内存中的所有操作的目标: 数据
* 变量
  * 在程序运行过程中它的值是允许改变的量
  * 一个变量对应一块小内存, 它的值保存在此内存中  
* 内存
  * 内存条通电后产生的存储空间(临时的)
  * 一块内存包含2个方面的数据
    * 内部存储的数据
    * 地址值数据
  * 内存空间的分类
    * 栈空间: 全局变量和局部变量
    * 堆空间: 对象 
* 内存,数据, 变量三者之间的关系
  * 内存是容器, 用来存储不同数据
  * 变量是内存的标识, 通过变量我们可以操作(读/写)内存中的数据  
  
*  var a = xxx, a内存中到底保存的是什么?
  * xxx是一个基本数据，保存的就是这个数据
  * xxx是一个对象，保存的是对象的地址值
  * xxx是一个变量，保存的是xxx的内容



### 1.3 对象的理解和使用

* 对象
  * 多个数据(属性)的集合
  * 用来保存多个数据(属性)的容器
* 属性
  * 属性名 : 字符串(标识)
  * 属性值 : 任意类型
* 属性的分类:
  * 一般 : 属性值不是function  描述对象的状态
  * 方法 : 属性值为function的属性  描述对象的行为
* 特别的对象
  * 数组: 属性名是0,1,2,3之类的索引
  * 函数: 可以执行的
* 如何操作内部属性(方法)
  * **.属性名: 编码简单, 但有时不能用**
  * **[ '属性名']: 编码麻烦, 但通用**(属性名不是合法的标识名、属性名不确定)
  

~~~html
  <script type="text/javascript">
    // 创建对象
    var p = {}

    /*情形一: 属性名不是合法的标识名*/
    /*需求: 添加一个属性: content-type: text/json */
    //  p.content-type = 'text/json' //不正确
    p['content-type'] = 'text/json'

    /*情形二: 属性名不确定*/
    var prop = 'xxx'//变量 不确定
    var value = 123
    // p.prop = value  //不正确
    p[prop] = value
    console.log(p['content-type'], p[prop])
  </script>
~~~



### 1.4 函数的理解和使用

* 函数
  * 用来实现特定功能的, n条语句的封装体
  * 只有函数类型的数据是可以执行的, 其它的都不可以

~~~html
  <script type="text/javascript">
    function f1() { // 函数声明
      console.log('f1()')
    }
    var f2 = function () { // 表达式
      console.log('f2()')
    }
    f1()
    f2()
  </script>
~~~

* 为什么要用函数?
  * 提高复用性
  * 便于阅读交流
  
* 函数也是对象
  * instanceof Object===true
  * 函数有属性: prototype
  * 函数有方法: call()/apply()
  * 可以添加新的属性/方法
  
* 函数的3种不同角色
  * **一般函数 : 直接调用**
  * **构造函数 : 通过new调用**
  * **对象 : 通过.调用内部的属性/方法**



**函数中的this**

  * **显式指定谁: obj.xxx()**
  * **通过call/apply指定谁调用: xxx.call(obj)**
  * **不指定谁调用: xxx()  : window**
  * **回调函数: 看背后是通过谁来调用的: window/其它**

~~~html
<script type="text/javascript">
    function Person(color) {
      console.log(this)
      this.color = color;
      this.getColor = function () {
        console.log(this)
        return this.color;
      };
      this.setColor = function (color) {
        console.log(this)
        this.color = color;
      };
    }
    Person("red"); //this是 windows
    var p = new Person("yello"); //this是 p
    p.getColor(); //this是 p 
    var obj = {};
    p.setColor.call(obj, "black"); //this是 obj
    var test = p.setColor;
    test(); //this是 windows
    function fun1() {
      function fun2() {
        console.log(this);
      }
      fun2(); //this是 windows
    }
    fun1();
  </script>
~~~



**匿名函数自调用**

```JavaScript
  (function(w, obj){
    //实现代码
  })(window, obj)
  
  
  (function (i) {
    var a = 4
    function fn() {
      console.log('fn ', i+a)//fn 7
    }
    fn()
  })(3)
  
```
* 专业术语为: **IIFE (Immediately Invoked Function Expression) 立即调用函数表达式**	



**回调函数**

  * 什么函数才是回调函数?
    * 你定义的
    * 你没有调用
    * 但它最终执行了(在一定条件下或某个时刻)
  * 常用的回调函数
    * dom事件回调函数
    * 定时器回调函数
    * ajax请求回调函数
    * 生命周期回调函数

~~~html
 <script type="text/javascript">
    //1. DOM事件函数
    var btn = document.getElementById('btn')
    btn.onclick = function () {
      alert(this.innerHTML)
    }
    //2. 定时器函数
    setInterval(function () {
      alert('到点啦!')
    }, 2000)
  </script>
~~~



## 2、函数高级

### 2.1 原型与原型链
* 所有函数都有一个特别的属性:
  * `prototype` : 显式原型属性

~~~JavaScript
  // 每个函数都有一个prototype属性, 它默认指向一个对象(即称为: 原型对象)
  function fn() {

  }
  console.log(fn.prototype, typeof fn.prototype)//object 'object'
 
// 原型对象中有一个属性constructor, 它指向函数对象
  console.log(fn.prototype.constructor===fn)//true
 
  // 2. 给原型对象添加属性(一般都是方法)
  function F() {

  }
  F.prototype.age = 12 //添加属性
  F.prototype.setAge = function (age) { // 添加方法
    this.age = age
  }
  // 创建函数的实例对象
  var f = new F()
  console.log(f.age)//12
  f.setAge(23)
  console.log(f.age)//23
~~~

* 所有实例对象都有一个特别的属性:
  * `__proto__` : 隐式原型属性

~~~javascript
  //对象的隐式原型的值为其对应构造函数的显式原型的值 
  function Fn() {

  }
  var fn = new Fn()
  console.log(Fn.prototype, fn.__proto__)//object  object
  console.log(Fn.prototype===fn.__proto__)//true
~~~

* 显式原型与隐式原型的关系
  * 函数的prototype: 定义函数时被自动赋值, 值默认为{}, 即用为原型对象
  * 实例对象的__ proto__: 在创建实例对象时被自动添加, 并赋值为构造函数的prototype值
  * 原型对象即为当前实例对象的父对象

![在这里插入图片描述](https://img-blog.csdnimg.cn/216be40352e64c1f802c41e380756cae.png#pic_center)


* 原型链（隐式原型链）
  * 所有的实例对象都有__ proto__属性, 它指向的就是原型对象
  * 这样**通过__ proto__属性就形成了一个链的结构---->原型链**
  * 当**查找对象内部的属性/方法时**, js引擎自动沿着这个原型链查找
  * 当给**对象属性赋值时不会使用原型链**, 而只是在当前对象中进行操作

![在这里插入图片描述](https://img-blog.csdnimg.cn/6b74451bda0540daa123d1811e75019a.png#pic_center)


* **函数的显示原型指向的对象默认是空object实例对象（但object除外）**

~~~JavaScript
console.log(Object.prototype instanceof Object)//false
~~~

* **所有函数都是Function的实例(包含Function)**

~~~JavaScript
console.log(Function.__proto__===Function.prototype)//false
~~~

* **Object的原型对象是原型链的尽头**



* instanceof
  * 表达式: A instanceof B
  * 如果B函数的显式原型对象在A对象的原型链上, 返回true, 否则返回false

![在这里插入图片描述](https://img-blog.csdnimg.cn/b313fa0e35a4421a94e95dfb893282a3.png#pic_center)


~~~JavaScript
  function Foo() {  }
  var f1 = new Foo();
  console.log(f1 instanceof Foo);//true
  console.log(f1 instanceof Object);//true
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/98dbeec5144540a4a7c726b45a0496d0.png#pic_center)


~~~javascript
  console.log(Object instanceof Function)//true
  console.log(Object instanceof Object)//true
  console.log(Function instanceof Object)//true
  console.log(Function instanceof Function)//true
  function Foo() {}
  console.log(Object instanceof  Foo);//false
~~~

* 典例

~~~javascript
 var A = function() {

  }
  A.prototype.n = 1

  var b = new A()

  A.prototype = {
    n: 2,
    m: 3
  }

  var c = new A()
  console.log(b.n, b.m, c.n, c.m)//1 undefined 2 3
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/c6aabf4f5d1c4524bf5ceb730eea089f.png#pic_center)


~~~JavaScript
	var F = function () { };
    Object.prototype.a = function () {
      console.log('a()')
    };
    Function.prototype.b = function () {
      console.log('b()')
    };
    var f = new F();
    f.a()//a()
    f.b()//报错 原型链找不到
    F.a()//a()
    F.b()//b()
~~~



### 2.2 执行上下文与执行上下文栈

* 变量提升与函数提升
  * 变量提升: 在变量定义语句之前, 就可以访问到这个变量**(undefined)**
  * 函数提升: **通过function声明的函数**，在函数定义语句之前, 就执行该函数
  * **先有变量提升, 再有函数提升**

~~~JavaScript
	/*变量提升*/
    console.log(a1) //可以访问, 但值是undefined
    /*函数提升*/
    a2() // 可以直接调用
    var a1 = 3
    function a2() {
      console.log('a2()')
    }
~~~

* 理解
  * 执行上下文: 由js引擎自动创建的对象, 包含对应作用域中的所有变量属性
  * 执行上下文栈: 用来管理产生的多个执行上下文
* 分类:
  * 全局: window
  * 函数: 对程序员来说是透明的
* 生命周期
  * 全局 : 准备执行全局代码前产生, 当页面刷新/关闭页面时死亡
  * 函数 : 调用函数时产生, 函数执行完时死亡
* 包含哪些属性:
  * 全局 : 
    * **用var定义的全局变量  ==>undefined**
    * **使用function声明的函数   ===>function**
    * **this   ===>window**
  * 函数
    * **用var定义的局部变量  ==>undefined**
    * **使用function声明的函数   ===>function**
    * **this   ===> 调用函数的对象, 如果没有指定就是window** 
    * **形参变量   ===>对应实参值**
    * **arguments ===>实参列表的伪数组**

~~~JavaScript
function fn (a1){
    console.log(a1)//2
    console.log(a2)//undefined
    a3()//a3()
    console.log(this)//window
    console.log(atguments)//伪数组(2,3)
    
    var a2 = 3
    function a3(){
		console.log('a3()')
    }
}
fn(2,3)
~~~

* 执行上下文创建和初始化的过程
  * 全局:
    * 在全局代码执行前最先创建一个全局执行上下文(window)
    * 收集一些全局变量, 并初始化
    * 将这些变量设置为window的属性
  * 函数:
    * 在调用函数时, 在执行函数体之前先创建一个函数执行上下文
    * 收集一些局部变量, 并初始化
    * 将这些变量设置为执行上下文的属性

~~~javascript
	//1. 进入全局执行上下文
    var a = 10
    var bar = function (x) {
      var b = 5
      foo(x + b)              //3. 进入foo执行上下文
    }
    var foo = function (y) {
      var c = 5
      console.log(a + c + y)
    }
    bar(10)                    //2. 进入bar函数执行上下文
~~~

~~~javascript
 	/*
    测试题1: 先预处理变量, 后预处理函数
    */
    function a() { }
    var a;
    console.log(typeof a)//function
    /*
    测试题2: 变量预处理, in操作符
     */
    if (!(b in window)) {
      var b = 1;
    }
    console.log(b)//undefined
    /*
    测试题3: 预处理, 顺序执行
     */
    var c = 1
    //var c
    function c(c) {
      console.log(c)
      var c = 3
    }
	//c = 1
    c(2)//报错
~~~



### 2.3 作用域与作用域链

* 理解:
  * 作用域: 一块代码区域, 在编码时就确定了, 不会再变化
  * 作用域链: 多个嵌套的作用域形成的由内向外的结构, 用于查找变量
* 分类:
  * 全局作用域
  * 函数作用域
  * **js没有块作用域(在ES6之前)**
* 作用
  * 作用域: **隔离变量**, 可以在不同作用域定义同名的变量不冲突
  * 作用域链**: 查找变量**
* 区别作用域与执行上下文 
  * 作用域: 静态的, 编码时就确定了(不是在运行时), 一旦确定就不会变化了
  * 执行上下文: 动态的, 执行代码时动态创建, 当执行结束消失
  * 联系: 执行上下文环境是在对应的作用域中的

~~~javascript
	var a = 10,
      b = 20
    function fn(x) {
      var a = 100,
        c = 300；
      console.log('fn()', a, b, c, x)
      function bar(x) {
        var a = 1000,
          d = 400
        console.log('bar()', a, b, c, d, x)
      }

      bar(100)//bar() 1000 20 300 400 100
      bar(200)//bar() 1000 20 300 400 200
    }
    fn(10)//fn() 100 20 300 10
~~~

~~~javascript
  var x = 10;
  function fn() {
    console.log(x);
  }
  function show(f) {
    var x = 20;
    f();
  }
  show(fn);//fn和show是同级函数
~~~

~~~javascript
	var fn = function () {
      console.log(fn)//输出函数
    }
    fn()

    var obj = {
      fn2: function () {
        console.log(fn2)//报错
        //console.log(this.fn2)
      }
    }
    obj.fn2()
~~~



### 2.4 闭包 

* 理解:
  * **当嵌套的内部函数引用了外部函数的变量时就产生了闭包**
  * 通过chrome工具得知: 闭包本质是内部函数中的一个对象, 这个对象中包含引用的变量属性
  
* 作用:
  * 延长局部变量的生命周期
  * 让函数外部能操作内部的局部变量
  
* 常见的闭包
  ```JavaScript
  // 1. 将函数作为另一个函数的返回值
  function fn1() {
    var a = 2;
    function fn2() {
      a++;
      console.log(a);
    }
    return fn2;
  }
  var f = fn1();
  f();//3
  f();//4
  
  
  // 2. 将函数作为实参传递给另一个函数调用
  function showMsgDelay(msg, time) {
    setTimeout(function () {
      console.log(msg)
    }, time)
  }
  showMsgDelay('hello', 1000)
  ```
  
* 闭包的生命周期

  * 产生: 在嵌套内部函数**定义执行**完时就产生了(不是在调用)
  * 死亡: 在嵌套的内部函数成为**垃圾对象**时

* 闭包应用:
  * **模块化: 封装一些数据以及操作数据的函数, 向外暴露一些行为**
  * 循环遍历加监听
  * JS框架(jQuery)大量使用了闭包
* 缺点:
  * 变量占用内存的时间可能会过长
  * 可能导致内存泄露
  * 解决:
    * 及时释放 : f = null; //让内部函数对象成为垃圾对象
    

~~~javascript
	//代码片段一
    var name = "The Window";
    var object = {
      name: "My Object",
      getNameFunc: function () {
        return function () {
          return this.name;
        };
      }
    };
    console.log(object.getNameFunc()());  //The Window 直接执行函数，this指向window 无闭包

    //代码片段二
    var name2 = "The Window";
    var object2 = {
      name2: "My Object",
      getNameFunc: function () {
        var that = this;
        return function () {
          return that.name2;
        };
      }
    };
    console.log(object2.getNameFunc()()); //My Object that保存的是函数 有闭包
~~~

~~~JavaScript
	function fun(n, o) {
      console.log(o)
      return {
        fun: function (m) {
          return fun(m, n)
        }
      }
    }
    var a = fun(0)
    a.fun(1)
    a.fun(2)
    a.fun(3) //undefined,0,0,0 

    var b = fun(0).fun(1).fun(2).fun(3) //undefined,0,1,2 闭包

    var c = fun(0).fun(1)
    c.fun(2)
    c.fun(3) //undefined,0,1,1 前面闭包，后面是因为闭包延长局部变量的生命周期
~~~



### 2.5 内存溢出与内存泄露

1. 内存溢出
  * 一种程序运行出现的错误
  * 当程序运行需要的内存超过了剩余的内存时, 就出抛出内存溢出的错误
2. 内存泄露
  * 占用的内存没有及时释放
  * 内存泄露积累多了就容易导致内存溢出
  * 常见的内存泄露:
    * 意外的全局变量
    * 没有及时清理的计时器或回调函数
    * 闭包



## 3、对象高级

### 3.1 对象的创建模式

* Object构造函数模式
  ```javascript
  //适用场景: 起始时不确定对象内部数据
  //问题: 语句太多
  var obj = {};
  obj.name = 'Tom'
  obj.setName = function(name){this.name=name}
  ```
  
* 对象字面量模式
  ```javascript
  //适用场景: 起始时对象内部数据是确定的
  //问题: 如果创建多个对象, 有重复代码
  var obj = {
    name : 'Tom',
    setName : function(name){this.name = name}
  }
  ```
  
* 工厂模式

  ~~~javascript
  // 工厂函数: 返回一个需要的数据的函数
  //适用场景: 需要创建多个对象
  //问题: 对象没有一个具体的类型, 都是Object类型
    function createPerson(name, age) {
      var p = {
        name: name,
        age: age,
        setName: function (name) {
          this.name = name
        }
      }
      return p
    }
  ~~~

* 构造函数模式
  
  ```javascript
  //适用场景: 需要创建多个类型确定的对象
  //问题: 每个对象都有相同的数据, 浪费内存
  function Person(name, age) {
    this.name = name;
    this.age = age;
    this.setName = function(name){this.name=name;};
  }
  new Person('tom', 12);
  ```
  
* 构造函数+原型的组合模式
  ```javascript
  //适用场景: 需要创建多个类型确定的对象
  function Person(name, age) {
    this.name = name;
    this.age = age;
  }
  Person.prototype.setName = function(name){this.name=name;};
  new Person('tom', 12);
  ```
  



### 3.2 继承模式

* 原型链继承 : 得到方法,**子类型的原型为父类型的一个实例对象**(关键)
  ```javascript
  function Parent(){}
  Parent.prototype.test = function(){};
  
  function Child(){}
  Child.prototype = new Parent(); // 子类型的原型指向父类型实例
  
  Child.prototype.constructor = Child
  var child = new Child(); //有test()
  ```

![在这里插入图片描述](https://img-blog.csdnimg.cn/5e26c428bae2465383cb7cf354bba124.png#pic_center)


* 借用构造函数 : 得到属性，**在子类型构造函数中通用super()调用父类型构造函数**(关键)

  ```javascript
  function Parent(xxx){this.xxx = xxx}
  Parent.prototype.test = function(){};
  function Child(xxx,yyy){
      Parent.call(this, xxx);//借用构造函数   this.Parent(xxx)
  }
  var child = new Child('a', 'b');  //child.xxx为'a', 但child没有test()
  ```
* 组合
  ```javascript
  function Parent(xxx){this.xxx = xxx}
  Parent.prototype.test = function(){};
  function Child(xxx,yyy){
      Parent.call(this, xxx);//借用构造函数   this.Parent(xxx)
  }
  Child.prototype = new Parent(); //得到test()
  var child = new Child(); //child.xxx为'a', 也有test()
  ```
* new一个对象背后做了些什么?
  * 创建一个空对象
  * 给对象设置__ proto__ , 值为构造函数对象的prototype属性值   this.__ proto__ = Fn.prototype
  * 执行构造函数体(给对象添加属性/方法)



## 4、线程机制与事程机制

### 4.1 线程与进程

* 进程:
  * 程序的一次执行, 它占有一片独有的内存空间
  * 可以通过windows任务管理器查看进程
* 线程:
  * 是进程内的一个独立执行单元
  * 是程序执行的一个完整流程
  * **是CPU的基本调度单元**
* 关系
  * 一个进程至少有一个线程(主)
  * 程序是在某个进程中的某个线程执行的



### 4.2 浏览器内核模块组成

* 主线程
  * js引擎模块 : 负责js程序的编译与运行
  * html,css文档解析模块 : 负责页面文本的解析
  * DOM/CSS模块 : 负责dom/css在内存中的相关处理 
  * 布局和渲染模块 : 负责页面的布局和效果的绘制(内存中的对象)
* 分线程
  * 定时器模块 : 负责定时器的管理
  * DOM事件模块 : 负责事件的管理
  * 网络请求模块 : 负责Ajax请求



### 4.3 js线程

* js是单线程执行的(回调函数也是在主线程)
* JavaScript的单线程，与它的用途有关；作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题
* H5提出了实现多线程的方案: Web Workers；只能是主线程更新界面



### 4.4 定时器问题

* 定时器并不真正完全定时
* 如果在主线程执行了一个长时间的操作, 可能导致延时才处理



### 4. 5 事件处理机制

* 代码分类
  * 初始化执行代码: **包含绑定dom事件监听, 设置定时器, 发送ajax请求的代码**
  * 回调执行代码: 处理回调逻辑
* js引擎执行代码的基本流程: 
  * 初始化代码===>回调代码
* 模型的2个重要组成部分:
  * 事件管理模块
  * 回调队列
* 模型的运转流程
  * 执行初始化代码, 将事件回调函数交给对应模块管理
  * 当事件发生时, 管理模块会将回调函数及其数据添加到回调列队中
  * 只有当初始化代码执行完后(可能要一定时间), 才会遍历读取回调队列中的回调函数执行

![在这里插入图片描述](https://img-blog.csdnimg.cn/6a6ec78fa0d74b6490cef4aacb8232c2.png#pic_center)




### 4.6 H5 Web Workers

![在这里插入图片描述](https://img-blog.csdnimg.cn/6b5a0c210a9b4608ad36f8c415c3c5bf.png#pic_center)


* 可以让js在分线程执行

* Worker

  ```javascript
  var worker = new Worker('worker.js');
  worker.onMessage = function(event){event.data};// 用来接收另一个线程发送过来的数据的回调
  worker.postMessage(data1);//向另一个线程发送数据
  ```

* 问题:

  * worker内代码不能操作DOM更新UI
  * 不是每个浏览器都支持这个新特性
  * 不能跨域加载JS

 

