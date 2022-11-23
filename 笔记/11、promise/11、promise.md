# Promise

## 1、Promise介绍与基本使用

### 1.1 Promise概述

**理解**

1. 抽象表达:

   1)Promise是一门新的技术(ES6规范)

   2)Promise是Js中进行异步编程的新解决方案

   * 备注:旧方案是单纯使用回调函数

2. 具体表达:

     1)从语法上来说: Promise是一个构造函数

     2)从功能上来说: promise对象用来封装一个异步操作(fs 文件操作、数据库操作、AJAX 、定时器 )并可以获取其成功/失败的结果值
     
     

**Promise的状态改变**

1. pending 变为resolved
1. pending变为reject
* 说明:只有这2种，且**一个promise对象只能改变一次**；无论变为成功还是失败，都会有一个结果数据；成功的结果数据一般称为value，失败的结果数据一般称为reason



**Promise的基本流程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1111e7dc18634ec590363b9cc03474c9.png#pic_center)




### 1.2 Promise的作用

* **指定回调函数的方式更加灵活**
  1. 旧的:必须在启动异步任务前指定
  2. promise:启动异步任务=>返回promie对象=>给promise对象绑定回调函数(甚至可以在异步任务结束后指定/多个)
* **支持链式调用，可以解决回调地狱问题**
     1. 什么是回调地狱 -- 回调函数嵌套调用，外部回调函数异步执行的结果是嵌套的回调执行的条件
     2. 回调地狱的缺点 -- 不便于阅读，不便于异常处理
     3. 解决方案 -- promise链式调用
     4. 终极解决方案 -- async/await



### 1.3 Promise的使用

* Promise实践练习-fs模块

~~~js
const fs = require('fs');

//回调函数 形式
// fs.readFile('./resource/content.txt', (err, data) => {
//     // 如果出错 则抛出错误
//     if(err)  throw err;
//     //输出文件内容
//     console.log(data.toString());
// });

//Promise 形式
let p = new Promise((resolve , reject) => {
    fs.readFile('./resource/content.txt', (err, data) => {
        //如果出错
        if(err) reject(err);
        //如果成功
        resolve(data);
    });
});

//调用 then 
p.then(value=>{
    console.log(value.toString());
}, reason=>{
    console.log(reason);
});
~~~

* Promise封装练习-fs模块

~~~js
/**
 * 封装一个函数 mineReadFile 读取文件内容
 * 参数:  path  文件路径
 * 返回:  promise 对象
 */
function mineReadFile(path){
    return new Promise((resolve, reject) => {
        //读取文件
        require('fs').readFile(path, (err, data) =>{
            //判断
            if(err) reject(err);
            //成功
            resolve(data);
        });
    });
}

mineReadFile('./resource/content.txt')
.then(value=>{
    //输出文件内容
    console.log(value.toString());
}, reason=>{
    console.log(reason);
});
~~~

* Promise实践练习-AJAX请求

~~~js
		const btn = document.querySelector('#btn');

        btn.addEventListener('click', function(){
            //创建 Promise
            const p = new Promise((resolve, reject) => {
                //1.创建对象
                const xhr = new XMLHttpRequest();
                //2. 初始化
                xhr.open('GET', 'https://api.apiopen.top/getJoke');
                //3. 发送
                xhr.send();
                //4. 处理响应结果
                xhr.onreadystatechange = function(){
                    if(xhr.readyState === 4){
                        //判断响应状态码 2xx   
                        if(xhr.status >= 200 && xhr.status < 300){
                            //控制台输出响应体
                            resolve(xhr.response);
                        }else{
                            //控制台输出响应状态码
                            reject(xhr.status);
                        }
                    }
                }
            });
            //调用then方法
            p.then(value=>{
                console.log(value);
            }, reason=>{
                console.warn(reason);
            });
        });
~~~

* Promise封装AJAX操作

~~~js
		/**
         * 封装一个函数 sendAJAX 发送 GET AJAX 请求
         * 参数   URL
         * 返回结果 Promise 对象
         */
        function sendAJAX(url){
            return new Promise((resolve, reject) => {
                const xhr = new XMLHttpRequest();
                xhr.responseType = 'json';
                xhr.open("GET", url);
                xhr.send();
                //处理结果
                xhr.onreadystatechange = function(){
                    if(xhr.readyState === 4){
                        //判断成功
                        if(xhr.status >= 200 && xhr.status < 300){
                            //成功的结果
                            resolve(xhr.response);
                        }else{
                            reject(xhr.status);
                        }
                    }
                }
            });
        }
    
        sendAJAX('https://api.apiopen.top/getJok')
        .then(value => {
            console.log(value);
        }, reason => {
            console.warn(reason);
        });
~~~



## 2、Promise API

1. **Promise构造函数**: Promise (excutor){}

   (1)executor函数:执行器(resolve, reject)=>{}

   (2)resolve函数:内部定义成功时我们调用的函数value =>{}

   (3)reject 函数:内部定义失败时我们调用的函数reason => {}

   * 说明: **executor 会在 Promise 内部立即同步调用**,异步操作在执行器中执行

     

2. **Promise.prototype.then**方法:(onResolved, onRejected)=>{}

    (1)onResolved 函数:成功的回调函数(value)=>{}

   (2)onRejected 函数:失败的回调函数(reason)=>{}

   * 说明:指定用于得到成功value 的成功回调和用于得到失败reason的失败回调返回一个新的promise对象

     

3. **Promise.prototype.catch方法**:(onRejected)=>{}

   *  onRejected 函数:失败的回调函数(reason)=> {}

   * 说明: then()的语法糖，相当于: then(undefined, onRejected)

     

4. **Promise.resolve方法**:(value)=>{}

  * value:成功的数据或promise对象

  * 说明:返回一个成功/失败的promise对象

    

5. **Promise.reject方法**: (reason)=>{}

  * reason:失败的原因

  * 说明:返回一个失败的promise对象

    

6. **Promise.all方法**:(promises)=>{}

  * promises:包含n个promise的数组

  * 说明:**返回一个新的promise，只有所有的promise都成功才成功，只要有一个失败了就直接失败**

    

7. **Promise.race方法**:(promises)=>0
   
   * promises:包含n个promise的数组
   * 说明:**返回一个新的promise，第一个完成的promise 的结果状态就是最终的结果状态**



## 3、Promise关键问题

1. 如何改变promise 的状态?

   (1)**resolve(value)**:如果当前是pending就会变为resolved

   (2)**reject(reason)**:如果当前是pending 就会变为rejected

   (3)**抛出异常**:如果当前是pending 就会变为rejected

   

2. 一个promise指定多个成功/失败回调函数，都会调用吗?

   当promise**改变为对应状态时都会调用**

   

3. 改变promise状态和指定回调函数谁先谁后?

   (1)都有可能，正常情况下是先指定回调再改变状态(异步任务)，但也可以先改状态再指定回调(同步任务)

   (2)如何先改状态再指定回调?

   * 在执行器中直接调用resolve()/reject()
   * 延迟更长时间才调用then()

   (3)什么时候才能得到数据?

   * 如果先指定的回调，那当状态发生改变时，回调函数就会调用，得到数据(异步任务)
   * 如果先改变的状态，那当指定回调时，回调函数就会调用，得到数据(同步任务)



4. promise.then()返回的新promise的结果状态由什么决定?

   (1)简单表达:由 then()指定的回调函数执行的结果决定

   (2)详细表达:

   * 如果抛出异常，**新promise变为rejected, reason为抛出的异常**
   * 如果返回的是非promise的任意值，**新promise变为resolved, value为返回的值**
   * 如果返回的是另一个新promise，**此promise的结果就会成为新promise的结果**



5. promise如何串连多个操作任务?

   (1)promise 的 then()返回一个新的promise，可以开成then()的链式调用

   (2)通过 then的链式调用串连多个同步/异步任务



6. promise异常传透?

   (1)当使用promise的then链式调用时，可以在最后指定失败的回调

   (2)前面任何操作出了异常，都会传到最后失败的回调中处理



7. 中断promise链?

   (1)当使用promise的then链式调用时，在中间中断，不再调用后面的回调函数

   (2)办法:**在回调函数中返回一个pendding状态的 promise对象**



## 4、Promise自定义封装

* 自定义Promise

~~~js
//声明构造函数
function Promise(executor) {
    //添加属性
    this.PromiseState = 'pending';
    this.PromiseResult = null;
    //声明属性
    this.callbacks = [];
    //保存实例对象的 this 的值
    const self = this;// self _this that
    //resolve 函数
    function resolve(data) {
        //判断状态
        if (self.PromiseState !== 'pending') return;
        //1. 修改对象的状态 (promiseState)
        self.PromiseState = 'fulfilled';// resolved
        //2. 设置对象结果值 (promiseResult)
        self.PromiseResult = data;
        //调用成功的回调函数
        setTimeout(() => {
            self.callbacks.forEach(item => {
                item.onResolved(data);
            });
        });
    }
    //reject 函数
    function reject(data) {
        //判断状态
        if (self.PromiseState !== 'pending') return;
        //1. 修改对象的状态 (promiseState)
        self.PromiseState = 'rejected';// 
        //2. 设置对象结果值 (promiseResult)
        self.PromiseResult = data;
        //执行失败的回调
        setTimeout(() => {
            self.callbacks.forEach(item => {
                item.onRejected(data);
            });
        })
    }
    try {
        //同步调用『执行器函数』
        executor(resolve, reject);
    } catch (e) {
        //修改 promise 对象状态为『失败』
        reject(e);
    }
}

//添加 then 方法
Promise.prototype.then = function (onResolved, onRejected) {
    const self = this;
    //判断回调函数参数
    if (typeof onRejected !== 'function') {
        onRejected = reason => {
            throw reason;
        }
    }
    if (typeof onResolved !== 'function') {
        onResolved = value => value;
        //value => { return value};
    }
    return new Promise((resolve, reject) => {
        //封装函数
        function callback(type) {
            try {
                //获取回调函数的执行结果
                let result = type(self.PromiseResult);
                //判断
                if (result instanceof Promise) {
                    //如果是 Promise 类型的对象
                    result.then(v => {
                        resolve(v);
                    }, r => {
                        reject(r);
                    })
                } else {
                    //结果的对象状态为『成功』
                    resolve(result);
                }
            } catch (e) {
                reject(e);
            }
        }
        //调用回调函数  PromiseState
        if (this.PromiseState === 'fulfilled') {
            setTimeout(() => {
                callback(onResolved);
            })
        }
        if (this.PromiseState === 'rejected') {
            setTimeout(() => {
                callback(onRejected);
            })
        }
        //判断 pending 状态
        if (this.PromiseState === 'pending') {
            //保存回调函数
            this.callbacks.push({
                onResolved: function () {
                    callback(onResolved);
                },
                onRejected: function () {
                    callback(onRejected);
                }
            });
        }
    })
}

//添加 catch 方法
Promise.prototype.catch = function (onRejected) {
    return this.then(undefined, onRejected);
}

//添加 resolve 方法
Promise.resolve = function (value) {
    //返回promise对象
    return new Promise((resolve, reject) => {
        if (value instanceof Promise) {
            value.then(v => {
                resolve(v);
            }, r => {
                reject(r);
            })
        } else {
            //状态设置为成功
            resolve(value);
        }
    });
}

//添加 reject 方法
Promise.reject = function (reason) {
    return new Promise((resolve, reject) => {
        reject(reason);
    });
}

//添加 all 方法
Promise.all = function (promises) {
    //返回结果为promise对象
    return new Promise((resolve, reject) => {
        //声明变量
        let count = 0;
        let arr = [];
        //遍历
        for (let i = 0; i < promises.length; i++) {
            //
            promises[i].then(v => {
                //得知对象的状态是成功
                //每个promise对象 都成功
                count++;
                //将当前promise对象成功的结果 存入到数组中
                arr[i] = v;
                //判断
                if (count === promises.length) {
                    //修改状态
                    resolve(arr);
                }
            }, r => {
                reject(r);
            });
        }
    });
}

//添加 race 方法
Promise.race = function (promises) {
    return new Promise((resolve, reject) => {
        for (let i = 0; i < promises.length; i++) {
            promises[i].then(v => {
                //修改返回对象的状态为 『成功』
                resolve(v);
            }, r => {
                //修改返回对象的状态为 『失败』
                reject(r);
            })
        }
    });
}
~~~



## 5、async与await

### 5.1. mdn文档
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async functionhttps://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await



### 5.2.async函数

1. 函数的返回值为promise对象

2. promise对象的结果由async函数执行的返回值决定



### 5.3.await表达式

1. await右侧的表达式一般为promise对象，但也可以是其它的值
1. 如果表达式是promise对象, await返回的是promise 成功的值
1. 如果表达式是其它值，直接将此值作为await的返回值



### 5.4.注意

1. await 必须写在async函数中，但 async函数中可以没有await
2. 如果await 的promise失败了，就会抛出异常，需要通过try...catch 捕获处理

sync与await


