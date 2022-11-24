# axios

## 1、axios的理解和使用

### 1.1 axios概述

1. 前端最流行的ajax请求库

2. react/vue官方都推荐使用axios 发ajax 请求 

3. **文档:** https://github.com/axios/axios

4. axios中文网：[axios中文网|axios API 中文文档 | axios (axios-js.com)](http://www.axios-js.com/)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2adafdd0431e4173b25a9aa62e43fa90.png#pic_center)






### 1.2 axios特点

1. 基于xhr + promise的异步ajax请求库
2. 浏览器端/node端都可以使用
3. 支持请求/响应拦截器
4. 支持请求取消
5. 请求/响应数据转换
6. 批量发送多个请求



### 1.3 axios常用语法

* axios(config):通用/最本质的发任意类型请求的方式
* axios(url[, config]):可以只指定url发get 请求
* axios.request(config):等同于axios(config)
* axios.get(url[, config]):发get请求
* axios.delete(url[, config]):发delete请求
* axios.post(url[, data, config]):发post请求
* axios.put(url[, data, configl):发put 请求
* axios.defaults.xxx:请求的默认全局配置
* axios.interceptors.request.use():添加请求拦截器
* axios.interceptors.response.use():添加响应拦截器
* axios.create([config]):创建一个新的axios(它没有下面的功能)
* axios.Cancel():用于创建取消请求的错误对象
* axios.CancelToken():用于创建取消请求的token对象
* axios.isCancel():是否是一个取消请求的错误
* axios.all(promises):用于批量执行多个异步请求
* axios.spread():用来指定接收所有成功数据的回调函数的方法


![在这里插入图片描述](https://img-blog.csdnimg.cn/5ec0d6b391d9486eb0b52cb41a3b925f.png#pic_center)



* axios基本使用

~~~js
    //获取按钮
    const btns = document.querySelectorAll('button');

    //第一个
    btns[0].onclick = function () {
        //发送 AJAX 请求
        axios({
            //请求类型
            method: 'GET',
            //URL
            url: 'http://localhost:3000/posts/2',
        }).then(response => {
            console.log(response);
        });
    }

    //添加一篇新的文章
    btns[1].onclick = function () {
        //发送 AJAX 请求
        axios({
            //请求类型
            method: 'POST',
            //URL
            url: 'http://localhost:3000/posts',
            //设置请求体
            data: {
                title: "今天天气不错, 还挺风和日丽的",
                author: "张三"
            }
        }).then(response => {
            console.log(response);
        });
    }

    //更新数据
    btns[2].onclick = function () {
        //发送 AJAX 请求
        axios({
            //请求类型
            method: 'PUT',
            //URL
            url: 'http://localhost:3000/posts/3',
            //设置请求体
            data: {
                title: "今天天气不错, 还挺风和日丽的",
                author: "李四"
            }
        }).then(response => {
            console.log(response);
        });
    }

    //删除数据
    btns[3].onclick = function () {
        //发送 AJAX 请求
        axios({
            //请求类型
            method: 'delete',
            //URL
            url: 'http://localhost:3000/posts/3',
        }).then(response => {
            console.log(response);
        });
    }
~~~

* axios其他使用

~~~js
//获取按钮
    const btns = document.querySelectorAll('button');

    //发送 GET 请求
    btns[0].onclick = function () {
        // axios()
        axios.request({
            method: 'GET',
            url: 'http://localhost:3000/comments'
        }).then(response => {
            console.log(response);
        })
    }

    //发送 POST 请求
    btns[1].onclick = function () {
        // axios()
        axios.post(
            'http://localhost:3000/comments',
            {
                "body": "喜大普奔",
                "postId": 2
            }).then(response => {
                console.log(response);
            })
    }
~~~

* axios默认配置

~~~js
    //获取按钮
    const btns = document.querySelectorAll('button');
    //默认配置
    axios.defaults.method = 'GET';//设置默认的请求类型为 GET
    axios.defaults.baseURL = 'http://localhost:3000';//设置基础 URL
    axios.defaults.params = { id: 100 };
    axios.defaults.timeout = 3000;//

    btns[0].onclick = function () {
        axios({
            url: '/posts'
        }).then(response => {
            console.log(response);
        })
    }
~~~



### 1.4 难点语法的理解和使用

 **axios.create(config)**

1. 根据指定配置创建一个新的axios，也就是每个新axios都有自己的配置
2. 新axios 只是没有取消请求和批量发请求的方法，其它所有语法都是一致的
3. 为什么要设计这个语法?
   (1)需求:项目中有部分接口需要的配置与另一部分接口需要的配置不太一
   样，如何处理
   (2)解决:创建2个新axios，每个都有自己特有的配置，分别应用到不同要
   求的接口请求中



**拦截器函数/ajax请求/请求的回调函数的调用顺序**

1. 说明:调用axios()并不是立即发送ajax请求，而是需要经历一个较长的流程
2. 流程:请求拦截器2=>请求拦截器1=>发ajax请求=>响应拦截器1=>响
   应拦截器2=>请求的回调  **(unshift,push)**
3. 注意:此流程是通过promise串连起来的，请求拦截器传递的是config，响应
   拦截器传递的是response

* 代码：

~~~js
    // Promise
    // 设置请求拦截器  config 配置对象
    axios.interceptors.request.use(function (config) {
        console.log('请求拦截器 成功 - 1号');
        //修改 config 中的参数
        config.params = { a: 100 };

        return config;
    }, function (error) {
        console.log('请求拦截器 失败 - 1号');
        return Promise.reject(error);
    });

    axios.interceptors.request.use(function (config) {
        console.log('请求拦截器 成功 - 2号');
        //修改 config 中的参数
        config.timeout = 2000;
        return config;
    }, function (error) {
        console.log('请求拦截器 失败 - 2号');
        return Promise.reject(error);
    });

    // 设置响应拦截器
    axios.interceptors.response.use(function (response) {
        console.log('响应拦截器 成功 1号');
        return response.data;
        // return response;
    }, function (error) {
        console.log('响应拦截器 失败 1号')
        return Promise.reject(error);
    });

    axios.interceptors.response.use(function (response) {
        console.log('响应拦截器 成功 2号')
        return response;
    }, function (error) {
        console.log('响应拦截器 失败 2号')
        return Promise.reject(error);
    });

    //发送请求
    axios({
        method: 'GET',
        url: 'http://localhost:3000/posts'
    }).then(response => {
        console.log('自定义回调处理成功的结果');
        console.log(response);
    });
~~~



**取消请求**

1. 基本流程
   配置cancelToken对象
   缓存用于取消请求的cancel函数
   在后面特定时机调用cancel函数取消请求
   在错误回调中判断如果error是cancel，做相应处理
2. 实现功能
   点击按钮，取消某个正在请求中的请求

* 代码：

~~~js
	//获取按钮
    const btns = document.querySelectorAll('button');
    //2.声明全局变量
    let cancel = null;
    //发送请求
    btns[0].onclick = function () {
        //检测上一次的请求是否已经完成
        if (cancel !== null) {
            //取消上一次的请求
            cancel();
        }
        axios({
            method: 'GET',
            url: 'http://localhost:3000/posts',
            //1. 添加配置对象的属性
            cancelToken: new axios.CancelToken(function (c) {
                //3. 将 c 的值赋值给 cancel
                cancel = c;
            })
        }).then(response => {
            console.log(response);
            //将 cancel 的值初始化
            cancel = null;
        })
    }

    //绑定第二个事件取消请求
    btns[1].onclick = function () {
        cancel();
    }
~~~



## 2、axios源码分析

### 2.1 源码目录结构 

![在这里插入图片描述](https://img-blog.csdnimg.cn/012dc3125db54ac89c62f3eefad5bd8f.png#pic_center)




### 2.2 源码分析

**axios 与Axios的关系**

1. 从语法上来说: axios不是Axios 的实例  **(对象，函数，实例对象的方法添加到函数身上)**
2. 从功能上来说: axios是Axios的实例   **(拥有实例对象上的方法)**
3. axios是Axios.prototype.request 函数bind()返回的函数
4. axios作为对象有Axios原型对象上的所有方法，有Axios对象上所有属性



**instance 与axios的区别**

1. 相同:
   (1都是一个能发任意请求的函数: request(config)

   (2)都有发特定请求的各种方法:get()/post()/put()/delete()

   (3)都有默认配置和拦截器的属性: defaults/interceptors

2. 不同:

   (1)默认配置很可能不一样

   (2)instance没有axios后面添加的一些方法: create()/CancelToken()/all()



**axios运行的整体流程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/042b6292616349c584af2e0543d61540.png#pic_center)


1. 整体流程:
   request(config) ==> dispatchRequest(config)  ==> xhrAdapter(config)

2. request(config):
将请求拦截器/ dispatchRequest()/响应拦截器通过promise链串连起来，返回promise
3. dispatchRequest(config):
转换请求数据== =>调用xhrAdapter()发请求 ===>请求返回后转换响应数据.返回 promise
4. xhrAdapter(config):
创建XHR对象，根据config进行相应设置，发送特定请求，并接收响应数据，返回promise



**axios的请求/响应拦截器是什么**

![在这里插入图片描述](https://img-blog.csdnimg.cn/6489a46d7e1a4709870445a164ed0d03.png#pic_center)


1. 请求拦截器:
   * 在真正发送请求前执行的回调函数
   * 可以对请求进行检查或配置进行特定处理
   * 成功的回调函数，传递的默认是config(也必须是)
   * 失败的回调函数，传递的默认是error
2. 响应拦截器
   * 在请求得到响应后执行的回调函数
   * 可以对响应数据进行特定处理
   * 成功的回调函数，传递的默认是response
   * 失败的回调函数，传递的默认是error



**axios的请求/响应数据转换器是什么**

1. 请求转换器:对请求头和请求体数据进行特定处理的函数
   if (utils.isObject(data)) {
   setContentTypelfUnset(headers, 'application/json;charset=utf-8');
   return JSON.stringify(data);
   }
2. 响应转换器:将响应体json字符串解析为js对象或数组的函数
   response.data = JSON.parse(response.data)



**response的整体结构**
{
data,

status,

statusText,

headers,

config,

request
}



**error的整体结构**
{
message,

response,
request,
}



**如何取消未完成的请求**

1. 当配置了cancelToken对象时，保存cancel函数

   (1创建一个用于将来中断请求的cancelPromise

   (2)并定义了一个用于取消请求的cancel函数

   (3)将cancel函数传递出来

2. 调用cancel()取消请求

   (1)执行cacel 函数，传入错误信息message

   (2)内部会让cancelPromise变为成功，且成功的值为一个Cancel对象

   (3)在cancelPromise 的成功回调中中断请求，并让发请求的 proimse失败，
   失败的reason为 Cancel对象
,

headers,

config,

request
}



**error的整体结构**
{
message,

response,
request,
}



**如何取消未完成的请求**

1. 当配置了cancelToken对象时，保存cancel函数

   (1创建一个用于将来中断请求的cancelPromise

   (2)并定义了一个用于取消请求的cancel函数

   (3)将cancel函数传递出来

2. 调用cancel()取消请求

   (1)执行cacel 函数，传入错误信息message

   (2)内部会让cancelPromise变为成功，且成功的值为一个Cancel对象

   (3)在cancelPromise 的成功回调中中断请求，并让发请求的 proimse失败，
   失败的reason为 Cancel对象

