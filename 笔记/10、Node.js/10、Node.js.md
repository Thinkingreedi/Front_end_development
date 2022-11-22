# Node.js

## 1、初识Node.js与内置模块

### 1.1 Node.js初识

**JavaScript可以在浏览器中执行**

* 不同的浏览器使用不同的JavaScript解析引擎:
  * Chrome浏览器 =>  v8
  * Firefox浏览器 =>  OdinMonkey(奥丁猴)
  * Safri浏览器 =>  JSCore
  * IE浏览器 => Chakra(查克拉)
  * etc...
* 其中，**Chrome浏览器的V8解析引擎性能最好**!



**JavaScript操作DOM和BOM**

* 每个浏览器都内置了DOM、BOM这样的API函数，因此，浏览器中的JavaScript才可以调用它们



**浏览器中的JavaScript运行环境**

* 运行环境是指代码正常运行所需的必要环境

![在这里插入图片描述](https://img-blog.csdnimg.cn/38f6ee6b630349f0bd93d9c91520a37f.png#pic_center)


* 总结:
  * v8引擎负责解析和执行JavaScript 代码
  * 内置API是由运行环境提供的特殊接口，只能在所属的运行环境中被调用



**Node.js简介**

* Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine
* Node.js是一个基于Chrome V8引擎的**JavaScript运行环境**
* Node.js 的官网地址: https://nodejs.org/zh-cn/
* 注意：
  * **浏览器**是JavaScript的前端运行环境
  * **Node.js**是JavaScript的后端运行环境
  * Node.js中**无法调用DOM和 BOM等浏览器内置API**

* 用途：
  * 基于Express框架（http://www.expressjs.com.cn/)，可以快速构建Web应用
  * 基于Electron框架(https://electronjs.org/)，可以构建跨平台的桌面应用
  * 基于restify框架(http://restify.com/)，可以快速构建API接口项目
  * 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc...



**Node.js的安装**

* 安装包可以从Node.js的官网首页直接下载，进入到Node.js的官网首页(https://nodejs.org/en/) node.js中文网 ([Node.js 中文网 (nodejs.cn)](http://nodejs.cn/))，点击绿色的按钮，下载所需的版本后，双击直接安装即可

* LTS为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装LTS版本的Node.js
* Current为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装Current版本的Node.js。但是，Current 版本中可能存在隐藏的Bug 或安全性漏洞，因此不推荐在企业级项目中使用Current版本的Node.js
* 打开终端，在终端输入命令node -v后，按下回车键，即可查看已安装的Node.js的版本号
* 在Node.js环境中执行JavaScript 代码
  1. 打开终端
  2. 输入node要执行的js文件的路径



### 1.2 fs文件系统模块

**fs文件系统模块概述**

* fs模块是Node.js官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求、例如:
  * fs.readFile()方法，用来**读取**指定文件中的内容
  * fs.writeFile()方法，用来向指定的文件中**写入**内容



**读取指定文件中的内容**

* 使用fs.readFile()方法，可以读取指定文件中的内容，语法格式如下:

~~~js
fs.readFile(path[, options], callback)
~~~

* 参数解读:
  * 参数1:**必选**参数，字符串，表示文件的路径
  * 参数2:可选参数，表示以什么**编码格式**来读取文件
  * 参数3:**必选**参数，文件读取完成后，通过回调函数拿到读取的结果
* 代码：

~~~js
// 1. 导入 fs 模块，来操作文件
const fs = require('fs')

// 2. 调用 fs.readFile() 方法读取文件
//    参数1：读取文件的存放路径
//    参数2：读取文件时候采用的编码格式，一般默认指定 utf8
//    参数3：回调函数，拿到读取失败和成功的结果  err  dataStr
fs.readFile('./files/1.txt', 'utf8', function (err, dataStr) {
  // 2.1 打印失败的结果
  // 如果读取成功，则 err 的值为 null
  // 如果读取失败，则 err 的值为 错误对象，dataStr 的值为 undefined
  console.log(err)
  console.log('-------')
  // 2.2 打印成功的结果
  console.log(dataStr)
})
~~~

* 判断文件是否读取成功：

~~~js
const fs = require('fs')

fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
~~~



**向指定文件写入内容**

* 使用fs.writeFile()方法，可以向指定的文件中写入内容，语法格式如下:

~~~js
fs.writeFile(file,data[, options], callback)
~~~

* 参数解读:
  * 参数1:**必选**参数，需要指定一个文件路径的字符串，表示文件的存放路径
  * 参数2:**必选**参数，表示要写入的内容
  * 参数3:可选参数，表示以什么格式写入文件内容，默认值是utf-8
  * 参数4:**必选**参数，文件写入完成后的回调函数
* 代码：

~~~js
// 1. 导入 fs 文件系统模块
const fs = require('fs')

// 2. 调用 fs.writeFile() 方法，写入文件的内容
//    参数1：表示文件的存放路径
//    参数2：表示要写入的内容
//    参数3：回调函数
fs.writeFile('./files/2.txt', 'Hello', function (err) {
  // 2.1 如果文件写入成功，则 err 的值等于 null
  // 2.2 如果文件写入失败，则 err 的值等于一个 错误对象
  // console.log(err)

  if (err) {
    return console.log('文件写入失败！' + err.message)
  }
  console.log('文件写入成功！')
})
~~~



**fs模块–路径动态拼接的问题**

* 在使用fs 模块操作文件时，如果提供的操作路径是以./或../开头的相对路径时，(非当前目录时)很容易出现路径动态拼接错误的问题
* 原因:代码在运行的时候，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径
* 解决方案:在使用fs模块操作文件时，直接提供完整的路径，不要提供./或../开头的相对路径，从而防止路径动态拼接的问题

* 代码：

~~~JavaScript
// __dirname 表示当前文件所处的目录
fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message)
  }
  console.log('读取文件成功！' + dataStr)
})
~~~



### 1.3 path路径模块

**path路径模块概述**

* path模块是Node.js官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求
* 例如:
  * path.join()方法，用来将多个路径片段拼接成一个完整的路径字符串
  * path.basename()方法，用来从路径字符串中，将文件名解析出来



**路径拼接**

* 使用path.join(方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下:

~~~js
path.join( [ .. .paths])
~~~

* 参数解读:
  * ...paths < string >路径片段的序列
  * 返回值: < string >
* 代码：

~~~js
//注意：  ../ 会抵消前面的路径
const pathStr = path.join('/a', '/b/c', '../', './d', 'e')
console.log(pathStr)  // \a\b\d\e
~~~

* 注意:今后凡是涉及到路径拼接的操作，都要使用path.join()方法进行处理，不要直接使用＋进行字符串的拼接
* 代码：

~~~js
fs.readFile(path.join(__dirname, './files/1.txt'), 'utf8', function (err, dataStr) {
  if (err) {
    return console.log(err.message)
  }
  console.log(dataStr)
})
~~~



**获取路径中的文件名**

* 使用path.basename()方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下:

~~~js
path.basename(path[, ext])
~~~

* 参数解读:
  * path < string >必选参数，表示—个路径的字符串
  * ext < string >可选参数，表示文件扩展名
  * 返回: < string >表示路径中的最后—部分

* 代码：

~~~js
const path = require('path')

// 定义文件的存放路径
const fpath = '/a/b/c/index.html'

const fullName = path.basename(fpath)
console.log(fullName)//index.html

const nameWithoutExt = path.basename(fpath, '.html')
console.log(nameWithoutExt)//index
~~~



**获取路径中的文件扩展名**

* 使用path.extname)方法，可以获取路径中的扩展名部分，语法格式如下:

~~~js
path.extname(path)
~~~

* 参数解读:
  * path < string >必选参数，表示—个路径的字符串
  * 返回:< string >返回得到的扩展名字符串

* 代码：

~~~js
const path = require('path')

// 这是文件的存放路径
const fpath = '/a/b/c/index.html'

const fext = path.extname(fpath)
console.log(fext)
~~~



### 1.4 http模块

 **http模块概述**

* 在网络节点中，负责消费资源的电脑，叫做**客户端**;负责对外提供网络资源的电脑，叫做**服务器**
* http模块是Node.js官方提供的、用来创建web服务器的模块。通过http模块提供的 http.createServer(方法，就能方便的把一台普通的电脑，变成一台Web服务器，从而对外提供Web 资源服务
* 服务器和普通电脑的区别在于，服务器上安装了web服务器软件，例如:lIS、Apache等。通过安装这些服务器软件，就能把一台普通的电脑变成一台web服务器
* 在Node.js 中，我们不需要使用IIS、Apache等这些第三方web服务器软件。因为我们可以基于Node.js 提供的http模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供web服务



**服务器相关概念：**

1、IP地址

* IP地址就是互联网上每台计算机的唯一地址，因此IP地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方IP地址的前提下，才能与对应的电脑之间进行数据通信
* IP地址的格式:通常用“点分十进制”表示成(a.b.c.d)的形式其中，a,b,c,d都是0~255之间的十进制整数。例如:用点分十进表示的IP地址(192.168.1.1)
* 注意:
  * 互联网中每台Web服务器，都有自己的IP地址，例如:大家可以在Windows的终端中运行**ping www.baidu.com 命令**，即可查看到百度服务器的IP地址
  * 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入**127.0.0.1**这个IP地址，就能把自己的电脑当做一台服务器进行访问了



2、域名和域名服务器

* 尽管IP地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即所谓的域名(Domain Name)地址
* IP地址和域名是——对应的关系，这份对应关系存放在一种叫做域名服务器(DNS,Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，域名服务器就是提供IР地址和域名之问的转换服务的服务器
* 注意:
  * 单纯使用IP地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便
  * 在开发测试期间，**127.0.0.1对应的域名是localhost**，它们都代表我们自己的这台电脑，在使用效果上没有任何区别



3、端口号

* 计算机中的端口号，就好像是现实生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中
* 同样的道理，在一台电脑中，可以运行成百上千个web服务。每个web服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的web服务进行处理
* 注意:
  * 每个端口号不能同时被多个web 服务占用
  * **在实际应用中，URL中的80端口可以被省略**

![在这里插入图片描述](https://img-blog.csdnimg.cn/75e1bcc05c9f463f9726e1ed9802fff5.png#pic_center)




**创建最基本的web服务器**

* 步骤

1. 导入http模块

* 如果希望在自己的电脑上创建一个web服务器，从而对外提供web 服务，则需要导入http模块

2. 创建web 服务器实例

* 调用http.createServer()方法，即可快速创建一个 web 服务器实例

3. 为服务器实例绑定request事件，监听客户端的请求

* 为服务器实例绑定request事件，即可监听客户端发送过来的网络请求

4. 启动服务器

* 调用服务器实例的.listen0方法，即可启动当前的web 服务器实例
* 代码：

~~~js
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(8080, function () {  
  console.log('server running at http://127.0.0.1:8080')
})
~~~



* req请求对象
* 只要服务器接收到了客户端的请求，就会调用通过server.on为服务器绑定的 request事件处理函数。如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用如下的方式:

* res响应对象
* 在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下的方式:

~~~js
server.on('request', (req, res) => {
  // req.url 是客户端请求的 URL 地址
  const url = req.url
  // req.method 是客户端请求的 method 类型
  const method = req.method
  const str = `Your request url is ${url}, and request method is ${method}`
  console.log(str)
  // 调用 res.end() 方法，向客户端响应一些内容
  res.end(str)
})
~~~



* 解决中文乱码问题
* 当调用res.end()方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式:

~~~js
server.on('request', (req, res) => {
  // 定义一个字符串，包含中文的内容
  const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
  // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // res.end() 将内容响应给客户端
  res.end(str)
})
~~~



**根据不同的url响应不同的html内容**

1. 获取请求的url地址
2. 设置默认的响应内容为404 Not found
3. 判断用户请求的是否为/或/index.html首页
4. 判断用户请求的是否为/about.html关于页面
5. 设置Content-Type响应头，防止中文乱码
6. 使用res.end()把内容响应给客户端

* 代码：

~~~js
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => {
  // 1. 获取请求的 url 地址
  const url = req.url
  // 2. 设置默认的响应内容为 404 Not found
  let content = '<h1>404 Not found!</h1>'
  // 3. 判断用户请求的是否为 / 或 /index.html 首页
  // 4. 判断用户请求的是否为 /about.html 关于页面
  if (url === '/' || url === '/index.html') {
    content = '<h1>首页</h1>'
  } else if (url === '/about.html') {
    content = '<h1>关于页面</h1>'
  }
  // 5. 设置 Content-Type 响应头，防止中文乱码
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // 6. 使用 res.end() 把内容响应给客户端
  res.end(content)
})

server.listen(80, () => {
  console.log('server running at http://127.0.0.1')
})

~~~



## 2、模块化

### 2.1 模块化的基本概念

**什么是模块化**

* 模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程，对于整个系统来说，模块是可组合、分解和更换的单元
* 编程领域中的模块化，就是遵守固定的规则，把一个大文件拆成独立并互相依赖的多个小模块。
* 把代码进行模块化拆分的好处:
  * 提高了代码的**复用性**
  * 提高了代码的**可维护性**
  * 可以实现**按需加载**



**模块化规范**

* 模块化规范就是对代码进行模块化的拆分与组合时，需要遵守的那些规则
* 例如:
  * 使用什么样的语法格式来引用模块
  * 在模块中使用什么样的语法格式向外暴露成员
* 模块化规范的好处:大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己



### 2.2 Node.js中模块化

**Node.js中模块的分类**

* Node.js 中根据模块来源的不同，将模块分为了3大类，分别是:
  * 内置模块(内置模块是由Node.js官方提供的，例如fs、path、http 等)
  * 自定义模块(用户创建的每个.js 文件，都是自定义模块)
  * 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载)



**加载模块**

* 使用强大的require()方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用
* 注意:使用require0方法加载其它模块时，会执行被加载模块中的代码**(加载且执行)**



**Node.js中模块作用域**

* 和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种**模块级别的访问限制**，叫做模块作用域
* **防止全局变量污染问题**



**向外共享模块作用域中的成员**

1. module对象
   在每个.js自定义模块中都有一个module对象，它里面**存储了和当前模块有关的信息**

2. module.exports对象
   在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用。外界用require(方法导入自定义模块时，得到的就是 module.exports 所指向的对象

3. 共享成员时的注意点
   使用require()方法导入模块时，导入的结果，**永远以module.exports指向的对象为准**

* 代码：

~~~js
// 在外界使用 require 导入一个自定义模块的时候，得到的成员，
// 就是 那个模块中，通过 module.exports 指向的那个对象
const m = require('./自定义模块')

console.log(m)
~~~

~~~js
// 在一个自定义模块中，默认情况下， module.exports = {}

const age = 20//*

// 1、向 module.exports 对象上挂载 username 属性
module.exports.username = 'zs'
// 2、向 module.exports 对象上挂载 sayHello 方法
module.exports.sayHello = function () {
  console.log('Hello!')
}
module.exports.age = age//*

///3、让 module.exports 指向一个全新的对象
module.exports = {
  nickname: '小黑',
  sayHi() {
    console.log('Hi!')
  }
}
~~~

4. exports 对象
   由于module.exports单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了exports对象。默认情况下，**exports和module.exports 指向同一个对象**。最终共享的结果，还是以module.exports 指向的对象为准
   * 时刻谨记,require()模块时，得到的永远是module.exports指向的对象
   * 注意:为了防止混乱，建议大家不要在同一个模块中同时使用exports和module.exports

![在这里插入图片描述](https://img-blog.csdnimg.cn/b2dc523a30f84990b9ec36df37423e39.png#pic_center)


* 一开始指向同一个对象，得到的永远是module.exports指向的对象，关键看有没有指向新的对象！！！



**Node.js中的模块化规范**

* Node.js遵循了CommonJS模块化规范，CommonJS规定了模块的特性和各模块之间如何相互依赖
* CommonJS规定:
  * 每个模块内部,module变量代表当前模块
  * module变量是一个对象，它的exports 属性(即module.exports）是对外的接口
  * 加载某个模块，其实是加载该模块的module.exports 属性。require()方法用于加载模块



### 2.3 npm与包

**包**

* Node.js 中的第三方模块又叫做包
* 不同于Node.js 中的内置模块与自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用(免费且开源)
* 由于Node.js的内置模块仅提供了一些底层的API，导致在基于内置模块进行项目开发的时，效率很低。包是基于内置模块封装出来的，提供了更高级、更方便的API，极大的提高了开发效率；包和内置模块之间的关系，类似于jQuery和浏览器内置API之间的关系
* 注意:
  * 从https://www.npmjs.com/ 网站上**搜索**自己所需要的包
  * 从https://registry.npmjs.org/服务器上**下载**自己需要的包
* 这个包管理工具的名字叫做Node Package Manager(简称npm包管理工具)，这个包管理工具随着Node.js 的安装包一起被安装到了用户的电脑上
* 大家可以在终端中执行npm -v命令，来查看自己电脑上所安装的npm包管理工具的版本号



**npm**

* 在项目中安装指定名称的包：`npm install 包的完整名称` ;可简写为：`npm i 包的完整名称`
* 初次装包完成后，在项目文件夹下多一个叫做node_modules的文件夹和package-lock.json的配置文件
* 其中:
  * node modules文件夹用来存放所有已安装到项目中的包；require()导入第三方包时，就是从这个目录中查找并加载包
  * package-lockjson配置文件用来记录node_modules目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等
  * 注意:程序员不要手动修改node modules或package-lock.json文件中的任何代码，npm 包管理工具会自动维护它们
* 默认情况下，使用npm install命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过**@符号指定具体的版本**，例如:`npm i moment@2.22.2`
* 包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如2.24.0其中每一位数字所代表的的含义如下:
  * 第1位数字:大版本
  * 第2位数字:功能版本
  * 第3位数字: Bug修复版本
  * 版本号提升的规则:只要前面的版本号增长了，则后面的版本号归零



**包管理配置文件**

* npm 规定，在项目根目录中，必须提供一个叫做 package.json的包管理配置文件。用来记录与项目有关的一些配置信息。例如:
  * 项目的名称、版本号、描述等
  * 项目中都用到了哪些包
  * 哪些包只在开发期间会用到
  * 那些包在开发和部署时都需要用到



* 多人协作 -- **共享时剔除node_modules**
* 在项目根目录中，创建一个叫做package,json的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除node_modules 目录之后，在团队成员之间共享项目的源代码
* 注意:今后在项目开发中，一定要把node_modules文件夹，添加到.gitignore忽略文件中



**快速创建package.json**

* npm包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，快速创建package.json这个包管理配置文件:` npm init -y`
* 注意:
  * 上述命令只能在英文的目录下成功运行！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格
  * 运行npm install 命令安装包的时候，npm包管理工具会自动把包的名称和版本号，记录到 package.json 中



**dependencies节点**

* package.json文件中，有一个dependencies节点，专门用来记录您使用npm install命令安装了哪些包

![在这里插入图片描述](https://img-blog.csdnimg.cn/d583082ce22544ee923d6a1af72b8cd6.png#pic_center)




**一次性安装所有的包**

* 可以运行`npm install`命令(或`npm i`)一次性安装所有的依赖包
* 执行npm install 命令时，npm包管理工具会先读取package.json 中的 dependencies节点
* 读取到记录的所有依赖包名称和版本号之后，npm包管理工具会把这些包一次性下载到项目中



**卸载包**

* 可以运行`npm uninstall`命令，来卸载指定的包
* 注意: npm uninstall 命令执行成功后，会把卸载的包，自动从packagejson的dependencies中移除掉。



**devDependencies节点**

* 如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies节点中;与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到dependencies节点中
* 可以使用如下的命令，将包记录到devDependencies节点中:`npm i 包名-D` (简写) `npm install包名--save-dev`(完整)



**npm下包速度慢的解决**

* 在使用npm下包的时候，默认从国外的 https://registry.npmjs.org/服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢
* 淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包同步到国内的服务器，然后在国内提供下包的服务；从而极大的提高了下包的速度

![在这里插入图片描述](https://img-blog.csdnimg.cn/044db0f2b7a546b29cf0be5aed15c785.png#pic_center)




* 切换npm的下包镜像源

~~~Markdown
# 查看当前的下包镜像源
npm config get registry

# 将下包的镜像源切换为淘宝镜像源
npm config set registry=https : /lregistry.npm.taobao.org/

# 检查镜像源是否下载成功
npm config get registry

~~~

* 为了更方便的切换下包的镜像源，我们可以安装nrm这个小工具，利用nrm提供的终端命令，可以快速查看和切换下包的镜像源。

~~~Markdown
# 通过npm包管理器，将nrm安装为全局可用的工具
npm i nrm -g

# 查看所有可用的镜像源
nrm ls

# 将下包的镜像源切换为taobao镜像
nrm use taobao
~~~



**包的分类**

* 使用npm包管理工具下载的包，共分为两大类，分别是:
  * 项目包
    * 那些被安装到项目的node_modules目录中的包，都是项目包
    * 项目包又分为两类，分别是:
      * 开发依赖包(被记录到devDependencies节点中的包，只在开发期间会用到)
      * 核心依赖包（被记录到dependencies节点中的包，在开发期间和项目上线之后都会用到)
  * 全局包
    * 在执行npm install 命令时，如果提供了 -g参数，则会把包安装为全局包
    * 全局包会被安装到C:\Users用户目录\AppData\Roaminginpm\node_modules目录下
    * 注意:
      * 只有工具性质的包，才有全局安装的必要性，因为它们提供了好用的终端命令
      * 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可



**i5ting_toc**

* i5ting_toc是一个可以把md文档转为 html页面的小工具，使用步骤如下:

~~~markdown
# 将i5ting_toc安装为全局包
npm install -g i5ting toc

# 调用i5ting_toc，轻松实现md转html的功能
i5ting_toc -f 要转换的md文件路径 -o
~~~



**规范的包结构**

* 一个规范的包，它的组成结构，必须符合以下3点要求:
  * 包必须以单独的目录而存在
  * 包的顶级目录下要必须包含package.json这个包管理配置文件
  * package.json中必须包含name，version，main这三个属性，分别代表包的名字、版本号、包的入口
* 更多约束：https://yarnpkg.com/zh-Hans/docs/package-json



**编写包 -- 发布包 -- 使用包**



### 2.4 模块的加载机制

**优先从缓存中加载**

* 模块在第一次加载后会被缓存，这也意味着**多次调用require()不会导致模块的代码被执行多次**
* 注意:不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率



**内置模块的加载机制**

* 内置模块是由Node.js官方提供的模块，**内置模块的加载优先级最高**
* 例如，require('fs')始终返回内置的fs模块，即使在node_modules目录下有名字相同的包也叫做fs



**自定义模块的加载机制**

* 使用require()加载自定义模块时，必须指定以./或../开头的路径标识符。在加载自定义模块时，如果没有指定./或../这样的路径标识符，则node 会把它当作内置模块或第三方模块进行加载
* 同时，在使用require()导入自定义模块时，如果省略了文件的扩展名，则Nodejs 会按顺序分别尝试加载以下的文件:
1. 按照确切的文件名进行加载
1. 补全js扩展名进行加载
1. 补全 .json扩展名进行加载
1. 补全.node扩展名进行加载
1. 加载失败，终端报错



**第三方模块的加载机制**

* 如果传递给require()的模块标识符不是一个内置模块，也没有以./或../开头，则Node.js 会从当前模块的父目录开始，尝试从/node_modules文件夹中加载第三方模块

* 如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录

* 例如，假设在'C:\Users\itheima\project\foojs'文件里调用require("tools')，则 Node.js 会按以下顺序找:

1. C:\Users\heima\project\node_modules\tools
2. C:\Users\heima\node_modules\tools
3. C:\Users\node_modules\tools
4. C:\node_modules\tools



**目录作为模块**

* 当把目录作为模块标识符，传递给require(进行加载的时候，有三种加载方式:
1. 在被加载的目录下查找一个叫做 package.json的文件，并寻找main属性，作为require()加载的入口
2. 如果目录里没有package.json 文件，或者main入口不存在或无法解析，则Node.js将会试图加载目录下的 index.js文件
3. 如果以上两步都失败了，则Nodejs 会在终端打印错误消息，报告模块的缺失: Error. Cannot find module 'xxx'



## 3、Express

### 3.1 初识Express

**Express简介**

* 官方给出的概念: Express是基于Node.js平台，快速、开放、极简的Web开发框架
* 通俗的理解: Express 的作用和Node.,js 内置的http模块类似，是专门用来创建Web服务器的
* Express 的本质:就是一个npm 上的第三方包，提供了快速创建web服务器的便捷方法
* Express 的中文官网: http://www.expressjs.com.cn/

* 对于前端程序员来说，最常见的两种服务器，分别是:

  * Web 网站服务器:专门对外提供Web 网页资源的服务器

  * API接口服务器:专门对外提供API接口的服务器

* 使用Express，我们可以方便、快速的创建Web 网站的服务器或API接口的服务器



**Express基本使用**

1. 安装：`npm i express@4.17.1`
2. 创建基本的Web服务器
3. 监听GET请求
4. 监听POST请求
5. 把内容响应给客户端
6. 获取URL中携带的查询参数
7. 获取URL中的动态参数

* 代码：

~~~js
// 1. 导入 express
const express = require('express')
// 2. 创建 web 服务器
const app = express()

// 3. 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 JSON 对象
  res.send({ name: 'zs', age: 20, gender: '男' })
})
app.post('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 文本字符串
  res.send('请求成功')
})
app.get('/', (req, res) => {
  // 通过 req.query 可以获取到客户端发送过来的 查询参数
  // 注意：默认情况下，req.query 是一个空对象
  console.log(req.query)
  res.send(req.query)
})
// 注意：这里的 :id 是一个动态的参数
app.get('/user/:ids/:username', (req, res) => {
  // req.params 是动态匹配到的 URL 参数，默认也是一个空对象
  console.log(req.params)
  res.send(req.params)
})

// 4. 启动 web 服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
~~~



**托管静态资源**

* express提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器例如，通过如下代码就可以将public目录下的图片、CSS文件、JavaScript文件对外开放访问了
* 注意:Express在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在URL中
* 访问静态资源文件时，express.static()函数会根据目录的添加顺序查找所需的文件
* 代码：

~~~js
const express = require('express')
const app = express()

// 在这里，调用 express.static() 方法，快速的对外提供静态资源
app.use('/files', express.static('./files'))//按添加顺序查找所需文件，挂载路径前缀
app.use(express.static('./clock'))

app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})

~~~



**nodemon**

* 在编写调试Nodejs项目的时候，如果修改了项目的代码，则需要频繁的手动close掉，然后再重新启动，非常繁琐；我们可以使用nodemon (https://www.npmjs.com/package/nodemon)这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试
* 在终端中，运行如下命令，即可将nodemon安装为全局可用的工具：`npm install -g nodemon`
* 使用：`node app.js` => `nodemon app.js`



### 3.2 Express路由

**路由的概念**

* 广义上来讲，路由就是映射关系

* 在Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系
* Express 中的路由分3部分组成，分别是请求的类型、请求的URL地址、处理函数，格式如下:`app.METHOD(PATH，HANDLER)`
* 每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数
* 在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则Express 会将这次请求，转交给对应的function函数进行处理

![在这里插入图片描述](https://img-blog.csdnimg.cn/bd7fe7e957244c38bcdb36d9df5345da.png#pic_center)


* 路由匹配的注意点:
  * 按照定义的先后顺序进行匹配
  * 请求类型和请求的URL同时匹配成功，才会调用对应的处理函数



**路由的使用**

* 最简单路由代码：

~~~js
const express = require('express')
const app = express()

// 挂载路由
app.get('/', (req, res) => {
  res.send('hello world.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
~~~

* 模块化路由 -- 为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到app 上，而是推荐将路由抽离为单独的模块。将路由抽离为单独模块的步骤如下:
  1. 创建路由模块对应的.js 文件
  2. 调用express.Router()函数创建路由对象
  3. 向路由对象上挂载具体的路由
  4. 使用module.exports向外共享路由对象
  5. 使用app.use()函数注册路由模块

* 创建路由模块代码：

~~~js
// 1. 导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()

// 3. 挂载具体的路由
router.get('/user/list', (req, res) => {
  res.send('Get user list.')
})
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})

// 4. 向外导出路由对象
module.exports = router
~~~

* 注册路由模块代码：

~~~js
// 1．导入路由模块
const userRouter = require( ' ./router/user.js ')

// 2．使用app.use()注册路由模块
app.use(userRouter)
// 注意： app.use() 函数的作用，就是来注册全局中间件
~~~

* 为路由模块添加前缀代码：

~~~js
//使用app.use()注册路由模块，并添加统的访问前缀
app.use( ' /api ', userRouter)
~~~



### 3.3 Express中间件

**中间件的概念**

* 中间件(Middleware ) ，特指业务流程的中间处理环节
* 当一个请求到达Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理

![在这里插入图片描述](https://img-blog.csdnimg.cn/e4b9ab872f9442d29ecb7a64a45b3ad5.png#pic_center)

* Express的中间件，本质上就是一个function处理函数，Express中间件的格式如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/4961e383611b4212aa28e891656fa8a6.png#pic_center)


* 注意:中间件函数的形参列表中，必须包含next参数，而路由处理函数中只包含req和res
* next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由

![在这里插入图片描述](https://img-blog.csdnimg.cn/16569adf38044122ba47720a6119cb54.png#pic_center)




**中间件初体验**

* 最简单的中间件函数：

~~~js
//常量mw所指向的,就是一个中间件函数
const mw = function (req. res,next) {
    console.log('这是一个最简单的中间件函数")
	//注意:在当前中间件的业务处理完毕后，必须调用next()函数
	//表示把流转关系转交给下一个中间件或路由
	next()
}
~~~

* 全局生效的中间件：

~~~js
//常量mw所指向的,就是一个中间件函数
const mw = function (req. res,next) {
    console.log( "这是一个最简单的中间件函数")
    next()
}
//全局生效的中间件
app.use(mw)
~~~

* 全局中间件的简化形式：

~~~js
//全局生效的中间件
app.use(function (req,res,next) {
    console.log( '这是一个最简单的中间件函数')
    next()
})
~~~

* 多个中间件之间，共享同一份req和res。基于这样的特性，我们可以在上游的中间件中，统一为req或 res对象添加自定义的属性或方法，供下游的中间件或路由进行使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/8c207cb2f09043d5974b3ce9570b815e.png#pic_center)


* 定义多个全局中间件

~~~js
app.use( function(req, res, next) //第1个全局中间
	console.1og('调用了第1个全局中间件')
	next()
})
app.use( function(req, res, next) //第2个全局中间件
    console.log('调用了第2个全局中间件")
	next()
})
app.get( ' /user ', (req, res) => {//请求这个路由，会依次触发上述两个全局中间件
	res.send( ' Home page.")
})
~~~

* 局部生效的中间件

~~~js
//定义中间件函数mw1
const mw1 = function(req. res,next) {
    console.log("这是中间件函数")
    next()
}
// mw1(中间件函数)这个中间件只在"当前路由中生效"，这种用法属于"局部生效的中间件"
app.get( '/'，mw1,function(req, res) {
    res.send('Home page.')
})
//mw1这个中间件不会影响下面这个路由↓↓↓
app.get( ' /user '， function(req，res) { 
    res.send( 'User page.') 
})
~~~

* 定义多个局部中间件

~~~js
//以下两种写法是"完全等价"的，可根据自己的喜好，选择任意一种方式进行使用
app.get( ' / ' ,mw1,mw2，(req，res) => { res.send( 'Home page. ')})
app.get( ' / '，[mw1，mw2]，(req，res) => { res.send( 'Home page.')})
~~~

* 注意事项：

1. —定要在路由之前注册中间件
2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
3. 执行完中间件的业务代码之后，不要忘记调用next()函数
4. 为了防止代码逻辑混乱，调用next()函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，共享req和res对象



**中间件分类**

1. 应用级别的中间件
   * 通过app.use()或 app.get()或app.post()，绑定到app实例上的中间件，叫做应用级别的中间件
   
     
   
2. 路由级别的中间件
   * 绑定到express.Router()实例上的中间件，叫做路由级别的中间件，它的用法和应用级别中间件没有任何区别，只不过，应用级别中间件是绑定到app实例上，路由级别中间件绑定到 router 实例上
   
     
   
3. 错误级别的中间件
   * 错误级别中间件的作用:专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题
   * 格式:错误级别中间件的 function 处理函数中，必须有4个形参，形参顺序从前到后，分别是(err,req, res, next)
   * 代码：
   
   ~~~js
   // 导入 express 模块
   const express = require('express')
   // 创建 express 的服务器实例
   const app = express()
   
   // 1. 定义路由
   app.get('/', (req, res) => {
     // 1.1 人为的制造错误
     throw new Error('服务器内部发生了错误！')
     res.send('Home page.')
   })
   
   // 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃,注册在所有路由之后
   app.use((err, req, res, next) => {
     console.log('发生了错误！' + err.message)
     res.send('Error：' + err.message)
   })
   
   // 调用 app.listen 方法，指定端口号并启动web服务器
   app.listen(80, function () {
     console.log('Express server running at http://127.0.0.1')
   })
   ~~~
   
   
   
4. Express内置的中间件
   * 自Express 4.16.0版本开始，Express内置了3个常用的中间件，极大的提高了Express 项目的开发效率和体验:
     1. express.static快速托管静态资源的内置中间件，例如:HTML文件、图片、CSS样式等(无兼容性)
     2. express.json解析JSON格式的请求体数据（有兼容性，仅在4.16.0+版本中可用)
     3. express.urlencoded解析URL-encoded格式的请求体数据（有兼容性，仅在4.16.0+版本中可用)
   
   * 代码：
   
   ~~~js
   // 导入 express 模块
   const express = require('express')
   // 创建 express 的服务器实例
   const app = express()
   
   // 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
   // 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
   app.use(express.json())
   // 通过 express.urlencoded() 这个中间件，来解析 表单中的 url-encoded 格式的数据
   app.use(express.urlencoded({ extended: false }))
   
   app.post('/user', (req, res) => {
     // 在服务器，可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
     // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
     console.log(req.body)
     res.send('ok')
   })
   
   app.post('/book', (req, res) => {
     // 在服务器端，可以通过 req,body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
     console.log(req.body)
     res.send('ok')
   })
   
   // 调用 app.listen 方法，指定端口号并启动web服务器
   app.listen(80, function () {
     console.log('Express server running at http://127.0.0.1')
   })
   ~~~
   
   
   
5. 第三方的中间件
   * 非Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率
   
   * 例如:在 express@4.16.0之前的版本中，经常使用body-parser这个第三方中间件，来解析请求体数据。
   
   * 使用步骤如下:
     
     1. 运行npm install body-parser安装中间件
     
     2. 使用require导入中间件
     
     3. 调用app.use()注册并使用中间件
     
   * 注意: Express 内置的express.urlencoded 中间件，就是基于body-parser这个第三方中间件进一步封装出来的



**自定义中间件**

1. 定义中间件
2. 监听req的data 事件
3. 监听req的end事件
4. 使用querystring模块解析请求体数据
5. 将解析出来的数据对象挂载为req.body
6. 将自定义中间件封装为模块

* 代码：

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()
// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring')

// 这是解析表单数据的中间件
app.use((req, res, next) => {
  // 定义中间件具体的业务逻辑
  // 1. 定义一个 str 字符串，专门用来存储客户端发送过来的请求体数据
  let str = ''
  // 2. 监听 req 的 data 事件
  req.on('data', (chunk) => {
    str += chunk
  })
  // 3. 监听 req 的 end 事件
  req.on('end', () => {
    // 在 str 中存放的是完整的请求体数据
    // console.log(str)
    // TODO: 把字符串格式的请求体数据，解析成对象格式
    const body = qs.parse(str)
    req.body = body
    next()
  })
})

app.post('/user', (req, res) => {
  res.send(req.body)
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
~~~



### 3.4 使用Express写接口

* 解决接口跨域问题的方案主要有两种:
1. CORS (主流的解决方案，推荐使用)
    * CORS 是 Express的一个第三方中间件,通过安装和配置cors 中间件，可以很方便地解决跨域问题。使用步骤分为如下3步:
      1. 运行npm install cors安装中间件
      2. 使用const cors = require('cors')导入中间件在路由之前调用
      3. app.use(cors())配置中间件
2. JSONP (有缺陷的解决方案:只支持GET请求)



**CORS跨域资源共享**

* CORS (Cross-Origin Resource Sharing，跨域资源共享）由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止前端JS代码跨域获取资源
* 浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了CORS相关的HTTP响应头，就可以解除浏览器端的跨域访问限制

![在这里插入图片描述](https://img-blog.csdnimg.cn/85b3a6273893455e9800539fba03d987.png#pic_center)


* CORS的注意事项
  1. CORS主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了CORS的接口
  2. CORS在浏览器中有兼容性。只有支持XMLHttpRequest Level2的浏览器，才能正常访问开启了CORS的服务端接口**(例如:IE10+、Chrome4+、FireFox3.5+)**

* 响应头部中可以携带一个Access-Control-Allow-Origin字段，其语法如下:
  `Access-Control-Allow-origin: <origin> | *`其中,origin参数的值指定了允许访问该资源的外域URL

~~~js
res.setHeader( ' Access-Control-Allow-Origin ', 'http: /litcast.cn')
~~~

* 默认情况下，CORS仅支持客户端向服务器发送如下的9个请求头:
  `Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type (值仅限于text/plain、multipart/form-data、application/x-www-form-urlencoded三者之一)`;如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败!

~~~js
//允许客户端额外向服务器发送Content-Type 请求头和X-Custom-Header请求头//注意:多个请求头之间使用英文的逗号进行分割
res.setHeader( ' Access-Control-Allow-Headers ' ，'Content-Type，x-Custom-Header ')
~~~

* 默认情况下，CORS仅支持客户端发起`GET、POST、HEAD`请求。
  如果客户端希望通过PUT、DELETE等方式请求服务器的资源，则需要在服务器端，通过Access-Control-Alow-Method来指明实际请求所允许使用的HTTP方法

~~~js
//只允许POST、GET、DELETE、HEAD请求方法
res.setHeader ( ' Access-Control-Allow-Methods ','POST，GET，DELETE，HEAD" )
//允许所有的 HTTP请求方法
res.setHeader( 'Access-Control-Allow-Methods " , '*')

~~~

* 客户端在请求CORS接口时，根据请求方式和请求头的不同，可以将CORS的请求分为两大类，分别是:

  1. 简单请求 **(客户端与服务器之间只会发生一次请求)**

  * 请求方式: GET、POST、HEAD三者之一
  * HTTP头部信息不超过以下几种字段:无自定义头部字段、Accept、Accept-Language、Content-Language、DPR,Downlink、Save-Data、Viewport-Width、Width 、Content-Type(只有三个值application/x-www-form-
    urlencoded、multipart/form-data、text/plain)

  2. 预检请求 **(客户端与服务器之间会发生两次请求，OPTION预检请求成功之后，才会发起真正的请求)**

  * 请求方式为GET、POST、HEAD之外的请求Method类型
  * 请求头中包含自定义头部字段
  * 向服务器发送了application/ison格式的数据



**JSONP接口**

* 概念:浏览器端通过< scrip t>标签的src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做JSONP
* 特点:
  1. JSONP 不属于真正的Ajax请求，因为它没有使用XMLHttpRequest这个对象
  2. JSONP仅支持GET请求，不支持 POST、PUT、DELETE 等请求

* 如果项目中已经配置了CORS跨域资源共享，为了防止冲突，必须在配置CORS中间件之前声明JSONP的接口
* 步骤：
  1. 获取客户端发送过来的回调函数的名字
  2. 得到要通过JSONP形式发送给客户端的数据
  3. 根据前两步得到的数据，拼接出—个函数调用的字符串
  4. 把上一步拼接得到的字符串，响应给客户端的< script >标签进行解析执行



* 代码：

~~~js
// 导入 express
const express = require('express')
// 创建服务器实例
const app = express()

// 配置解析表单数据的中间件
app.use(express.urlencoded({ extended: false }))

// 必须在配置 cors 中间件之前，配置 JSONP 的接口
app.get('/api/jsonp', (req, res) => {
  // TODO: 定义 JSONP 接口具体的实现过程
  // 1. 得到函数的名称
  const funcName = req.query.callback
  // 2. 定义要发送到客户端的数据对象
  const data = { name: 'zs', age: 22 }
  // 3. 拼接出一个函数的调用
  const scriptStr = `${funcName}(${JSON.stringify(data)})`
  // 4. 把拼接的字符串，响应给客户端
  res.send(scriptStr)
})

// 一定要在路由之前，配置 cors 这个中间件，从而解决接口跨域的问题
const cors = require('cors')
app.use(cors())

// 导入路由模块
const router = require('./apiRouter')
// 把路由模块，注册到 app 上
app.use('/api', router)

// 启动服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
~~~

~~~js
const express = require('express')
const router = express.Router()

// 在这里挂载对应的路由
router.get('/get', (req, res) => {
  // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
  const query = req.query
  // 调用 res.send() 方法，向客户端响应处理的结果
  res.send({
    status: 0, // 0 表示处理成功，1 表示处理失败
    msg: 'GET 请求成功！', // 状态的描述
    data: query, // 需要响应给客户端的数据
  })
})

// 定义 POST 接口
router.post('/post', (req, res) => {
  // 通过 req.body 获取请求体中包含的 url-encoded 格式的数据
  const body = req.body
  // 调用 res.send() 方法，向客户端响应结果
  res.send({
    status: 0,
    msg: 'POST 请求成功！',
    data: body,
  })
})

// 定义 DELETE 接口
router.delete('/delete', (req, res) => {
  res.send({
    status: 0,
    msg: 'DELETE请求成功',
  })
})

module.exports = router
~~~



## 4、数据库与身份认证

### 4.1 数据库的基本概念

**数据库的概念**

* 数据库(database）是用来组织、存储和管理数据的仓库
* 为了方便管理互联网世界中的数据，就有了数据库管理系统的概念（简称:数据库)
* 用户可以对数据库中的数据进行新增、查询、更新、删除等操作



**常见数据库及分类**

* 市面上的数据库有很多种，最常见的数据库有如下几个:
  * MySQL数据库（目前使用最广泛、流行度最高的开源免费数据库;Community + Enterprise)
  * Oracle数据库（收费)
  * SQL Server数据库（收费)
  * Mongodb数据库(Community + Enterprise)

* 其中，MySQL、Oracle、SQL Server属于**传统型数据库**(又叫做:关系型数据库或SQL数据库)，这三者的设计理念相同，用法比较类似
* 而Mongodb属于**新型数据库**(又叫做:非关系型数据库或NoSQL数据库)，它在一定程度上弥补了传统型数据库的缺陷



**传统型数据库的数据组织结构**

* 数据的组织结构:指的就是数据以什么样的结构进行存储

* 传统型数据库的数据组织结构，与Excel 中数据的组织结构比较类似

  * Excel的数据组织结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/65ba32fc283647d7aaafef31a23d7676.png#pic_center)


    * 整个Excel叫做工作簿
    * users和books是工作表
    * users 工作表中有3行数据
    * 每行数据由6列信息组成，每列信息都有对应的数据类型
    
  * 传统型数据库的数据组织结构
  
    * 在传统型数据库中，数据的组织结构分为**数据库(database)、数据表(table)、数据行(row)、字段(field)**这4大部分组成。
    * **数据库**类似于Excel的**工作簿**
    * **数据表**类似于Excel的**工作表**
    * **数据行**类似于Excel的**每一行数据**
    * **字段**类似于Excel的**列**，每个字段都有对应的数据类型



### 4.2 安装并配置MySQL

* MySQL Server:专门用来提供数据存储和服务的软件
* MySQL Workbench:可视化的 MySQL管理工具，通过它，可以方便的操作存储在MySQL Server中的数据

* [MySQL的安装（Windows系统）](https://blog.csdn.net/ASHIYI66/article/details/125046816)
* [Mac 系统配置 MySql 数据库](https://blog.csdn.net/ASHIYI66/article/details/125047739)



### 4.3 MySQL的基本使用

**使用MySQL Workbench管理数据库**

1. 连接数据库

![在这里插入图片描述](https://img-blog.csdnimg.cn/465310c6a09b4f7088255111b67fea9f.png#pic_center)


2. 主界面的组成部分

![在这里插入图片描述](https://img-blog.csdnimg.cn/8c95b8f2ae4d49279a71db4fccc9e793.png#pic_center)


3. 创建数据库

![在这里插入图片描述](https://img-blog.csdnimg.cn/3e4cd8dadda84dc98532201f8de245b8.png#pic_center)


4. 创建数据表

![在这里插入图片描述](https://img-blog.csdnimg.cn/529ae3f2dffa406c8812e0df7e3d9316.png#pic_center)


* DataType数据类型:

  * int 整数

  * varchar(len) 字符串

  * tinyint(1) 布尔值

* 字段的特殊标识:

  * PK (Primary Key) 主键、唯一标识

  * NN (Not Null) 值不允许为空

  * UQ(Unique) 值唯一

  * Al (Auto Increment) 值自动增长

5. 向表中写入数据

![在这里插入图片描述](https://img-blog.csdnimg.cn/35f1eb192e8742e5bc2e44e7705b32d3.png#pic_center)




**使用SQL管理数据库**

* SQL(英文全称: Structured Query Language)是**结构化查询语言**，专门用来访问和处理数据库的编程语言。能够让我们以编程的形式，操作数据库里面的数据
* 三个关键点:
  * SQL是一门**数据库编程语言**
  * 使用SQL语言编写出来的代码，叫做**SQL语句**
  * SQL语言**只能在关系型数据库中使用**（例如MySQL、Oracle、SQL Server)；非关系型数据库（例如Mongodb)不支持SQL语言

* 作用：
  1. 从数据库中查询数据(查)
  2. 向数据库中插入新的数据(增)
  3. 更新数据库中的数据(改)
  4. 从数据库删除数据(删)
  5. 可以创建新数据库
  6. 可在数据库中创建新表
  7. 可在数据库中创建存储过程、视图
  8. etc...



**SQL的SELECT语句**

* SELECT语句用于从表中查询数据。执行的结果被存储在一个结果表中（称为结果集)。语法格式如下:

~~~sql
--这是注释
--从　FROM　指定的［表中］，查询出［所有的］数据。　　*　表示［所有列］
SELECT　*　FROM　表名称
 
--从　FROM　指定的［表中］，查询出指定　　列名称　（字段）　的数据
SELECT 列名称 FROM 表名称
~~~

* 注意:SQL语句中的关键字对大小写不敏感。SELECT等效于select，FROM等效于from



* 我们希望从users表中选取所有的列，可以使用符号*取代列的名称，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/603c9efc765c436bb30a2852719ec54b.png#pic_center)




* 如需获取名为“username”和"password”的列的内容(从名为"users"的数据库表)，请使用下面的SELECT语句:

![在这里插入图片描述](https://img-blog.csdnimg.cn/4b70aedcc7ef4255a90e7bfb9b67415d.png#pic_center)




**SQL的INSERT INTO语句**

* INSERT INTO语句用于向数据表中插入新的数据行，语法格式如下:

~~~sql
--语法解读：向指定的表中，插入如下几列数据，列的值通过 values  -----指定
--注意：列和值要一一对应，多个列和多个值之间，使用英文的逗号分隔
insert into table_name (列1,列2...) values (值1,值2...)
~~~



* 向users 表中，插入一条username为 tony stark，password为098123的用户数据，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/a80befe850e548fdb1de8f23a56d9644.png#pic_center)



**SQL的UPDATE语句**

* Update语句用于修改表中的数据。语法格式如下:

~~~sql
--语法解读：
--1.用update 指定要更新哪个表中的数据
--2.用 set 指定列对应的新值
--3.用 where 指定更新的条件
 
 update 表名称 set 列名称 = 新值 where 列名称 = 某值
~~~



* UPDATE示例–更新某一行中的一个列，把users表中id为7的用户密码，更新为888888。示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/5dc1ab1c716b49e1b183c9b0f0b327b7.png#pic_center)




* UPDATE示例–更新某一行中的若干列，把users表中id为2的用户密码和用户状态，分别更新为admin123和1。示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/709f651be5dd454490d760414e718156.png#pic_center)




**SQL的DELETE语句**

* DELETE语句用于删除表中的行。语法格式如下:

~~~sql
--语法解读：
--从指定的表中，根据where条件，删除对应的数据行
delete from 表名称 where 列名称 = 值
~~~



* 从users表中，删除id为4的用户，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/edecca5696f84d30a65300393ca834c0.png#pic_center)





**SQL的WHERE子句**

* WHERE子句用于限定选择的标准。在SELECT、UPDATE、DELETE语句中，皆可使用WHERE子句来限定选择的标准

~~~sql
--查询语句中的 where 条件
select 列名称 from 表名称 where 列 运算符 值

--更新语句中的 where 条件
update 表名称 set 列=新值 where 列 运算符 值

--删除语句中的 where 条件
delete from 表名称 where 列 运算符 值
~~~



* 下面的运算符可在WHERE子句中使用，用来限定选择的标准:

![在这里插入图片描述](https://img-blog.csdnimg.cn/c54df7d6f6f4451db8dbe8a380572b7c.png#pic_center)


* 注意:在某些版本的SQL中，操作符<>可以写为!=

* 可以通过WHERE子句来限定SELECT的查询条件:

~~~sql
--查询status为1的所有用户
SELECT * FROM users WHERE status=1

--查询id 大于2的所有用户
SELECT * FROM users WHERE id>2

--查询username 不等于admin的所有用户
SELECT * FROM users WHERE username<> 'admin'
~~~



**SQL的AND和OR运算符**

* AND和OR可在WHERE子语句中把两个或多个条件结合起来
* AND表示必须同时满足多个条件，相当于JavaScript中的&&运算符，例如 if (a !== 10 && a !== 20)
* OR表示只要满足任意一个条件即可，相当于JavaScript中||运算符，例如if(a !== 10||a !== 20)

* 使用AND来显示所有status为0，并且id小于3的用户:

![在这里插入图片描述](https://img-blog.csdnimg.cn/d1f2bd4aee6344c8b88e1b800315786b.png#pic_center)


* 使用OR来显示所有status为1，或者username为zs 的用户:

![在这里插入图片描述](https://img-blog.csdnimg.cn/4f648717ef29475289d41ee3ffdb2e03.png#pic_center)




**SQL的OEDED BY子句**

* ORDER BY语句用于根据指定的列对结果集进行排序
* RDER BY语句**默认**按照**升序**对记录进行排序
* 如果您希望按照**降序**对记录进行排序，可以使用**DESC关键字**

* 升序排序：对users表中的数据，按照status字段进行升序排序，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/9245cd5675e7419b8329e050f4f15f48.png#pic_center)


* 降序排序：对users表中的数据，按照id字段进行降序排序，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/9c499cc6a46f4ed4870d212f7e9ab0e5.png#pic_center)


* 多重排序：对users 表中的数据，先按照status字段进行降序排序，再按照username的字母顺序，进行升序排序，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/dfa4cfd7661c4770ada543d287bde471.png#pic_center)




**SQL的COUNT(*)语句**

* COUNT(*)函数用于返回查询结果的总数据条数，语法格式如下:

~~~sql
SELECT COUNT(*) FROM 表名称
~~~



* 杳询users表中status为0的总数据条数:

![在这里插入图片描述](https://img-blog.csdnimg.cn/047ef7c623814bceb44c5720fbf2dcde.png#pic_center)


* 如果希望给查询出来的列名称设置别名，可以使用AS关键字，示例如下:

![在这里插入图片描述](https://img-blog.csdnimg.cn/1eb7afa84e12450cbe039149ca8aa0d8.png#pic_center)




### 4.4 在项目中操作MySql

**步骤：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/19b32916bc994cc0a82c9a1ac7f62faf.png#pic_center)


1. 安装操作MySQL数据库的第三方模块(mysql)

   * `npm install mysql`

2. 通过mysql模块连接到MySQL数据库

   ~~~js
   //1.导入mysql模块
   const mysql = require('mysql')
   //2.建立与mysql数据库的连接关系
   const db = mysql.createPool({
       host: '127.0.0.1',      //数据库的IP地址
       user: 'root',           //登录数据库的账号
       password: '123456',     //登录数据库的密码
       database: 'my_db_01',   //待操作的数据库
   })
   ~~~

3. 通过mysql模块执行SQL语句

   ~~~js
   //测试mysql模块能否正常工作
   db.query('select 1', (err, results) => {
       //报错
       if (err) return console.log(err.message)
       //正常
       console.log(results)
   })
   ~~~

* 查：

~~~js
//查询user表中所有的数据
const sqlStr = 'select * from users'
db.query(sqlStr, (err, results) => {
    //报错
    if (err) return console.log(err.message)
    //正常
    console.log(results)
})
~~~

* 增：

~~~js
//新增数据
const user = { username: 'ironman', password: '123456' }
//定义待执行的SQL语句
const sqlStr = 'insert into users (username,password) values(?,?)'
//执行SQL语句
db.query(sqlStr, [user.username, user.password], (err, results) => {
    //报错
    if (err) return console.log(err.message)
    //正常
    if (results.affectedRows === 1) {
        console.log('插入数据成功!')
    }
})
~~~

~~~js
//向表中新增数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速插入数据
//新增数据
const user = { username: 'ironman', password: '123456' }
//定义待执行的SQL语句
const sqlStr = 'insert into users set ?'
//执行SQL语句
db.query(sqlStr, user, (err, results) => {
    //报错
    if (err) return console.log(err.message)
    //正常
    if (results.affectedRows === 1) {
        console.log('插入数据成功!')
    }
})
~~~

* 改：

~~~js
//更新用户信息
const user = { id: 6, username: 'aaa', password: '000' }
//定义SQL语句
const sqlStr = 'update users set username=?,password=? where id=?'
//执行SQL语句
db.query(sqlStr, [user.ueername, user.password, user.id], (err, results) => {
    //报错
    if (err) return console.log(err.message)
    //正常
    if (results.affectedRows === 1) {
        console.log('更新数据成功!')
    }
})
~~~

~~~js
//向表中新增数据时，如果数据对象的每个属性和数据表的字段—一对应，则可以通过如下方式快速更新数据
//更新用户信息
const user = { id: 6, username: 'aaa', password: '000' }
//定义SQL语句
const sqlStr = 'update users set ? where id=?'
//执行SQL语句
db.query(sqlStr, [user, user.id], (err, results) => {
    //报错
    if (err) return console.log(err.message)
    //正常
    if (results.affectedRows === 1) {
        console.log('更新数据成功!')
    }
})
~~~

* 删：

~~~js
// 1．要执行的SQL语句
const sqlStr = 'DELETE FROM users WHERE id=?'
//2．调用db.query()执行SQL语句的同时，为占位符指定具体的值
//注意:如果SQL语句中有多个占位符，则必须使用数组为每个占位符指定具体的值"
//如果SQL语句中只有一个占位符，则可以省略数组
db.query(sqlStr, 5, (err, results) => {
    if (err) return console.log(err.message)// 失败
    if (results.affectedRows === 1) {
        console.log('删除数据成功! ')
    } // 成功
})
~~~

~~~js
//所谓的标记删除，就是在表中设置类似于status这样的状态字段，来标记当前这条数据是否被删除

~~~



### 4.5 前后端的身份认证

**Web开发模式**

1. 基于服务端渲染的传统Web开发模式(企业级网站)
   * 服务端渲染的概念:服务器发送给客户端的HTML页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用Ajax这样的技术额外请求页面的数据
   * 优点：前端耗时少，有利于SEO
   * 缺点：占用服务器资源，不利于前后端分离，开发效率低
2. 基于前后端分吉的新型web开发模式(后台管理项目)
   * 前后端分离的概念:前后端分离的开发模式，依赖于Ajax技术的广泛应用。简而言之，前后端分离的Web开发模式，就是后端只负责提供API接口，前端使用Ajax调用接口的开发模式
   * 优点：开发体验好，用户体验好，减轻了服务器端的渲染压力
   * 缺点：不利于SEO



 **身份认证**

* 身份认证(Authentication)又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认
* 如手机验证码登录、邮箱密码登录、二维码登录等等
* 对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案:
  1. 服务端渲染推荐使用Session认证机制
  2. 前后端分离推荐使用JWT认证机制



**Session 认证机制**

* HTTP协议的无状态性，指的是客户端的每次HTTP请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次HTTP请求的状态
* Cookie 是存储在用户浏览器中的一段不超过4KB的字符串。它由一个名称(Name)、一个值(Value)和其它几个用于控制Cookie 有效期、安全性、使用范围的可选属性组成
* 不同域名下的Cookie**各自独立**，每当客户端发起请求时，会自动把当前域名下所有未过期的Cookie一同发送到服务器
* Cookie的几大特性:
  1. 自动发送
  2. 域名独立
  3. 过期时限
  4. 4KB限制

![在这里插入图片描述](https://img-blog.csdnimg.cn/e860467aac4e405db2597cb1613b2d8b.png#pic_center)


* 由于Cookie 是存储在浏览器中的，而且浏览器也提供了读写Cookie的API，因此Cookie很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据， 通过Cookie的形式发送给浏览器**(Cookie不具有安全性)**
* Session认证机制：

![在这里插入图片描述](https://img-blog.csdnimg.cn/6eb70135413c4904a57a67ca65a1f6b6.png#pic_center)




**在Express中使用Session 认证**

1. 安装express-session中间件：`npm install express-session`
2. 配置express-session中间件
3. 向session中存数据
4. 从session中取数据
5. 清空session

* 代码：

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：请配置 Session 中间件
const session = require('express-session')
app.use(
  session({
    secret: 'itheima',
    resave: false,
    saveUninitialized: true,
  })
)

// 托管静态页面
app.use(express.static('./pages'))
// 解析 POST 提交过来的表单数据
app.use(express.urlencoded({ extended: false }))

// 登录的 API 接口
app.post('/api/login', (req, res) => {
  // 判断用户提交的登录信息是否正确
  if (req.body.username !== 'admin' || req.body.password !== '000000') {
    return res.send({ status: 1, msg: '登录失败' })
  }

  // TODO_02：请将登录成功后的用户信息，保存到 Session 中
  // 注意：只有成功配置了 express-session 这个中间件之后，才能够通过 req 点出来 session 这个属性
  req.session.user = req.body // 用户的信息
  req.session.islogin = true // 用户的登录状态

  res.send({ status: 0, msg: '登录成功' })
})

// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
  // TODO_03：请从 Session 中获取用户的名称，响应给客户端
  if (!req.session.islogin) {
    return res.send({ status: 1, msg: 'fail' })
  }
  res.send({
    status: 0,
    msg: 'success',
    username: req.session.user.username,
  })
})

// 退出登录的接口
app.post('/api/logout', (req, res) => {
  // TODO_04：清空 Session 信息
  req.session.destroy()
  res.send({
    status: 0,
    msg: '退出登录成功',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1:80')
})
~~~



**JWT认证机制**

* 当前端请求后端接口不存在跨域问题的时候，推荐使用**Session身份认证机制**
* 当前端需要跨域请求后端接口的时候，不推荐使用Session身份认证机制，推荐使用**JWT认证机制**(JSON Web Token目前最流行的跨域认证解决方案)
* JWT工作原理：用户的信息通过Token字符串的形式，保存在客户端浏览器中。服务器通过还原Token 字符串的形式来认证用户的身份

![在这里插入图片描述](https://img-blog.csdnimg.cn/d67ee49d87cd4217849eb3d02f49e5ae.png#pic_center)


* JWT通常由三部分组成，分别是Header (头部) 、Payload(有效荷载） 、Signature(签名)，三者之间使用英文的“.”分隔；**Payload部分**才是**真正的用户信息**，它是用户信息经过加密之后生成的字符串，Header和Signature**是**安全性相关**的部分，只是为了保证Token的安全性

![在这里插入图片描述](https://img-blog.csdnimg.cn/c5eb4a7a31a2422e97a2aaa1dd263b11.png#pic_center)


* 客户端收到服务器返回的JWT之后，通常会将它储存在localStorage或sessionStorage 中；此后，客户端每次与服务器通信，都要带上这个JWT的字符串，从而进行身份认证；推荐的做法是把JWT放在HTTP请求头的Authorization字段中：`Authorization: Bearer <token>`



**在Express中使用JWT**

1. 安装JWT相关的包：`npm install jsonwebtoken express-jwt`
2. 导入JWT相关的包
3. 定义secret密钥
4. 在登录成功后生成JWT字符串
5. 将JWT字符串还原为JSON对象
6. 使用req.user获取用户信息
7. 捕获解析JWT失败后产生的错误

* 代码：

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')

// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }))

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
~~~

 
码：

~~~js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// TODO_01：安装并导入 JWT 相关的两个包，分别是 jsonwebtoken 和 express-jwt
const jwt = require('jsonwebtoken')
const expressJWT = require('express-jwt')

// 允许跨域资源共享
const cors = require('cors')
app.use(cors())

// 解析 post 表单数据的中间件
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))

// TODO_02：定义 secret 密钥，建议将密钥命名为 secretKey
const secretKey = 'itheima No1 ^_^'

// TODO_04：注册将 JWT 字符串解析还原成 JSON 对象的中间件
// 注意：只要配置成功了 express-jwt 这个中间件，就可以把解析出来的用户信息，挂载到 req.user 属性上
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }))

// 登录接口
app.post('/api/login', function (req, res) {
  // 将 req.body 请求体中的数据，转存为 userinfo 常量
  const userinfo = req.body
  // 登录失败
  if (userinfo.username !== 'admin' || userinfo.password !== '000000') {
    return res.send({
      status: 400,
      message: '登录失败！',
    })
  }
  // 登录成功
  // TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
  // 参数1：用户的信息对象
  // 参数2：加密的秘钥
  // 参数3：配置对象，可以配置当前 token 的有效期
  // 记住：千万不要把密码加密到 token 字符中
  const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' })
  res.send({
    status: 200,
    message: '登录成功！',
    token: tokenStr, // 要发送给客户端的 token 字符串
  })
})

// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function (req, res) {
  // TODO_05：使用 req.user 获取用户信息，并使用 data 属性将用户信息发送给客户端
  console.log(req.user)
  res.send({
    status: 200,
    message: '获取用户信息成功！',
    data: req.user, // 要发送给客户端的用户信息
  })
})

// TODO_06：使用全局错误处理中间件，捕获解析 JWT 失败后产生的错误
app.use((err, req, res, next) => {
  // 这次错误是由 token 解析失败导致的
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      message: '无效的token',
    })
  }
  res.send({
    status: 500,
    message: '未知的错误',
  })
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(8888, function () {
  console.log('Express server running at http://127.0.0.1:8888')
})
~~~

 

