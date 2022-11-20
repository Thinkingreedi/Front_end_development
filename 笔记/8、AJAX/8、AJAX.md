# AJAX

## 1、AJAX概述

### 1.1 AJAX简介

* AJAX全称为Asynchronous JavaScript And XML，就是异步的JS和XML
* 通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势:**无刷新获取数据**
* AJAX不是新的编程语言，而是一种将现有的标准组合在一起使用的新方式



### 1.2  XML简介

* XML可扩展标记语言
* XML被设计用来传输和存储数据
* XML和HTML类似，不同的是HTML中都是预定义标签，而XML中没有预定义标签，全都是自定义标签，用来表示一些数据

~~~xml
<!--XML表示-->
<student>
	<name>孙情空</name>
	<age>18</age>
	<gender>男</gender>
</student>
~~~

~~~json
//JSON表示
{"name":"孙悟空","age":18,"gender":"男"}
~~~



### 1.3 AJAX的特点

* AJAX的优点
  1. **可以无需刷新页面而与服务器端进行通信**
  2. 允许你根据用户事件来更新部分页面内容
* AJAX的缺点
  1. 没有浏览历史，不能回退
  2. 存在跨域问题(同源)
  3. SEO不友好



## 2、HTTP相关

### 2.1 HTTP概述

* HTTP（hypertext transport protocol）协议『超文本传输协议』，协议详细规定了浏览器和万维网服务器之间互相通信的规则

* [HTTP概述 - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview)

* HTTP交互：
  1. 前后应用从浏览器端向服务器发送HTTP 请求(请求报文)
  2. 后台服务器接收到请求后, 调度服务器应用处理请求, 向浏览器端返回HTTP响应(响应报文)
  3. 浏览器端接收到响应, 解析显示响应体/调用监视回调



### 2.2 请求报文

~~~Markdown
行      POST  /s?ie=utf-8  HTTP/1.1 
头      Host: atguigu.com
        Cookie: name=guigu
        Content-type: application/x-www-form-urlencoded
        User-Agent: chrome 83
空行
体      username=admin&password=admin
~~~



### 2.3 响应报文

~~~Markdown
行      HTTP/1.1  200  OK
头      Content-Type: text/html;charset=utf-8
        Content-length: 2048
        Content-encoding: gzip
空行    
体      <html>
            <head>
            </head>
            <body>
                <h1>尚硅谷</h1>
            </body>
        </html>
~~~



### 2.4 常见的响应状态码

* **200 OK** 请求成功。一般用于GET 与POST 请求
* **201 Created** 已创建。成功请求并创建了新的资源
* **401 Unauthorized** 未授权/请求要求用户的身份认证
* **404 Not Found** 服务器无法根据客户端的请求找到资源
* **500 Internal Server Error** 服务器内部错误，无法完成请求



### 2.5 不同类型的请求及其作用

* GET: 从服务器端读取数据（查）
* POST: 向服务器端添加新数据 （增）
* PUT: 更新服务器端已有数据 （改）
* DELETE: 删除服务器端数据 （删）



### 2.6 一般http请求 与 ajax请求

* ajax请求是一种特别的 http请求
* 对服务器端来说, 没有任何区别, 区别在浏览器端
* 浏览器端发请求: **只有XHR 或fetch 发出的才是ajax 请求**, **其它所有的都是非ajax 请求**
* 浏览器端接收到响应
    (1) 一般请求: 浏览器一般会直接显示响应体数据, 也就是我们常说的刷新/跳转页面
    (2) ajax请求: 浏览器不会对界面进行任何更新操作, 只是调用监视的回调函数并传入响应相关数据



## 3、原生AJAX的使用

### 3.1 准备工作

**安装node.js**

* [Node.js 中文网 (nodejs.cn)](http://nodejs.cn/)
* 检查安装成功：node -v(命令行窗口)



**安装express(服务端框架)**

* [Express - 基于 Node.js 平台的 web 应用开发框架 - Express 中文文档 | Express 中文网 (expressjs.com.cn)](https://www.expressjs.com.cn/)

* 操作步骤：

  1. 初始化环境：`npm init --yes`

  2. 下载express包：`npm install express --save`

  3. 编写js代码：

     ~~~javascript
     // 1. 引入express
     const express = require('express');
     
     // 2. 创建应用对象
     const app = express();
     
     // 3. 创建路由规则
     // request 是对请求报文的封装
     // response 是对响应报文的封装
     app.get('/', (request, response) => {
       //  设置响应
       response.send("Hello Express");
     });
     
     // 4. 监听端口，启动服务
     app.listen(8000, () => {
       console.log("服务已经启动, 8000 端口监听中...");
      })
     ~~~

  4. 运行js程序：`node .\01express使用.js`

  5. 打开网页显示页面

  6. 调试程序可以查看请求和响应



**安装nodemon自动重启工具**

* [nodemon - npm (npmjs.com)](https://www.npmjs.com/package/nodemon)
* 步骤：
  1. 安装：`npm install -g nodemon`
  2. 启动服务：`nodemon server.js`



### 3.2 核心对象

* 核心对象

  * XMLHttpRequest，AJAX的所有操作都是通过该对象进行的

* 使用步骤

  1. 创建XMLHttpRequest对象

     ~~~javascript
     var xhr = new XMLHttpRequest();
     ~~~

  2. 设置请求信息
     ~~~javascript
     xhr.open(method, url);
     //可以设置请求头，一般不设置
     xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
     ~~~

  3. 发送请求
     ~~~javascript
     xhr.send(body)//get请求不传body参数，只有post 请求使用
     ~~~

  4. 接收响应
     ~~~javascript
     //xhr.responseXML接收xml格式的响应数据
     //xhr.responseText接收文本格式的响应数据
     xhr.onreadystatechange = function (){
     		if(xhr.readyState == 4 &&xhr.status == 200){
     			var text = xhr.responseText;
     			console.log(text);
     	}
     }
     ~~~

     

### 3.3 GET请求

* 点击返回响应信息

* 创建浏览器端使用的html文件和服务端使用的js文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/f3cdf7a415b740b3a665f5ceda296428.png#pic_center)


* 服务器端server.js

~~~javascript
// 1. 引入express
const express = require('express');

// 2. 创建应用对象
const app = express();

// 3. 创建路由规则
app.get('/server', (request, response) => {
  // 设置响应头 设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  // 设置响应体
  response.send("Hello Ajax");
});

// 4. 监听服务
app.listen(8000, () => {
  console.log("服务已经启动, 8000 端口监听中...");
 })
~~~

* 启动服务：`node server.js`
* 前端页面

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX GET 请求</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px #90b;
        }
    </style>
</head>

<body>
    <button>点击发送请求</button>
    <div id="result"></div>

    <script>
        //获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById("result");
        //绑定事件
        btn.onclick = function () {
            //1. 创建对象
            const xhr = new XMLHttpRequest();
            //2. 初始化 设置请求方法和 url
            xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200&c=300');
            //3. 发送
            xhr.send();
            //4. 事件绑定 处理服务端返回的结果
            // on  when 当....时候
            // readystate 是 xhr 对象中的属性, 表示状态 0 1 2 3 4
            // change  改变
            xhr.onreadystatechange = function () {
                //判断 (服务端返回了所有的结果)
                if (xhr.readyState === 4) {
                    //判断响应状态码 200  404  403 401 500
                    // 2xx 成功
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //处理结果  行 头 空行 体
                        //响应 
                        // console.log(xhr.status);//状态码
                        // console.log(xhr.statusText);//状态字符串
                        // console.log(xhr.getAllResponseHeaders());//所有响应头
                        // console.log(xhr.response);//响应体
                        //设置 result 的文本
                        result.innerHTML = xhr.response;
                    } else {

                    }
                }
            }
        }
    </script>
</body>

</html>
~~~



**GET请求设置请求参数**

* 设置url参数：`xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200&c=300');`

![在这里插入图片描述](https://img-blog.csdnimg.cn/7366343785f04742b6c846cf14ac42fb.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/8cc6cbfbe75b41519cad3591a6171539.png#pic_center)




### 3.4 POST请求

* 鼠标放到div中，发post请求，将响应体放在div中呈现

* server.js添加post

~~~javascript
//可以接收任意类型的请求 
app.all('/server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    //响应头
    response.setHeader('Access-Control-Allow-Headers', '*');
    //设置响应体
    response.send('HELLO AJAX POST');
});
~~~

* 前端页面

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX POST 请求</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #903;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        //获取元素对象
        const result = document.getElementById("result");
        //绑定事件
        result.addEventListener("mouseover", function(){
            //1. 创建对象
            const xhr = new XMLHttpRequest();
            //2. 初始化 设置类型与 URL
            xhr.open('POST', 'http://127.0.0.1:8000/server');
            //设置请求头
            xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
            xhr.setRequestHeader('name','atguigu');
            //3. 发送
            xhr.send('a=100&b=200&c=300');
            // xhr.send('a:100&b:200&c:300');
            // xhr.send('1233211234567');
            
            //4. 事件绑定
            xhr.onreadystatechange = function(){
                //判断
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status < 300){
                        //处理服务端返回的结果
                        result.innerHTML = xhr.response;
                    }
                }
            }
        });
    </script>
</body>
</html>
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/0b703b40e51d43dcbb7b6751a8f1fdcd.png#pic_center)




**设置请求头信息**

~~~javascript
// 设置请求体内容的类型
xhr.setRequesHeader('Content-Type','application/x-www-from-urlencoded');
// 自定义头信息
xhr.setRequesHeader('name', 'ashiyi');
~~~

* server.js中设置响应头允许自定义请求头 post改成all

~~~javascript
response.setHeader('Access-Control-Allow-Header','*');
~~~



### 3.5 json数据请求

~~~JavaScript
app.all('/json-server', (request, response) => {
  // 设置响应头, 设置允许跨域
  response.setHeader('Access-Control-Allow-Origin', '*');
  // 设置响应头, 设置允许自定义头信息
  response.setHeader('Access-Control-Allow-Headers', '*');
  // 响应一个数据
  const data = {
    name: 'atguigu'
  };
  // 对 对象 进行 字符串 转换
  let str = JSON.stringify(data)
  // 设置响应体 
  response.send(str);
});
~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSON响应</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #89b;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        //绑定键盘按下事件
        window.onkeydown = function(){
            //发送请求
            const xhr = new XMLHttpRequest();
            //设置响应体数据的类型
            xhr.responseType = 'json';
            //初始化
            xhr.open('GET','http://127.0.0.1:8000/json-server');
            //发送
            xhr.send();
            //事件绑定
            xhr.onreadystatechange = function(){
                if(xhr.readyState === 4){
                    if(xhr.status >= 200 && xhr.status < 300){
                        //
                        // console.log(xhr.response);
                        // result.innerHTML = xhr.response;
                        // 1. 手动对数据转化
                        // let data = JSON.parse(xhr.response);
                        // console.log(data);
                        // result.innerHTML = data.name;
                        // 2. 自动转换
                        console.log(xhr.response);
                        result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
</body>
</html>
~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/bb9e081745d7496aad0745aaba1e3623.png#pic_center)




### 3.6 解决IE缓存问题

  * 问题:在一些浏览器中(IE),由于缓存机制的存在，ajax只会发送的第一次请求，剩余多次请求不会在发送给浏览器而是直接加载缓存中的数据
  * 解决方式:浏览器的缓存是根据url地址来记录的，所以我们**只需要修改url地址即可避免缓存问题**
  * `xhr.open("get" ," /testAJAX?t="+Date.now());`



### 3.7 请求超时和网络异常

* 前端页面

~~~JavaScript
// 超时设置 （2秒）
xhr.timeout = 2000;
// 超时回调
xhr.ontimeout = function(){
	alert('网络超时，请稍后重试')
}
// 网络异常回调
xhr.onerror = function(){
	alert('网络异常，请稍后重试')
}
~~~

* server.js

~~~javascript
//延时响应
app.all('/delay', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    setTimeout(() => {
        //设置响应体
        response.send('延时响应');
    }, 1000)
});
~~~



### 3.8 取消请求

~~~JavaScript
// 手动取消
xhr.abort()
~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>取消请求</title>
</head>
<body>
    <button>点击发送</button>
    <button>点击取消</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        let x = null;

        btns[0].onclick = function(){
            x = new XMLHttpRequest();
            x.open("GET",'http://127.0.0.1:8000/delay');
            x.send();
        }

        // abort
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
~~~



 **重复请求问题**

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重复请求问题</title>
</head>
<body>
    <button>点击发送</button>
    <script>
        //获取元素对象
        const btns = document.querySelectorAll('button');
        let x = null;
        //标识变量
        let isSending = false; // 是否正在发送AJAX请求

        btns[0].onclick = function(){
            //判断标识变量
            if(isSending) 
                x.abort();// 如果正在发送, 则取消该请求, 创建一个新的请求
            x = new XMLHttpRequest();
            //修改 标识变量的值
            isSending = true;
            x.open("GET",'http://127.0.0.1:8000/delay');
            x.send();
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    //修改标识变量
                    isSending = false;//节流
                }
            }
        }
        // abort
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
~~~



### 3.9 AJAX请求状态

* xhr.readyState 可以用来查看请求当前的状态
* https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState
* 0:表示XMLHttpRequest实例已经生成，但是open()方法还没有被调用
* 1:表示send()方法还没有被调用，仍然可以使用setRequestHeader()，设定HTTP请求的头信息
* 2:表示send()方法已经执行，并且头信息和状态码已经收到
* 3:表示正在接收服务器传来的body 部分的数据
* 4:表示服务器数据已经完全接收，或者本次接收已经失败了



### 3.10 API总结
* XMLHttpRequest()：创建 XHR 对象的构造函数
* status：响应状态码值，如 200、404
* statusText：响应状态文本，如 ’ok‘、‘not found’
* readyState：标识请求状态的只读属性 0-1-2-3-4
* onreadystatechange：绑定 readyState 改变的监听
* responseType：指定响应数据类型，如果是 ‘json’，得到响应后自动解析响应
* response：响应体数据，类型取决于 responseType 的指定
* timeout：指定请求超时时间，默认为 0 代表没有限制
* ontimeout：绑定超时的监听
* onerror：绑定请求网络错误的监听
* open()：初始化一个请求，参数为：(method, url[, async])
* send(data)：发送请求
* abort()：中断请求 （发出到返回之间）
* getResponseHeader(name)：获取指定名称的响应头值
* getAllResponseHeaders()：获取所有响应头组成的字符串
* setRequestHeader(name, value)：设置请求头



## 4、jQuery-AJAX

### 4.1 get请求

* $.get(url, [data], [callback], [type])
  * url:请求的URL地址
  * data:请求携带的参数
  * callback:载入成功时回调函数
  * type:设置返回内容格式，xml, html, script, json, text,_default



### 4.2 post请求

* $.post(url, [data], [callback], [type])
  * url:请求的URL地址
  * data:请求携带的参数
  * callback:载入成功时回调函数
  * type:设置返回内容格式，xml, html, script, json, text,_default



### 4.3 通用方法

* 前端代码

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery 发送 AJAX 请求</title>
    <link crossorigin="anonymous" href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
<body>
    <div class="container">
        <h2 class="page-header">jQuery发送AJAX请求 </h2>
        <button class="btn btn-primary">GET</button>
        <button class="btn btn-danger">POST</button>
        <button class="btn btn-info">通用型方法ajax</button>
    </div>
    <script>
        $('button').eq(0).click(function(){
            $.get('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
                console.log(data);
            },'json');
        });

        $('button').eq(1).click(function(){
            $.post('http://127.0.0.1:8000/jquery-server', {a:100, b:200}, function(data){
                console.log(data);
            });
        });

        $('button').eq(2).click(function(){
            $.ajax({
                //url
                url: 'http://127.0.0.1:8000/jquery-server',
                //参数
                data: {a:100, b:200},
                //请求类型
                type: 'GET',
                //响应体结果
                dataType: 'json',
                //成功的回调
                success: function(data){
                    console.log(data);
                },
                //超时时间
                timeout: 2000,
                //失败的回调
                error: function(){
                    console.log('出错啦!!');
                },
                //头信息
                headers: {
                    c:300,
                    d:400
                }
            });
        });
    </script>
</body>
</html>
~~~

* server.js添加

~~~JavaScript
//jQuery 服务
app.all('/jquery-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'尚硅谷'};
    response.send(JSON.stringify(data));
});
~~~



## 5、Axios-AJAX

* 前端界面

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios 发送 AJAX请求</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
</head>

<body>
    <button>GET</button>
    <button>POST</button>
    <button>AJAX</button>

    <script>
        // https://github.com/axios/axios
        const btns = document.querySelectorAll('button');

        //配置 baseURL
        axios.defaults.baseURL = 'http://127.0.0.1:8000';

        btns[0].onclick = function () {
            //GET 请求
            axios.get('/axios-server', {
                //url 参数
                params: {
                    id: 100,
                    vip: 7
                },
                //请求头信息
                headers: {
                    name: 'atguigu',
                    age: 20
                }
            }).then(value => {
                console.log(value);
            });
        }

        btns[1].onclick = function () {
            axios.post('/axios-server', {
                username: 'admin',
                password: 'admin'
            }, {
                //url 
                params: {
                    id: 200,
                    vip: 9
                },
                //请求头参数
                headers: {
                    height: 180,
                    weight: 180,
                }
            });
        }
    
        btns[2].onclick = function(){
            axios({
                //请求方法
                method : 'POST',
                //url
                url: '/axios-server',
                //url参数
                params: {
                    vip:10,
                    level:30
                },
                //头信息
                headers: {
                    a:100,
                    b:200
                },
                //请求体参数
                data: {
                    username: 'admin',
                    password: 'admin'
                }
            }).then(response=>{
                //响应状态码
                console.log(response.status);
                //响应状态字符串
                console.log(response.statusText);
                //响应头信息
                console.log(response.headers);
                //响应体
                console.log(response.data);
            })
        }
    </script> 
</body>

</html>
~~~

* server.js添加

~~~javascript
//axios 服务
app.all('/axios-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'尚硅谷'};
    response.send(JSON.stringify(data));
});
~~~



## 6、fetch-AJAX

* 前端页面

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>fetch 发送 AJAX请求</title>
</head>
<body>
    <button>AJAX请求</button>
    <script>
        //文档地址
        //https://developer.mozilla.org/zh-CN/docs/Web/API/WindowOrWorkerGlobalScope/fetch
        
        const btn = document.querySelector('button');

        btn.onclick = function(){
            fetch('http://127.0.0.1:8000/fetch-server?vip=10', {
                //请求方法
                method: 'POST',
                //请求头
                headers: {
                    name:'atguigu'
                },
                //请求体
                body: 'username=admin&password=admin'
            }).then(response => {
                // return response.text();
                return response.json();
            }).then(response=>{
                console.log(response);
            });
        }
    </script>
</body>
</html>
~~~

* server.js添加

~~~JavaScript
//fetch 服务
app.all('/fetch-server', (request, response) => {
    //设置响应头  设置允许跨域
    response.setHeader('Access-Control-Allow-Origin', '*');
    response.setHeader('Access-Control-Allow-Headers', '*');
    // response.send('Hello jQuery AJAX');
    const data = {name:'尚硅谷'};
    response.send(JSON.stringify(data));
});
~~~



## 7、跨域

### 7.1 同源策略

* 同源策略(Same-Origin Policy)最早由Netscape公司提出，是浏览器的一种安全策略
* 同源:协议、域名、端口号必须完全相同
* 违背同源策略就是跨域

* 前端页面

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>首页</title>
</head>
<body>
    <h1>尚硅谷</h1>
    <button>点击获取用户数据</button>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            const x = new XMLHttpRequest();
            //这里因为是满足同源策略的, 所以 url 可以简写
            x.open("GET",'/data');
            //发送
            x.send();
            //
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
</html>
~~~

* server.js

~~~javascript
const express = require('express');

const app = express();

app.get('/home', (request, response)=>{
    //响应一个页面
    response.sendFile(__dirname + '/index.html');
});

app.get('/data', (request, response)=>{
    response.send('用户数据');
});

app.listen(9000, ()=>{
    console.log("服务已经启动...");
});
~~~



### 7.2如何解决跨域

**JSONP**

* JSONP是什么

  * JSONP(JSON with Padding)，是一个非官方的跨域解决方案，纯粹凭借程序员的聪明才智开发出来，只支持get请求

* JSONP工作流程
  * 在网页有一些标签天生具有跨域能力，比如:img link iframe script
  * **JSONP就是利用script标签的跨域能力来发送请求的**

* JSONP的使用

  * 动态的创建一个script标签

  ~~~javascript
  var script = document.createElement("script");
  ~~~
  
  * 设置script的 src，设置回调函数
  
  ~~~javascript
  script.src = "http://localhost:3000/testAJAX?callback=abc";
  function abc(data){
             alert(data.name);
    };
  ~~~
  
  * 将script添加到body 中
  
  ~~~javascript
  document.body.appendChild(script);
  ~~~
  
  * 服务器中路由的处理
  
  ~~~javascript
  router.get("/testAJAX" , function (req , res) {
      console.log("收到请求");
  var callback = req.query.callback;
  var obj={
      name:"孙悟空",
      age:18
    }
    res.send(callback+"("+JSON.stringify(obj)+")");
  });
  ~~~
  
  * 原理
  
    * 前端页面
  
    ~~~html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>原理演示</title>
        <style>
            #result {
                width: 300px;
                height: 100px;
                border: solid 1px #78a;
            }
        </style>
    </head>
    
    <body>
        <div id="result"></div>
        <script>
            //处理数据
            function handle(data) {
                //获取 result 元素
                const result = document.getElementById('result');
                result.innerHTML = data.name;
            }
        </script>
        <!-- <script src="http://127.0.0.1:5500/%E8%AF%BE%E5%A0%82/%E4%BB%A3%E7%A0%81/7-%E8%B7%A8%E5%9F%9F/2-JSONP/js/app.js"></script> -->
        <script src="http://127.0.0.1:8000/jsonp-server"></script>
    </body>
    
    </html>
    ~~~
  
    * server.js
  
    ~~~javascript
    //jsonp服务
    app.all('/jsonp-server',(request, response) => {
        // response.send('console.log("hello jsonp")');
        const data = {
            name: '尚硅谷atguigu'
        };
        //将数据转化为字符串
        let str = JSON.stringify(data);
        //返回结果
        response.end(`handle(${str})`);
    });
    ~~~
  
  * JSONP实践
  
    * 前端页面
  
    ~~~html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>案例</title>
    </head>
    <body>
        用户名: <input type="text" id="username">
        <p></p>
        <script>
            //获取 input 元素
            const input = document.querySelector('input');
            const p = document.querySelector('p');
            
            //声明 handle 函数
            function handle(data){
                input.style.border = "solid 1px #f00";
                //修改 p 标签的提示文本
                p.innerHTML = data.msg;
            }
    
            //绑定事件
            input.onblur = function(){
                //获取用户的输入值
                let username = this.value;
                //向服务器端发送请求 检测用户名是否存在
                //1. 创建 script 标签
                const script = document.createElement('script');
                //2. 设置标签的 src 属性
                script.src = 'http://127.0.0.1:8000/check-username';
                //3. 将 script 插入到文档中
                document.body.appendChild(script);
            }
        </script>
    </body>
    </html>
    ~~~
  
    * server.js中添加
  
    ~~~JavaScript
    //用户名检测是否存在
    app.all('/check-username',(request, response) => {
        // response.send('console.log("hello jsonp")');
        const data = {
            exist: 1,
            msg: '用户名已经存在'
        };
        //将数据转化为字符串
        let str = JSON.stringify(data);
        //返回结果
        response.end(`handle(${str})`);
    });
    ~~~
  
  * JQuery中的JSONP
  
    * 前端页面
  
    ~~~html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>jQuery-jsonp</title>
        <style>
            #result{
                width:300px;
                height:100px;
                border:solid 1px #089;
            }
        </style>
        <script crossorigin="anonymous" src='https://cdn.bootcss.com/jquery/3.5.0/jquery.min.js'></script>
    </head>
    <body>
        <button>点击发送 jsonp 请求</button>
        <div id="result">
    
        </div>
        <script>
            $('button').eq(0).click(function(){
                $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function(data){
                    $('#result').html(`
                        名称: ${data.name}<br>
                        校区: ${data.city}
                    `)
                });
            });
        </script>
    </body>
    </html>
    ~~~
  
    * server.js中添加
  
    ~~~JavaScript
    app.all('/jquery-jsonp-server',(request, response) => {
        // response.send('console.log("hello jsonp")');
        const data = {
            name:'尚硅谷',
            city: ['北京','上海','深圳']
        };
        //将数据转化为字符串
        let str = JSON.stringify(data);
        //接收 callback 参数
        let cb = request.query.callback;
    
        //返回结果
        response.end(`${cb}(${str})`);
    });
    ~~~
  
    

 **CORS**

* https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access control CORS
* CORS
  * CORS(Cross-Origin Resource Sharing)，跨域资源共享
  * CORS是**官方**的跨域解决方案，它的特点是不需要在客户端做任何特殊的操作，完全在服务器中进行处理，支持get和 post请求。跨域资源共享标准新增了一组HTTP首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源
* CORS工作过程
    * CORS是通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应以后就会对响应放行

* 前端界面

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CORS</title>
    <style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #90b;
        }
    </style>
</head>
<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            //1. 创建对象
            const x = new XMLHttpRequest();
            //2. 初始化设置
            x.open("GET", "http://127.0.0.1:8000/cors-server");
            //3. 发送
            x.send();
            //4. 绑定事件
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        //输出响应体
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
</html>
~~~

* server.js中添加

~~~JavaScript
app.all('/cors-server', (request, response)=>{
    //设置响应头
    response.setHeader("Access-Control-Allow-Origin", "*");
    response.setHeader("Access-Control-Allow-Headers", '*');
    response.setHeader("Access-Control-Allow-Method", '*');
    // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
    response.send('hello CORS');
});
~~~

~~~html
<style>
        #result{
            width:200px;
            height:100px;
            border:solid 1px #90b;
        }
</style>
</head>
<body>
    <button>发送请求</button>
    <div id="result"></div>
    <script>
        const btn = document.querySelector('button');

        btn.onclick = function(){
            //1. 创建对象
            const x = new XMLHttpRequest();
            //2. 初始化设置
            x.open("GET", "http://127.0.0.1:8000/cors-server");
            //3. 发送
            x.send();
            //4. 绑定事件
            x.onreadystatechange = function(){
                if(x.readyState === 4){
                    if(x.status >= 200 && x.status < 300){
                        //输出响应体
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
</html>
~~~

* server.js中添加

~~~JavaScript
app.all('/cors-server', (request, response)=>{
    //设置响应头
    response.setHeader("Access-Control-Allow-Origin", "*");
    response.setHeader("Access-Control-Allow-Headers", '*');
    response.setHeader("Access-Control-Allow-Method", '*');
    // response.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
    response.send('hello CORS');
});
~~~

