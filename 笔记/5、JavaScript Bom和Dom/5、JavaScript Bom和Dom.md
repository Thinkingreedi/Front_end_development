# JavaScript Bom和Dom

## 1、Web API 基本认知

![在这里插入图片描述](https://img-blog.csdnimg.cn/388cf6af4cc4440fb6bed06a6daf2777.png#pic_center)


* APl (Application Programming Interface,应用程序编程接口)是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。简单理解:**API是给程序员提供的一种工具，以便能更轻松的实现想要完成的功能**
* Web API是浏览器提供的一套操作浏览器功能和页面元素的API( BOM和DOM )
* MDN 详细 API : https://developer.mozilla.org/zh-CN/docs/Web/API



## 2、DOM -- 基础

### 2.1 DOM简介

* 文档对象模型（Document Object Model，简称DOM)，是W3C组织推荐的处理可扩展标记语言(HTML或者XML)的标准编程接口
* W3C已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式
* DOM树：

![在这里插入图片描述](https://img-blog.csdnimg.cn/b85698e6e04c428dbaa420014799218c.png#pic_center)


* 文档:一个页面就是一个文档，DOM中使用document表示
* 元素:页面中的所有标签都是元素，DOM中使用element表示
* 节点:网页中的所有内容都是节点(标签、属性、文本、注释等)，DOM中使用node表示

* **DOM把以上内容都看做是对象**



### 2.2 获取元素

**根据ID获取**

* 使用**getElementByld()**方法可以获取带有ID的元素对象

* 代码：

~~~html
	<div id="time">2019-9-9</div>
    <script>
        // 1. 因为我们文档页面从上往下加载，所以先得有标签 所以我们script写到标签的下面
        // 2. get 获得 element 元素 by 通过 驼峰命名法 
        // 3. 参数 id是大小写敏感的字符串
        // 4. 返回的是一个元素对象
        var timer = document.getElementById('time');
        console.log(timer);
        console.log(typeof timer);
        // 5. console.dir 打印我们返回的元素对象 更好的查看里面的属性和方法
        console.dir(timer);
    </script>
~~~



**根据标签名获取**

* 使用**getElementsByTagName()**方法可以返回带有指定标签名的对象的集合

* 代码：

~~~html
	<ul>
        <li>知否知否，应是等你好久11</li>
        <li>知否知否，应是等你好久22</li>
        <li>知否知否，应是等你好久33</li>
        <li>知否知否，应是等你好久44</li>

    </ul>
    <ol id="ol">
        <li>生僻字</li>
        <li>生僻字</li>
        <li>生僻字</li>
        <li>生僻字</li>

    </ol>

    <script>
        // 1.返回的是 获取过来元素对象的集合 以伪数组的形式存储的
        var lis = document.getElementsByTagName('li');
        console.log(lis);
        console.log(lis[0]);
        // 2. 我们想要依次打印里面的元素对象我们可以采取遍历的方式
        for (var i = 0; i < lis.length; i++) {
            console.log(lis[i]);

        }
        // 3. 如果页面中只有一个li 返回的还是伪数组的形式 
        // 4. 如果页面中没有这个元素 返回的是空的伪数组的形式
        // 5. element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素
        // var ol = document.getElementsByTagName('ol'); // [ol]
        // console.log(ol[0].getElementsByTagName('li'));
        var ol = document.getElementById('ol');
        console.log(ol.getElementsByTagName('li'));
    </script>
~~~

* 注意：
  1. 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
  2. 得到元素对象是动态的
  3. 如果获取不到元素,则返回为空的伪数组(因为获取不到对象)
  4. 父元素必须是单个对象(必须指明是哪一个元素对象).获取的时候不包括父元素自己



**通过HTML5新增的方法获取**

* 代码：

~~~html
	<div class="box">盒子1</div>
    <div class="box">盒子2</div>
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    <script>
        // 1. getElementsByClassName 根据类名获得某些元素集合
        var boxs = document.getElementsByClassName('box');
        console.log(boxs);
        // 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
        var firstBox = document.querySelector('.box');
        console.log(firstBox);
        var nav = document.querySelector('#nav');
        console.log(nav);
        var li = document.querySelector('li');
        console.log(li);
        // 3. querySelectorAll()返回指定选择器的所有元素对象集合
        var allBox = document.querySelectorAll('.box');
        console.log(allBox);
        var lis = document.querySelectorAll('li');
        console.log(lis);
    </script>
~~~

* 注意：querySelector和 queryselectorAll里面的选择器需要加符号,比如:document.querySelector ( '#nav')



**特殊元素获取**

* 代码：

~~~html
<body>
    <script>
        // 1.获取body 元素
        var bodyEle = document.body;
        console.log(bodyEle);
        console.dir(bodyEle);
        // 2.获取html 元素
        // var htmlEle = document.html;
        var htmlEle = document.documentElement;
        console.log(htmlEle);
    </script>
</body>
~~~



### 2.3 事件基础

* JavaScript使我们有能力创建动态页面，而事件是可以被JavaScript侦测到的行为。简单理解:触发---响应机制
* 事件三要素：
  1. 事件源
  2. 事件类型
  3. 事件处理程序
* 代码：

~~~html
	<button id="btn">唐伯虎</button>
    <script>
        // 点击一个按钮，弹出对话框
        //(1) 事件源 事件被触发的对象   谁  按钮
        var btn = document.getElementById('btn');
        //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
        //(3) 事件处理程序  通过一个函数赋值的方式 完成
        btn.onclick = function () {
            alert('点秋香');
        }
    </script>
~~~

* 执行事件步骤：
  1. 获取事件源
  2. 注册事件(绑定事件)
  3. 添加事件处理程序(采用函数赋值形式)



### 2.4 操作元素

* Javascript 的 DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作元索来改变元素里面的内容、属性等。注意以下都是属性



**改变元素内容**

* element.innerText:从起始位置到终止位置的内容,**但它去除 html标签**，同时**空格和换行**也会去掉
* element.innerHTML:起始位置到终止位置的全部内容，**包括html 标签**，同时保留**空格和换行**
* 代码：

~~~html
	<button>显示当前系统时间</button>
    <div>某个时间</div>
    <p>1123</p>
    <script>
        // 当我们点击了按钮，  div里面的文字会发生变化
        // 1. 获取元素 
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        // 2.注册事件
        btn.onclick = function() {
            // div.innerText = '2019-6-6';
            div.innerHTML = getDate();
        }

        function getDate() {
            var date = new Date();
            // 我们写一个 2019年 5月 1日 星期三
            var year = date.getFullYear();
            var month = date.getMonth() + 1;
            var dates = date.getDate();
            var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            var day = date.getDay();
            return '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day];
        }
        // 3.我们元素可以不用添加事件
        var p = document.querySelector('p');
        p.innerHTML = getDate();
    </script>
~~~



**常见元素的属性操作**

1. innerText、innerHTML。改变元素内容
2. src、href
3. id、alt、title

* 代码：

~~~html
	<button id="ldh">刘德华</button>
    <button id="zxy">张学友</button> <br>
    <img src="images/ldh.jpg" alt="" title="刘德华">

    <script>
        // 修改元素属性  src
        // 1. 获取元素
        var ldh = document.getElementById('ldh');
        var zxy = document.getElementById('zxy');
        var img = document.querySelector('img');
        // 2. 注册事件  处理程序
        zxy.onclick = function () {
            img.src = 'images/zxy.jpg';
            img.title = '张学友';
        }
        ldh.onclick = function () {
            img.src = 'images/ldh.jpg';
            img.title = '刘德华';
        }
    </script>
~~~



**表单元素的属性操作**

* 利用DOM可以操作如下表单元素的属性:type、value、checked、selected、disabled

* 代码：

~~~html
	<button>按钮</button>
    <input type="text" value="输入内容">
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var input = document.querySelector('input');
        // 2. 注册事件 处理程序
        btn.onclick = function() {
            // input.innerHTML = '点击了';  这个是 普通盒子 比如 div 标签里面的内容
            // 表单里面的值 文字内容是通过 value 来修改的
            input.value = '被点击了';
            // 如果想要某个表单被禁用 不能再点击 disabled  我们想要这个按钮 button禁用
            // btn.disabled = true;
            this.disabled = true;
            // this 指向的是事件函数的调用者 btn
        }
    </script>
~~~

* 仿京东显示密码代码：

~~~html
	<div class="box">
        <label for="">
            <img src="images/close.png" alt="" id="eye">
        </label>
        <input type="password" name="" id="pwd">
    </div>
    <script>
        var eye = document.getElementById('eye');
        var pwd = document.getElementById('pwd');

        var flag = 0;
        eye.onclick = function () {
            if (flag == 0) {
                pwd.type = 'text';
                eye.scr = 'imagrs/open.png';
                flag = 1;
            } else {
                pwd.type = 'password';
                eye.scr = 'imagrs/close.png';
                flag = 0;
            }
        }
    </script>
~~~



**样式属性操作**

* 我们可以通过JS修改元素的大小、颜色、位置等样式。
  1. element.style 	行内样式操作
  2. element.className     类名样式操作

* 注意:
  1. JS里面的样式采取驼峰命名法比如fontsize、backgroundcolor
  2. JS修改style样式操作，产生的是行内样式，css权重比较高
  3. 如果样式修改较多，可以采取操作类名方式更改元紊样式
  4. class因为是个保留字，因此使用className来操作元素类名属性
  5. className会直接更改元素的类名，会覆盖原先的类名

* 代码：

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        // 1. 获取元素
        var div = document.querySelector('div');
        // 2. 注册事件 处理程序
        div.onclick = function () {
            // div.style里面的属性 采取驼峰命名法 
            this.style.backgroundColor = 'purple';
            this.style.width = '250px';
        }
    </script>
</body>

</html>
~~~

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        .change {
            background-color: purple;
            color: #fff;
            font-size: 25px;
            margin-top: 100px;
        }
    </style>
</head>


<body>
    <div class="first">文本</div>
    <script>
        // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
        var test = document.querySelector('div');
        test.onclick = function () {
            // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况
            // 3. 如果想要保留原先的类名，我们可以这么做 多类名选择器
            this.className = 'change';
            this.className = 'first change';
        }
    </script>
</body>

</html>
~~~



![在这里插入图片描述](https://img-blog.csdnimg.cn/166c8198de704e1791326a4e7d749f85.png#pic_center)




**排他思想**

* 如果有同—组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法:
  1. 所有元素全部清除样式（干掉其他人)
  2. 给当前元素设置样式(留下我自己)
  3. 注意顺序不能颠倒，首先干掉其他人，再设置自己

* 代码：

~~~html
	<button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1. 获取所有按钮元素
        var btns = document.getElementsByTagName('button');
        // btns得到的是伪数组  里面的每一个元素 btns[i]
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function() {
                // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
                for (var i = 0; i < btns.length; i++) {
                    btns[i].style.backgroundColor = '';
                }
                // (2) 然后才让当前的元素背景颜色为pink 留下我自己
                this.style.backgroundColor = 'pink';

            }
        }
        //2. 首先先排除其他人，然后才设置自己的样式 这种排除其他人的思想我们成为排他思想
    </script>
~~~



**自定义属性的操作**

1. 获取属性值
   * element.属性		获取属性值。
   * element.getAttribute('属性');
* 区别:
     * element.属性	获取**内置属性值(元素本身自带的属性)**
     * element.getAttribute ( '属性');	主要获得**自定义的属性(标准)我们程序员自定义的属性**

2. 设置属性值

   * element.属性=‘值’		设置内置属性值

   * element.setAttribute('属性'，'值");
* 区别:
     * element.属性	设置内置属性值
     * element.setAttribute ( '属性'); 主要设置自定义的属性(标准)

3. 移除属性
   * element.removeAttribute('属性')

* 代码：

~~~html
	<div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        // (1) element.属性
        console.log(div.id);
        //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思 我们程序员自己添加的属性我们称为自定义属性 index
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));
        
        // 2. 设置元素属性值
        // (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是class 不是className
        
        // 3 移除属性 removeAttribute(属性)    
        div.removeAttribute('index');
    </script>
~~~



**H5自定义属性**

* 自定义属性目的:是为了保存并使用数据； 有些数据可以保存到页面中而不用保存到数据库中
* 自定义属性获取是通过getAttribute( 属性)获取。
* 1.设置H5自定义属性
  * H5规定自定义属性 **data- **开头做为属性名并且赋值。比如<div data-index= "1”> < /div>；或者使用JS设置element.setAttribute( 'data-index’ ,2)

* 2.获取H5自定义属性
  * 兼容性获取	element.getAttribute( 'data-index’ );
  * H5新增element.dataset.index或者element.dataset['index' ] **ie 11才开始支持**

* 代码：

~~~html
	<div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));
        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);
        // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
~~~



### 2.5 节点操作

* 获取元素通常使用两种方式
  1. 利用DOM提供的方法获取元素 -- 逻辑性不强，繁琐
  2. 利用节点层级关系获取元素 -- 利用父子兄节点关系获取元素，逻辑性强，兼容性稍差



**节点概述**

* 网页中的所有内容都是节点(标签、属性、文本、注释等)，在DOM中，节点使用node 来表示
* HTML DOM树中的所有节点均可通过JavaScript进行访问，所有HTML元素(节点)均可被修改，也可以创建或删除
* 一般地，节点至少拥有**nodeType (节点类型)**、**nodeName(节点名称）**和**nodeValue(节点值)**这三个基本属性
* 元素节点    nodeType 为1
* 属性节点    nodeType 为2
* 文本节点    nodeType 为3 (文本节点包含文字、空格、换行等)
* 我们在实际开发中，节点操作主要操作的是元素节点



**节点层次**

* 利用DOM树可以把节点划分为不同的层级关系，常见的是父子兄层级关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/53f70a47a91b42c980dcea88ed87730b.png#pic_center)


* 1.父级节点 -- node.parentNode
  * parentNode属性可返回某节点的父节点，注意是**最近的一个父节点**
  * 如果指定的节点没有父节点则返回null

* 代码：

~~~html
	<div class="demo">
        <div class="box">
            <span class="erweima">×</span>
        </div>
    </div>

    <script>
        // 1. 父节点 parentNode
        var erweima = document.querySelector('.erweima');
        // var box = document.querySelector('.box');
        // 得到的是离元素最近的父级节点(亲爸爸) 如果找不到父节点就返回为 null
        console.log(erweima.parentNode);
    </script>
~~~



* 2.1子节点 -- parentNode.childNodes(标准)
  * parentNode.childNodes返回包含指定节点的子节点的集合，该集合为即时更新的集合
  * 注意:返回值里面包含了所有的子节点，包括元素节点，文本节点等
  * 如果只想要获得里面的元素节点，则需要专门处理。所以我们一般不提倡使用childNodes

* 2.2子节点 -- parentNode.children (非标准)
  * parentNode.children是一个只读属性，返回所有的子元素节点。**它只返回子元素节点，其余节点不返回**(这个是我们重点掌握的)
  * 虽然children是一个非标准，但是得到了各个浏览器的支持，因此我们可以放心使用

* 2.3子节点 -- parentNode.firstchild
  * firstChild返回第一个子节点，找不到则返回null。同样，也是包含所有的节点

* 2.4子节点 -- parentNode. lastChild
  * lastChild返回最后一个子节点，找不到则返回null。同样，也是包含所有的节点

* 2.5子节点 -- parentNode.firstElementChild
  * firstElementchild返回第一个子元素节点，找不到则返回null
  * 注意:这个方法有兼容性问题，IE9以上才支持

* 2.6子节点 -- parentNode . lastElementchild
  * lastElementchild返回最后一个子元素节点，找不到则返回null
  * 注意:这个方法有兼容性问题，IE9以上才支持



* 实际开发中，firstChild和lastChild包含其他节点，操作不方便，而firstElementChild和lastElementChild又有兼容性问题
  1．如果想要第一个子元素节点，可以使用**parentNode.chilren[0]**
  2．如果想要最后一个子元素节点，可以使用**parentNode.chilren[parentNode.chilren.length - 1]**



* 3.1兄弟节点 -- node.nextSibling
  * nextSibling返回当前元素的下一个兄弟元素节点，找不到则返回null。同样，也是包含所有的节点

* 3.2兄弟节点 -- node.previousSibling
  * previousSibling 返回当前元素上一个兄弟元素节点，找不到则返回null。同样，也是包含所有的节点

* 3.3兄弟节点 -- node.nextElementSibling
  * nextElementsibling返回当前元素下一个兄弟元素节点，找不到则返回null
  * 注意:这个方法有兼容性问题，IE9以上才支持

* 3.4兄弟节点 -- node.previousElementsibling
  * previousElementsibling返回当前元素上一个兄弟节点，找不到则返回null
  * 注意:这个方法有兼容性问题，IE9以上才支持

* 兼容性函数代码

~~~JavaScript
   function getNextElementSibling(element) {
      var el = element;
      while (el = el.nextSibling) {
        if (el.nodeType === 1) {
            return el;
        }
      }
      return null;
    }  
~~~



**创建节点**

* document.createElement ( "tagName " )
* document.createElement()方法创建由tagName 指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点



**添加节点**

* node. appendchild (child)
  * node.appendChild()方法将一个节点添加到指定父节点的子节点列表**末尾**。类似于css里面的after 伪元素

* node . insertBefore (child，指定元素)
  * node.insertBefore(）方法将一个节点添加到父节点的指定子节点**前面**。类似于css里面的 before伪元素  

* 代码：

~~~html
	<ul>
        <li>123</li>
    </ul>
    <script>
        // 1. 创建节点元素节点
        var li = document.createElement('li');
        // 2. 添加节点 node.appendChild(child)  node 父级  child 是子级 后面追加元素  类似于数组中的push
        var ul = document.querySelector('ul');
        ul.appendChild(li);
        // 3. 添加节点 node.insertBefore(child, 指定元素);
        var lili = document.createElement('li');
        ul.insertBefore(lili, ul.children[0]);
        // 4. 我们想要页面添加一个新的元素 ： 1. 创建元素 2. 添加元素
    </script>
~~~



**删除节点**

* node . removeChild (child)
  * node.removechild()方法从DOM中删除一个子节点，返回删除的节点
* 代码：

~~~html
	<button>删除</button>
    <ul>
        <li>熊大</li>
        <li>熊二</li>
        <li>光头强</li>
    </ul>
    <script>
        // 1.获取元素
        var ul = document.querySelector('ul');
        var btn = document.querySelector('button');
        // 2. 删除元素  node.removeChild(child)
        // ul.removeChild(ul.children[0]);
        // 3. 点击按钮依次删除里面的孩子
        btn.onclick = function() {
            if (ul.children.length == 0) {
                this.disabled = true;
            } else {
                ul.removeChild(ul.children[0]);
            }
        }
    </script>
~~~

* 阻止链接跳转需要添加javascript:void(0);或者javascript:;



**复制节点**

* node.cloneNode ( )

  * node.cloneNode()方法返回调用该方法的节点的一个副本。也称为克隆节点/拷贝节点

* 注意：
  1. 如果括号参数为**空或者为false**，则是**浅拷贝**，即只克隆复制节点本身，不克隆里面的子节点
  2. 如果括号参数为**true**，则是**深度拷贝**，会复制节点本身以及里面所有的子节点
* 代码：

~~~html
	<ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        // 1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
        // 2. node.cloneNode(true); 括号为true 深拷贝 复制标签复制里面的内容
        var lili = ul.children[0].cloneNode(true);
        ul.appendChild(lili);
    </script>
~~~



**三种动态创建元素区别**

* document.write ()
* element.innerHTML
* document.createElement ()

* 区别

  1. document.write 是直接将内容写入页面的内容流，**但是文档流执行完毕，则它会导致页面全部重绘**

  2. innerHTML是将内容写入某个DOM节点，不会导致页面全部重绘

  3. innerHTML创建多个元素效率更高(不要拼接字符串，采取数组形式拼接)，结构稍微复杂

  4. createElement ()创建多个元素效率稍低—点点，但是结构更清晰


* 总结:不同浏览器下, innerHTML效率要比creatElement高



### 2.6 DOM重点核心

* 关于dom操作，我们主要针对于元素的操作。主要有创建、增、删、改、查、属性操作、事件操作



**创建**

1. document.write
2. innerHTML
3. createElement



**增**

1. appendChild
2. insertBefore



**删**

1. removeChild



**改**

* 主要修改dom的元素属性。dom元素的内容、属性,表单的值等
  1. 修改元素属性:src. href、 title等
  2. 修改普通元素内容:innerHTML . innerText
  3. 修改表单元索:value. type.disabled等
  4. 修改元素样式:style. className



**查**

* 主要获取查询dom的元素
  1. DOM提供的API方法: getElementByld.getElementsByTagName 古老用法不太推荐
  2. H5提供的新方法: querySelector.querySelectorAll提倡
  3. 利用节点操作获取元素:父(parentNode)、子(children)、兄(previousElementSibling、nextElementsibling)提倡



**属性操作**

* 主要针对于自定义属性
  1. setAttribute:设置dom的属性值
  2. getAttribute:得到dom的属性值
  3. removeAttribute移除属性



**事件操作**

* 给元素注册事件,采取事件源.事件类型=事件处理程序



## 3、DOM -- 事件高级

  ### 3.1 注册事件(绑定事件)

**注册事件**

* 给元素添加事件，称为注册事件或者绑定事件，注册事件有两种方式:
  1. 传统注册方式
     * 利用on开头的事件：onclick
     * 注册事件的唯一性
     * 同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数
  2. 方法监听注册方式
     * addEventListener()它是一个方法
     * 特点:同一个元素同一个事件可以注册多个监听器；按注册顺序依次执行



**addEventListener 事件监听方式** 

* eventTarget.addEventListener(type, listener[, useCapture]) 

* type:事件类型字符串，比如click 、mouseover，注意这里**不要带on**
* listener:事件处理函数，事件发生时，会调用该监听函数
* useCapture:可选参数，是一个布尔值，默认是false



**attachEvent 事件监听方式** (IE8及早期版本支持)

* eventTarget.attachEvent(eventNameWithOn, callback) 

* eventNameWithOn:事件类型字符串，比如onclick 、onmouseover，这里要**带 on**
* callback:事件处理函数，当目标触发事件时回调函数被调

* 代码：

~~~html
	<button>传统注册事件</button>
    <button>方法监听注册事件</button>
    <button>ie9 attachEvent</button>
    <script>
        var btns = document.querySelectorAll('button');
        // 1. 传统方式注册事件
        btns[0].onclick = function () {
            alert('hi');
        }
        btns[0].onclick = function () {
            alert('hao a u');
        }
        // 2. 事件侦听注册事件 addEventListener 
        // (1) 里面的事件类型是字符串 必定加引号 而且不带on
        // (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click', function () {
            alert(22);
        })
        btns[1].addEventListener('click', function () {
            alert(33);
        })
        // 3. attachEvent ie9以前的版本支持
        btns[2].attachEvent('onclick', function () {
            alert(11);
        })
    </script>
~~~



**注册事件兼容性解决方案** 

* 代码：

~~~javascript
 function addEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 addEventListener 方法
      if (element.addEventListener) {
        element.addEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.attachEvent) {
        element.attachEvent('on' + eventName, fn);
      } else {
        // 相当于 element.onclick = fn;
        element['on' + eventName] = fn;
 } 
~~~



### 3.2 删除事件(解绑事件)

1. 传统注册方式
   * eventTarget.onclick = null;

2. 方法监听注册方式
   * ①eventTarget.removeEventListener(type, listener[, useCapture]);
   * ②eventTarget.detachEvent(eventNameWithOn, callback);

* 代码：

~~~html
	<div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        var divs = document.querySelectorAll('div');
        divs[0].onclick = function() {
                alert(11);
                // 1. 传统方式删除事件
                divs[0].onclick = null;
            }
            // 2. removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号

        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn);
        }
        // 3. detachEvent
        divs[2].attachEvent('onclick', fn1);

        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick', fn1);
        }
    </script>
~~~



**删除事件兼容性解决方案** 

~~~JavaScript
 function removeEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 removeEventListener 方法
      if (element.removeEventListener) {
        element.removeEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.detachEvent) {
        element.detachEvent('on' + eventName, fn);
      } else {
        element['on' + eventName] = null;
 } 
~~~



### 3.3 DOM事件流

* 事件流描述的是从页面中接收事件的顺序
* 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

![在这里插入图片描述](https://img-blog.csdnimg.cn/e97d2e84b8d34d88825ac9bcff55b416.png#pic_center)


* DOM事件流分为3个阶段:
  1. 捕获阶段
  2. 当前目标阶段
  3. 冒泡阶段

* **事件冒泡**:IE最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到DOM最顶层节点的过程(回溯)
* **事件捕获**:网景最早提出，由DOM最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程(自顶向下)

* 举例：我们向水里面扔一块石头，首先它会有一个下降的过程，这个过程就可以理解为从最顶层向事件发生的最具体元素（目标点)的捕获过程;之后会产生泡泡，会在最低点（最具体元素)之后漂浮到水面上，这个过程相当于事件冒泡

* **事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流**
* 注意
  1. JS 代码中只能执行捕获或者冒泡其中的一个阶段
  2. onclick和attachEvent只能得到冒泡阶段
  3. addEventListener(type,listener[,useCapture])第三个参数如果是**true**，表示在事件**捕获阶段调用事件处理程序**;如果是 **false (不写默认就是false)**，表示在事件**冒泡阶段调用事件处理程序**
  4. 实际开发中我们很少使用事件捕获，我们更关注事件冒泡
  5. 有些事件是没有冒泡的，比如onblur、onfocus、onmouseenter、onmouseleave

* 代码：

~~~html
	<div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // dom 事件流 三个阶段
        // 1. JS 代码中只能执行捕获或者冒泡其中的一个阶段。
        // 2. onclick 和 attachEvent（ie） 只能得到冒泡阶段。
        // 3. 捕获阶段 如果addEventListener 第三个参数是 true 那么则处于捕获阶段  document -> html -> body -> father -> son
        // var son = document.querySelector('.son');
        // son.addEventListener('click', function() {
        //     alert('son');
        // }, true);
        // var father = document.querySelector('.father');
        // father.addEventListener('click', function() {
        //     alert('father');
        // }, true);
        // 4. 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 那么则处于冒泡阶段  son -> father ->body -> html -> document
        var son = document.querySelector('.son');
        son.addEventListener('click', function () {
            alert('son');
        }, false);
        var father = document.querySelector('.father');
        father.addEventListener('click', function () {
            alert('father');
        }, false);
        document.addEventListener('click', function () {
            alert('document');
        })
    </script>
~~~



### 3.4 事件对象

~~~JavaScript
  eventTarget.onclick = function(event) {} 
  eventTarget.addEventListener('click', function(event) {}）
  // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt 
~~~

* 官方解释: event对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态
* 代码：

~~~html
	<div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        div.onclick = function (e) {
            // console.log(e);
            // console.log(window.event);
            // e = e || window.event;
            //事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;
            console.log(e);
        }
    </script>
~~~



**事件对象的常见属性和方法**

| 事件对象属性方法  |                             说明                             |
| :---------------: | :----------------------------------------------------------: |
|     e.target      |                  返回触发事件的对象    标准                  |
|   e.srcElement    |           返回触发事件的对象    非标准  ie6-8使用            |
|      e.type       |        返回事件的类型    比如click  mouseover  不带on        |
|  e.cancelBubble   |               该属性阻止冒泡 非标准 ie6-8使用                |
|   e.returnValue   | 该方法阻止默认事件(默认行为)    非标准  ie6-8使用  比如不让链接跳转 |
| e.preventDefault  |    该方法阻止默认事件(默认行为)    标准  比如不让链接跳转    |
| e.stopPropagation |                       阻止冒泡    标准                       |



**target与this**

~~~html
	<div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 常见事件对象的属性和方法
        // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
        // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            console.log(e.target);
            console.log(this);

        })
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
                // 我们给ul 绑定了事件  那么this 就指向ul  
                console.log(this);
                console.log(e.currentTarget);

                // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
                console.log(e.target);

            })
            // 了解兼容性
            // div.onclick = function(e) {
            //     e = e || window.event;
            //     var target = e.target || e.srcElement;
            //     console.log(target);

        // }
        // 2. 了解 跟 this 有个非常相似的属性 currentTarget  ie678不认识
    </script>
~~~



**返回事件类型和阻止默认行为**

~~~html
	<div>123</div>
    <a href="http://www.baidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function (e) {
            e.preventDefault(); //  dom 标准写法
        })
        // 3. 传统的注册方式
        a.onclick = function (e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);
        }
    </script>
~~~



**阻止事件冒泡**

* 标准写法:利用事件对象里面的stopPropagation()方法
  * e.stopPropagation ()
* 非标准写法:IE 6-8利用事件对象cancelBubble 属性
  * e.cancelBubble = true;

* 代码：

~~~html
	<div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        // 常见事件对象的属性和方法
        // 阻止冒泡  dom 推荐的标准 stopPropagation() 
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // stop 停止  Propagation 传播
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false);

        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
        document.addEventListener('click', function() {
            alert('document');
        })
    </script>
~~~

* 阻止事件冒泡的兼容性解决方案 

~~~javascript
if(e && e.stopPropagation){
      e.stopPropagation();
  }else{
      window.event.cancelBubble = true;
  }
~~~



### 3.5 事件委托

* 事件委托也称为事件代理，在jQuery里面称为事件委派
* 事件委托的原理：不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点
* 事件委托的作用：我们只操作了一次DOM，提高了程序的性能

* 代码：

~~~html
	<ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function (e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
        })
    </script>
~~~





### 3.6 常用事件

**常见的鼠标事件**

|  鼠标事件   |     触发条件     |
| :---------: | :--------------: |
|   onclick   | 鼠标点击左键触发 |
| onmouseover |   鼠标经过触发   |
| onmouseout  |   鼠标离开触发   |
|   onfocus   | 获得鼠标焦点触发 |
|   onblur    | 失去鼠标焦点触发 |
| onmousemove |   鼠标移动触发   |
|  onmouseup  |   鼠标弹起触发   |
| onmousedown |   鼠标按下触发   |

* 禁止鼠标右键菜单
  * contextmenu主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单

~~~JavaScript
document.addEventListener('contextmenu', function(e) {
	e.preventDefault();
})
~~~

* 禁止鼠标选中（selectstart 开始选中）

~~~JavaScript
document.addEventListener('selectstart', function(e) {
	e.preventDefault();
})
~~~



**鼠标事件对象**

* event对象代表事件的状态，跟事件相关的一系列信息的集合。现阶段我们主要是用鼠标事件对象MouseEvent和键盘事件对象KeyboardEvent

| 鼠标事件对象 |                   说明                    |
| :----------: | :---------------------------------------: |
|  e.clientX   |   返回鼠标相对于浏览器窗口可视区的X坐标   |
|  e.clientY   |   返回鼠标相对于浏览器窗口可视区的Y坐标   |
|   e.pageX    | 返回鼠标相对于文档页面的X坐标    IE9+支持 |
|   e.pageY    | 返回鼠标相对于文档页面的Y坐标    IE9+支持 |
|  e.screenX   |       返回鼠标相对于电脑屏幕的X坐标       |
|  e.screenY   |       返回鼠标相对于电脑屏幕的Y坐标       |

* 代码：

~~~html
	<script>
        // 鼠标事件对象 MouseEvent
        document.addEventListener('click', function(e) {
            // 1. client 鼠标在可视区的x和y坐标
            console.log(e.clientX);
            console.log(e.clientY);
            console.log('---------------------');

            // 2. page 鼠标在页面文档的x和y坐标
            console.log(e.pageX);
            console.log(e.pageY);
            console.log('---------------------');

            // 3. screen 鼠标在电脑屏幕的x和y坐标
            console.log(e.screenX);
            console.log(e.screenY);

        })
    </script>
~~~



**常用键盘事件**

|  键盘事件  |                 触发条件                 |
| :--------: | :--------------------------------------: |
|  onkeyup   |         某个键盘按键被松开时触发         |
| onkeydown  |         某个键盘按键被按下时触发         |
| onkeypress | 某个键盘按键被松开时触发    不识别功能键 |

* 代码：

~~~html
	<script>
        // 常用的键盘事件
        //1. keyup 按键弹起的时候触发 
        // document.onkeyup = function() {
        //         console.log('我弹起了');

        //     }
        document.addEventListener('keyup', function () {
            console.log('我弹起了');
        })

        //3. keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keypress', function () {
            console.log('我按下了press');
        })
        //2. keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keydown', function () {
            console.log('我按下了down');
        })
    </script>
~~~

* 注意:

  1. 如果使用addEventListener不需要加on

  2. onkeypress和前面2个的区别是，它不识别功能键，比如左右箭头,shift等
  3. 三个事件的执行顺序是: **keydown -- keypress --- keyup**





**键盘事件对象**

* keyCode -- 返回该键的ASCII值



* 代码：

~~~html
	<script>
        // 键盘事件对象中的keyCode属性可以得到相应键的ASCII码值
        // 1. 我们的keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
        // 2. 我们的keypress 事件 区分字母大小写  a  97 和 A 得到的是65
        document.addEventListener('keyup', function(e) {
            // console.log(e);
            console.log('up:' + e.keyCode);
            // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
            if (e.keyCode === 65) {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }

        })
        document.addEventListener('keypress', function(e) {
            // console.log(e);
            console.log('press:' + e.keyCode);

        })
    </script>
~~~

* 注意:onkeydown和onkeyup 不区分字母大小写，onkeypress区分字母大小写

 

## 4、BOM

### 4.1 BOM概述

* BOM (Browser Object Model）即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是window
* BOM缺乏标准，JavaScript语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape浏览器标准的一部分

|              DOM               |                       BOM                       |
| :----------------------------: | :---------------------------------------------: |
|          文档对象模型          |                 浏览器对象模型                  |
| 把**[文档]**当做一个**[对象]** |        把**[浏览器]**当做一个**[对象]**         |
|    DOM的顶级对象是document     |            BOM的顶级对象是**window**            |
|  DOM主要学习的是操作页面元素   |        BOM学习的是浏览窗口交互的一些对象        |
|        DOM是W3C标准规范        | BOM是浏览器厂商在各自浏览器上定义的，兼容性较差 |

* 构成

![在这里插入图片描述](https://img-blog.csdnimg.cn/2170a0df0205446c9a130f2832769af1.png#pic_center)


* window对象是浏览器的顶级对象，它具有双重角色。

  1. 它是JS访问浏览器窗口的一个接口

  2. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成window对象的属性和方法

* 在调用的时候可以省略window，前面学习的对话框都属于window对象方法，如 alert()、prompt()等
* **注意: window下的一个特殊属性window.name(变量不要声明为name)**



### 4.2 windows对象的常见事件

**窗口加载事件**

* **window.onload 是窗口(页面)加载事件,当文档内容完全加载完成会触发该事件(包括图像、脚本文件、CSS文件等),就调用的处理函数**
* 注意:
  1. 有了window.onload就可以把JS代码写到页面元素的上方，因为onload 是等页面内容全部加载完毕，再去执行处理函数
  2. window.onload传统注册事件方式只能写一次，如果有多个，会以最后一个window.onload为准
  3. 如果使用addEventListener则没有限制
* DOMContentLoaded事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等。(le9以上才支持)如果页面的图片很多的话,从用户访问到onload触发可能需要较长的时间,交互效果就不能实现，必然影响用户的体验，此时用DOMContentLoaded事件比较合适

* 代码：

~~~html
	<script>
        window.addEventListener('load', function () {
            var btn = document.querySelector('button');
            btn.addEventListener('click', function () {
                alert(11);
            })
        })
        window.addEventListener('load', function () {
            alert(22);
        })
        document.addEventListener('DOMContentLoaded', function () {
            alert(33);
        })
            // load 等页面内容全部加载完毕，包含页面dom元素 图片 flash  css 等等
            // DOMContentLoaded 是DOM 加载完毕，不包含图片 falsh css 等就可以执行 加载速度比 load更快一些
    </script>
~~~



**调整窗口大小事件**

* **window. onresize是调整窗口大小加载事件，当触发时就调用的处理函数**
* 注意:
  1. 只要窗口大小发生像索变化，就会触发这个事件
  2. 我们经常利用这个事件完成响应式布局。window.innerWidth当前屏慕的宽度

* 代码：

~~~html
	<script>
        window.addEventListener('load', function () {
            var div = document.querySelector('div');
            window.addEventListener('resize', function () {
                console.log(window.innerWidth);

                console.log('变化了');
                if (window.innerWidth <= 800) {
                    div.style.display = 'none';
                } else {
                    div.style.display = 'block';
                }

            })
        })
    </script>
~~~



### 4.3 定时器

**setTimeout()定时器**

* **window.setTimeout(调用函数, [延迟的毫秒数]);**
* setTimeout()方法用于设置一个定时器，该定时器在定时器到期后执行调用函数
* setTimeout()这个调用函数我们也称为**回调函数callback**；普通函数是按照代码顺序直接调用，而这个函数，需要等待时间，时间到了才去调用这个函数，因此称为回调函数
* 注意:
  1. window可以省略
  2. 这个调用函数可以直接写函数，或者写函数名或者采取字符串‘函数名0'三种形式。第三种不推荐
  3. 延迟的毫秒数省略默认是0。如果写，必须是毫秒
  4. 因为定时器可能有很多。所以我们经常给定时器赋值一个标识符

* 代码：

~~~html
	<script>
        function callback() {
            console.log('爆炸了');

        }
        var timer1 = setTimeout(callback, 3000);
        var timer2 = setTimeout(callback, 5000);
        // setTimeout('callback()', 3000); // 我们不提倡这个写法
    </script>
~~~

~~~html
	//广告自动关闭
	<img src="images/ad.jpg" alt="" class="ad">
    <script>
        var ad = document.querySelector('.ad');
        setTimeout(function() {
            ad.style.display = 'none';
        }, 5000);
    </script>
~~~



**停止setTimeout()定时器**

* window.clearTimeout(timeoutID)；
* clearTimeout ()方法取消了先前通过调用setTimeout(〉建立的定时器
* 注意:
  1. window可以省略
  2. 里面的参数就是定时器的标识符

* 代码：

~~~html
	<button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
        var timer = setTimeout(function() {
            console.log('爆炸了');

        }, 5000);
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
    </script>
~~~



**setInterval()定时器**

*  window.setInterval(回调函数, [间隔的毫秒数]);
* setinterval0方法重复调用一个函数。每限这个时间，就去调用一次回调函数
* 注意基本同setTimeout()定时器
* 代码：

~~~html
	<script>
        setInterval(function () {
            console.log('继续输出');
        }, 1000);
    </script>
~~~

~~~html
	//定时器
	<div>
        <span class="hour">1</span>
        <span class="minute">2</span>
        <span class="second">3</span>
    </div>
    <script>
        // 1. 获取元素 
        var hour = document.querySelector('.hour'); // 小时的黑色盒子
        var minute = document.querySelector('.minute'); // 分钟的黑色盒子
        var second = document.querySelector('.second'); // 秒数的黑色盒子
        var inputTime = +new Date('2022-5-6 12:00:00'); // 返回的是用户输入时间总的毫秒数
        countDown(); // 我们先调用一次这个函数，防止第一次刷新页面有空白 
        // 2. 开启定时器
        setInterval(countDown, 1000);

        function countDown() {
            var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
            var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
            var h = parseInt(times / 60 / 60 % 24); //时
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h; // 把剩余的小时给 小时黑色盒子
            var m = parseInt(times / 60 % 60); // 分
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;
            var s = parseInt(times % 60); // 当前的秒
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;
        }
    </script>
~~~



**停止setInterval()定时器**

* window.clearInterval(intervalID);
* clearInterval()方法取消了先前通过调用setInterval()建立的定时器
* 注意:基本同停止setTimeout()定时器
* 代码：

~~~html
	<button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var timer = null; // 全局变量  null是一个空对象
        begin.addEventListener('click', function () {
            timer = setInterval(function () {
                console.log('你好');
            }, 1000);
        })
        stop.addEventListener('click', function () {
            clearInterval(timer);
        })
    </script>
~~~

~~~html
	//发送短信
	手机号码:<input type="number"><button>发送</button>
	<script>
    	var btn = document.querySelector('button');
    	var time = 5;
    	btn.addEventListener('click', function () {
        	btn.disabled = true;
        	var timer = setInterval(function () {
            	if (time == 0) {
                	clearInterval(timer);
                	btn.disabled = false;
                	btn.innerHTML = '发送';
                	time = 5;
            	} else {
                	btn.innerHTML = '还剩下' + time + '秒';
                	time--;
            	}
        	}, 1000)
    	})
	</script>
~~~



**this**

* this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，一般情况下**this的最终指向的是那个调用它的对象**
  1. **全局作用域或者普通函数**中this**指向全局对象window** (注意定时器里面的this指向window)
  2. **方法调用中谁调用this指向谁**
  3. **构造函数中this**指向**构造函数的实例**



### 4.4 JS执行机制

* JavaScript语言的一大特点就是单线程，也就是说，**同一个时间只能做一件事**
* 这是Javascript这门脚本语言诞生的使命所致——JavaScript是为处理页面中用户的交互，以及操作DOM而诞生的。比如我们对某个DOM元素进行添加和删除操作，不能同时进行。应该先进行添加，之后再删除



**同步和异步**

* 为了解决这个问题，利用多核CPU的计算能力，HTML5提出 Web Worker标准，允许JavaScript脚本创建多个线程。于是，JS中出现了同步和异步
* 本质区别:这条流水线上各个流程的执行顺序不同
* 同步任务：同步任务都在主线程上执行，形成一个**执行栈**
* 异步任务：JS的异步是通过回调函数实现的
* —般而言，异步任务有以下三种类型:
  1. **普通事件**，如click、resize等
  2. **资源加载**，如load、error等
  3. **定时器**，包括setlnterval、setTimeout等
* 异步任务相关回调函数添加到**任务队列**中(任务队列也称为消息队列)。



**执行机制**

1. **先执行执行栈中的同步任务**
2. **异步任务(回调函数）放入任务队列中**
3. **一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行**



![在这里插入图片描述](https://img-blog.csdnimg.cn/c978f93f1e6443d780a05ba9e510fed0.png#pic_center)


* **由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为事件循环（event loop)**

* 代码：

~~~html
	<script>
        // 第一个问题
        // console.log(1);
        // setTimeout(function () {
        //     console.log(3);
        // }, 1000);
        // console.log(2);
        // 2. 第二个问题
        // console.log(1);
        // setTimeout(function () {
        //     console.log(3);
        // }, 0);
        // console.log(2);
        // 3. 第三个问题
        console.log(1);
        document.onclick = function () {
            console.log('click');
        }
        console.log(2);
        setTimeout(function () {
            console.log(3)
        }, 3000)
    </script>
~~~



### 4.5 location对象

* window对象给我们提供了一个**location属性**用于**获取或设置窗体的URL**，并且可以用于解析URL。因为这个属性返回的是一个对象，所以我们将这个属性也称为**location对象**



**UPL**

* 统一资源定位符(Uniform Resource Locator,URL)是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它

* 一般格式：

  *  protocol://host[:port]/path/[?query]#fragment

     http://www.itcast.cn/index.html?name=andy&age=18#link

|   组成   |                             说明                             |
| :------: | :----------------------------------------------------------: |
| protocol |               通信协议 常用的http,ftp.maito等                |
|   host   |                  主机（域名） www.baidu.com                  |
|   port   |            端口号 可选，省略时使用方案的默认端口             |
|   path   | 路径 由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
|  query   |            参数 以键值对的形式，通过&符号分隔开来            |
| fragment |                片段 #后面内容 常见于链接 锚点                |



**location对象的属性**

| location对象属性  |              返回值              |
| :---------------: | :------------------------------: |
|   location.href   |       获取或者设置 整个URL       |
|   location.host   |   返回主机(域名) www.bandu.com   |
|   location.port   | 返回端口号 如果未写返回 空字符串 |
| location.pathname |             返回路径             |
|  location.search  |             返回参数             |
|   location.hash   |             返回片段             |

* 代码：

~~~html
	<button>点击</button>
    <div></div>
    <script>
        var btn = document.querySelector('button');
        var div = document.querySelector('div');
        btn.addEventListener('click', function () {
            // console.log(location.href);
            location.href = 'http://www.baidu.com';
        })
        var timer = 5;
        setInterval(function () {
            if (timer == 0) {
                location.href = 'http://www.baidu.com';
            } else {
                div.innerHTML = '您将在' + timer + '秒钟之后跳转到首页';
                timer--;
            }

        }, 1000);
    </script>
~~~



**location对象的方法**

|  location对象方法  |                            返回值                            |
| :----------------: | :----------------------------------------------------------: |
| location.assign()  |         跟href一样，可以跳转页面（(也称为重定向页面)         |
| location.replace() |      替换当前页面，因为**不记录历史**，所以不能后退页面      |
| location.reload()  | 重新加载页面，相当于刷新按钮或者f5如果参数为true 强制刷新ctrl+f5 |

* 代码：

~~~html
	<button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            // 记录浏览历史，所以可以实现后退功能
            // location.assign('http://www.baidu.com');
            // 不记录浏览历史，所以不可以实现后退功能
            // location.replace('http://www.baidu.com');
            location.reload(true);
        })
    </script>
~~~



### 4.6 navigator对象

* navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值
* 判断终端

~~~JavaScript
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
} else {
    window.location.href = "";     //电脑
}

~~~



### 4.7 history对象

* window对象给我们提供了一个history对象，与浏览器历史记录进行交互。该对象包含用户(在浏览器窗口中)访问过的 URL

| history对象方法 |                       作用                       |
| :-------------: | :----------------------------------------------: |
|     back()      |                     后退功能                     |
|    forword()    |                     前进功能                     |
|    go(参数)     | 前进后退功能，参数为1前进1个页面，-1后退一个页面 |

* 代码：

~~~html
	//index.html
	<a href="list.html">点击我去往列表页</a>
    <button>前进</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // history.forward();
            history.go(1);
        })
    </script>

	//list.html
	<a href="index.html">点击我去往首页</a>
    <button>后退</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // history.back();
            history.go(-1);
        })
    </script>
~~~



## 5、PC端网页特效

### 5.1 元素偏移量offset系列

* offset翻译过来就是偏移量，我们使用offset系列相关属性可以**动态的**得到该元素的位置（偏移)、大小等
* 获得元素距离带有定位父元素的位置
* 获得元素自身的大小(宽度高度)
* 注意:返回的数值都不带单位

![在这里插入图片描述](https://img-blog.csdnimg.cn/654c5b89096b418fb8e42df119960af9.png#pic_center)


* offset常见属性：

|    offset系列属性    |                             作用                             |
| :------------------: | :----------------------------------------------------------: |
| element.offsetParent | 返回作为该元素带有定位的父级元素，如果父级都没有定位则返回body |
|  element.offsetTop   |             返回元素相对带有定位父元素上方的偏移             |
|  element.offsetLeft  |            返回元素相对带有定位父元素左边框的偏移            |
| element.offsetWidth  |  返回自身包括padding、边框、内容区的宽度、返回数值不带单位   |
| element.offsetHeight |  返回自身包括padding、边框、内容区的高度、返回数值不带单位   |

* 代码：

~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .father {
            /* position: relative; */
            width: 200px;
            height: 200px;
            background-color: pink;
            margin: 150px;
        }

        .son {
            width: 100px;
            height: 100px;
            background-color: purple;
            margin-left: 45px;
        }

        .w {
            height: 200px;
            background-color: skyblue;
            margin: 0 auto 200px;
            padding: 10px;
            border: 15px solid red;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
    <div class="w"></div>
    <script>
        // offset 系列
        var father = document.querySelector('.father');
        var son = document.querySelector('.son');
        // 1.可以得到元素的偏移 位置 返回的不带单位的数值  
        console.log(father.offsetTop);
        console.log(father.offsetLeft);
        // 它以带有定位的父亲为准  如果么有父亲或者父亲没有定位 则以 body 为准
        console.log(son.offsetLeft);
        var w = document.querySelector('.w');
        // 2.可以得到元素的大小 宽度和高度 是包含padding + border + width 
        console.log(w.offsetWidth);
        console.log(w.offsetHeight);
        // 3. 返回带有定位的父亲 否则返回的是body
        console.log(son.offsetParent); // 返回带有定位的父亲 否则返回的是body
        console.log(son.parentNode); // 返回父亲 是最近一级的父亲 亲爸爸 不管父亲有没有定位
    </script>
</body>

</html>
~~~



**offset与style的区别**

|                     offset                     |                    style                     |
| :--------------------------------------------: | :------------------------------------------: |
|       offset可以得到任意样式表中的样式值       |      style只能得到行内样式表中的样式值       |
|      offset系列获得的数值是**没有单位**的      |   style.width获得的是带**有单位的**字符串    |
|    offsetWidth 包含**padding+border+width**    | style.width获得**不包含padding和border**的值 |
| offsetWidth 等属性是只读属性，只能获取不能赋值 | style.width是可读写属性，可以获取也可以赋值  |
|      **获取**元素大小位置、用offset更合适      |     想要给元素**更改**值，则需要用style      |

* 代码：

~~~html
	//获取鼠标在盒子内的坐标
	<script>
        // 我们在盒子内点击， 想要得到鼠标距离盒子左右的距离。
        // 首先得到鼠标在页面中的坐标（ e.pageX, e.pageY）
        // 其次得到盒子在页面中的距离(box.offsetLeft, box.offsetTop)
        // 用鼠标距离页面的坐标减去盒子在页面中的距离， 得到 鼠标在盒子内的坐标
        var box = document.querySelector('.box');
        box.addEventListener('mousemove', function (e) {
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            this.innerHTML = 'x坐标是' + x + ' y坐标是' + y;
        })
    </script>
~~~



### 5.2 元素可视区client系列

* client翻译过来就是客户端，我们使用client系列的相关属性来获取元素可视区的相关信息。![在这里插入图片描述](https://img-blog.csdnimg.cn/efbb85b3dbec46c6b2cab0e84f786259.png#pic_center)
通过client 系列的相关属性可以动态的得到该元素的边框大小、元素大小等



|    client系列属性    |                             作用                             |
| :------------------: | :----------------------------------------------------------: |
|  element.clientTop   |                     返回元素上边框的大小                     |
|  element.clientLeft  |                     返回元素左边框的大小                     |
| element.clientWidth  | 返回自身包括padding 、内容区的宽度，**不含边框**，返回数值不带单位 |
| element.clientHeight | 返回自身包括padding 、内容区的高度，**不含边框**，返回数值不带单位 |



**立即执行函数**

* 立即执行函数**(function() {})()**或者**(function(){}())**
* 主要作用:创建一个独立的作用域；避免了命名冲突问题
* 代码：

~~~html
	<script>
        // 1.立即执行函数: 不需要调用，立马能够自己执行的函数
        function fn() {
            console.log(1);
        }
        fn();
        // 2. 写法 也可以传递参数进来
        // 1.(function() {})()    或者  2. (function(){}());
        (function (a, b) {
            console.log(a + b);
            var num = 10;
        })(1, 2); // 第二个小括号可以看做是调用函数
        (function sum(a, b) {
            console.log(a + b);
            var num = 10; // 局部变量
        }(2, 3));
        // 3. 立即执行函数最大的作用就是 独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况
    </script>
~~~



**flexible.js源码分析**

* 代码：

~~~JavaScript
(function flexible(window, document) {
    // 获取的html 的根元素
    var docEl = document.documentElement
    // dpr 物理像素比
    var dpr = window.devicePixelRatio || 1

    // adjust body font size  设置我们body 的字体大小
    function setBodyFontSize() {
        // 如果页面中有body 这个元素 就设置body的字体大小
        if (document.body) {
            document.body.style.fontSize = (12 * dpr) + 'px'
        } else {
            // 如果页面中没有body 这个元素，则等着 我们页面主要的DOM元素加载完毕再去设置body
            // 的字体大小
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
    setBodyFontSize();

    // set 1rem = viewWidth / 10    设置我们html 元素的文字大小
    function setRemUnit() {
        var rem = docEl.clientWidth / 10
        docEl.style.fontSize = rem + 'px'
    }

    setRemUnit()

    // reset rem unit on page resize  当我们页面尺寸大小发生变化的时候，要重新设置下rem 的大小
    window.addEventListener('resize', setRemUnit)
    // pageshow 是我们重新加载页面触发的事件
    window.addEventListener('pageshow', function (e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem 的大小
        if (e.persisted) {
            setRemUnit()
        }
    })

    // detect 0.5px supports  有些移动端的浏览器不支持0.5像素的写法
    if (dpr >= 2) {
        var fakeBody = document.createElement('body')
        var testElement = document.createElement('div')
        testElement.style.border = '.5px solid transparent'
        fakeBody.appendChild(testElement)
        docEl.appendChild(fakeBody)
        if (testElement.offsetHeight === 1) {
            docEl.classList.add('hairlines')
        }
        docEl.removeChild(fakeBody)
    }
}(window, document))
~~~

* 下面三种情况都会刷新页面都会触发load 事件
  1. a标签的超链接
  2. F5或者刷新按钮(强制刷新)
  3. 前进后退按钮
* 但是火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态;实际上是将整个页面都保存在了内存里；所以此时后退按钮不能刷新页面
* 此时可以使用pageshow事件来触发，这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页面中，pageshow会在load事件触发后触发;根据事件对象中的persisted来判断是否是缓存中的页面触发的pageshow事件，注意这个事件给window添加



### 5.3 元素滚动scroll系列

* scroll翻译过来就是滚动的，我们使用scroll系列的相关属性可以动态的得到该元素的大小、滚动距离等

![在这里插入图片描述](https://img-blog.csdnimg.cn/83996f6f97db43dc837f5355ba75b3a4.png#pic_center)

|    scroll系列属性    |                        作用                        |
| :------------------: | :------------------------------------------------: |
|  element.scrollTop   |       返回被卷去的上侧距离，返回数值不带单位       |
|  element.scrollLeft  |       返回被卷去的左侧距离，返回数值不带单位       |
| element.scrollWidth  | 返回自身内容实际的宽度、不含边框、返回数值不带单位 |
| element.scrollHeight | 返回自身内容实际的高度、不含边框、返回数值不带单位 |

* 代码：

~~~html
//仿淘宝侧边栏
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .slider-bar {
            position: absolute;
            left: 50%;
            top: 300px;
            margin-left: 600px;
            width: 45px;
            height: 130px;
            background-color: pink;
        }

        .w {
            width: 1200px;
            margin: 10px auto;
        }

        .header {
            height: 150px;
            background-color: purple;
        }

        .banner {
            height: 250px;
            background-color: skyblue;
        }

        .main {
            height: 1000px;
            background-color: yellowgreen;
        }

        span {
            display: none;
            position: absolute;
            bottom: 0;
        }
    </style>
</head>

<body>
    <div class="slider-bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体部分</div>
    <script>
        //1. 获取元素
        var sliderbar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        // banner.offestTop 就是被卷去头部的大小 一定要写到滚动的外面
        var bannerTop = banner.offsetTop
        // 当我们侧边栏固定定位之后应该变化的数值
        var sliderbarTop = sliderbar.offsetTop - bannerTop;
        // 获取main 主体元素
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');
        var mainTop = main.offsetTop;
        // 2. 页面滚动事件 scroll
        document.addEventListener('scroll', function () {
            // 3 .当我们页面被卷去的头部大于等于了 172 此时 侧边栏就要改为固定定位
            if (window.pageYOffset >= bannerTop) {
                sliderbar.style.position = 'fixed';
                sliderbar.style.top = sliderbarTop + 'px';
            } else {
                sliderbar.style.position = 'absolute';
                sliderbar.style.top = '300px';
            }
            // 4. 当我们页面滚动到main盒子，就显示 goback模块
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }
        })
    </script>
</body>

</html>
~~~



**页面被卷去的头部兼容性解决**

* 如果浏览器的高（或宽)度不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面上面被隐藏掉的高度，我们就称为页面被卷去的头部。滚动条在滚动时会触发onscroll事件
* 需要注意的是，页面被卷去的头部，有兼容性问题，因此被卷去的头部通常有如下几种写法:
  1. 声明了DTD，使用document.documentElement.scrollTop
  2. 未声明DTD，使用document.body.scrollTop
  3. 新方法window. pageYoffset和window.pageXoffset，IE9开始支持

~~~JavaScript
function getScroll() {
    return {
      left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft||0,
      top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
    };
 } 
//使用的时候  getScroll().left
~~~



**三大系列总结**

1. offset系列经常用于**获得元素位置**offsetLeft offsetTop
2. client经常**用于获取元素大小**clientWidth clientHeight
3. scroll经常用于**获取滚动距离**scrollTop scrollLeft
4. 注意页面滚动的距离通过window.pageXoffset获得



**mouseenter和mouseover的区别**

* 当鼠标移动到元素上时就会触发mouseenter事件，类似mouseover，它们两者之间的差别是**mouseover鼠标经过自身盒子会触发，经过子盒子还会触发**。**mouseenter只会经过自身盒子触发**。之所以这样，就是因为**mouseenter不会冒泡**；跟mouseenter搭配，鼠标离开 mouseleave 同样不会冒泡



### 5.4 动画函数封装

**动画实现原理**

* **核心原理:通过定时器setlnterval()不断移动盒子位置**
* 实现步骤:
  1. 获得盒子当前位置
  2. 让盒子在当前位置加上1个移动距离
  3. 利用定时器不断重复这个操作
  4. 加一个结束定时器的条件
  5. 注意此元素需要添加定位，才能使用element.style.left

* 代码：

~~~html
	<div></div>//绝对定位
    <script>
        var div = document.querySelector('div');
        var timer = setInterval(function () {
            if (div.offsetLeft >= 400) {
                // 停止动画 本质是停止定时器
                clearInterval(timer);
            }
            div.style.left = div.offsetLeft + 1 + 'px';//改变 = 获取 + 1 + 'px'
        }, 30);
    </script>
~~~



**动画函数简单封装**

* 函数需要传递2个参数，动画对象和移动到的距离
* 代码：

~~~JavaScript
// 简单动画函数封装obj目标对象 target 目标位置
        function animate(obj, target) {
            var timer = setInterval(function () {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';

            }, 30);
        }
~~~



**动画函数给不同元素记录不同定时器**

* 如果多个元素都使用这个动画函数，每次都要var声明定时器。我们可以给不同的元素使用不同的定时器(自己专门用自己的定时器)
* 核心原理:利用JS是一门动态语言，可以很方便的给当前对象添加属性
* 代码：

~~~JavaScript
function animate(obj, target) {
            // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
            // 解决方案就是 让我们元素只有一个定时器执行
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                if (obj.offsetLeft >= target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + 1 + 'px';
            }, 30);
        }
~~~



**缓动效果原理**

* 缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来
* 思路:
  1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来
  2. **核心算法:(目标值-现在的位置)/ 10 作为每次移动的距离步长**
  3. 停止的条件是:让当前盒子位置等于目标位置就停止定时器
  4. 注意步长值需要取整

* 代码：

~~~JavaScript
function animate(obj, target) {
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                // 步长值写到定时器的里面
                var step = (target - obj.offsetLeft) / 10;
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                obj.style.left = obj.offsetLeft + step + 'px';
            }, 15);
        }
~~~



**动画函数多个目标值之间移动**

* 可以让动画函数从800移动到500
* 当我们点击按钮时候，判断步长是正值还是负值
  1. 如果是正值，则步长往大了取整
  2. 如果是负值，则步长向小了取整

* 代码：

~~~JavaScript
function animate(obj, target) {
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                // 步长值写到定时器的里面
                // 把我们步长值改为整数 不要出现小数的问题
                // var step = Math.ceil((target - obj.offsetLeft) / 10);
                var step = (target - obj.offsetLeft) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                obj.style.left = obj.offsetLeft + step + 'px';
            }, 15);
        }
~~~



**动画函数添加回调函数**

* 回调函数原理:函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数，这个过程就叫做回调
* 回调函数写的位置:定时器结束的位置

* 代码：

~~~JavaScript
function animate(obj, target, callback) {
            // console.log(callback);  callback = function() {}  调用的时候 callback()
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                // 步长值写到定时器的里面
                // 把我们步长值改为整数 不要出现小数的问题
                // var step = Math.ceil((target - obj.offsetLeft) / 10);
                var step = (target - obj.offsetLeft) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    if (callback) {
                        // 调用函数
                        callback();
                    }
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                obj.style.left = obj.offsetLeft + step + 'px';
            }, 15);
        } 
~~~



**动画函数封装到单独JS文件里面**

* 因为以后经常使用这个动画函数，可以单独封装到一个ls文件里面，使用的时候引用这个JS文件即可
  1. 单独新建一个JS文件
  2. HTML文件引入JS文件

* 代码：

~~~JavaScript
//animate.js
function animate(obj, target, callback) {
    // console.log(callback);  callback = function() {}  调用的时候 callback()

    // 先清除以前的定时器，只保留当前的一个定时器执行
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
        // 步长值写到定时器的里面
        // 把我们步长值改为整数 不要出现小数的问题
        // var step = Math.ceil((target - obj.offsetLeft) / 10);
        var step = (target - obj.offsetLeft) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            // 回调函数写到定时器结束里面
            // if (callback) {
            //     // 调用函数
            //     callback();
            // }
            callback && callback();
        }
        // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
        obj.style.left = obj.offsetLeft + step + 'px';
    }, 15);
}
~~~



### 5.5 常见网页特效案例

**轮播图**

* 轮播图也称为焦点图，是网页中比较常见的网页特效。
* 功能需求:
  1. 鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮
  2. 点击右侧按钮一次，图片往左播放一张，以此类推，左侧按钮同理
  3. 图片播放的同时，下面小圆圈模块跟随─起变化
  4. 点击小圆圈，可以播放相应图片
  5. 鼠标不经过轮播图，轮播图也会自动播放图片
  6. 鼠标经过，轮播图模块，自动播放停止



**节流阀**

* 防止轮播图按钮连续点击造成播放过快
* 节流阀目的:当上一个函数动画内容执行完毕，再去执行下一个函数动画，让事件无法连续触发
* 核心实现思路:利用回调函数，添加一个变量来控制，锁住函数和解锁函数(操作系统信号量PV操作)
  * 开始设置一个变量var flag = true;
  * lf(flag) {flag = false; do something}关闭水龙头
  * 利用回调函数动画执行完毕, flag = true打开水龙头

 

## 6、移动端网页特效

### 6.1 触屏事件

**触屏事件概述**

* 移动端浏览器兼容性较好，我们不需要考虑以前JS的兼容性问题，可以放心的使用原生S书写效果，但是移动端也有自己独特的地方。比如触屏事件 touch(也称触摸事件)，Android和IOS都有
* touch对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。触屏事件可响应用户手指(或触控笔)对屏幕或者触控板操作
* 常见的触屏事件如下：

| 触屏touch事件 |               说明                |
| :-----------: | :-------------------------------: |
|  touchstart   |  手指**触摸到**一个DOM元素时触发  |
|   touchmove   | 手指在一个DOM元素上**滑动时**触发 |
|   touchend    |  手指从一个DOM元素**移开时**触发  |

* 代码：

~~~html
	<div></div>
    <script>
        // 1. 获取元素
        // 2. 手指触摸DOM元素事件
        var div = document.querySelector('div');
        div.addEventListener('touchstart', function () {
            console.log('我摸了你');
        });
        // 3. 手指在DOM元素身上移动事件
        div.addEventListener('touchmove', function () {
            console.log('我继续摸');
        });
        // 4. 手指离开DOM元素事件
        div.addEventListener('touchend', function () {
            console.log('轻轻的我走了');
        });
    </script>
~~~



**触摸事件对象**

* TouchEvent是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少，等等
* touchstart、touchmove、touchend三个事件都会各自有事件对象

|    触摸列表    |                         说明                         |
| :------------: | :--------------------------------------------------: |
|    touches     |         正在**触摸屏幕的所有手指**的一个列表         |
| targetTouches  |      正在**触摸当前DOM元素上的手指**的一个列表       |
| changedTouches | 手指**状态发生了改变的列表**，从无到有，从有到无变化 |



**移动端拖动元素**

* touchstart、touchmove、touchend可以实现拖动元素；但是拖动元素需要当前手指的坐标值；我们可以使用targetTouches[0]里面的pageX和pageY
* 移动端拖动的原理:手指移动中，计算出手指移动的距离；然后用盒子原来的位置＋手指移动的距离
* 手指移动的距离:**手指滑动中的位置减去手指刚开始触摸的位置**
* 拖动元素三步曲:
  1. 触摸元素touchstart: 获取手指初始坐标，同时获得盒子原来的位置
  2. 移动手指touchmove: 计算手指的滑动距离，并且移动盒子
  3. 离开手指touchend:
* 注意:**手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动e.preventDefault();**

* 代码：

~~~html
	<div></div>
    <script>
        // （1） 触摸元素 touchstart：  获取手指初始坐标，同时获得盒子原来的位置
        // （2） 移动手指 touchmove：  计算手指的滑动距离，并且移动盒子
        // （3） 离开手指 touchend:
        var div = document.querySelector('div');
        var startX = 0; //获取手指初始坐标
        var startY = 0;
        var x = 0; //获得盒子原来的位置
        var y = 0;
        div.addEventListener('touchstart', function (e) {
            //  获取手指初始坐标
            startX = e.targetTouches[0].pageX;
            startY = e.targetTouches[0].pageY;
            x = this.offsetLeft;
            y = this.offsetTop;
        });

        div.addEventListener('touchmove', function (e) {
            //  计算手指的移动距离： 手指移动之后的坐标减去手指初始的坐标
            var moveX = e.targetTouches[0].pageX - startX;
            var moveY = e.targetTouches[0].pageY - startY;
            // 移动我们的盒子 盒子原来的位置 + 手指移动的距离
            this.style.left = x + moveX + 'px';
            this.style.top = y + moveY + 'px';
            e.preventDefault(); // 阻止屏幕滚动的默认行为
        });
    </script>
~~~



### 6.2 移动端常见特效

**classList属性**

* classList属性是HTML5新增的一个属性，返回元素的类名。但是ie10以上版本支持。该属性用于在元素中添加，移除及切换CSS类，对类选择器进行操作
* 添加类:element.classList.add (’类名’) ;
* 移除类:element.classList.remove (’类名’);
* 切换类:element.classList.toggle (’类名’)；
* 注意以上方法里面，所有类名都不带点



**click延时解决方案**

* 移动端click事件会有300ms的延时，原因是移动端屏幕双击会缩放(double tap to zoom)页面

* 解决方案:

1. 禁用缩放。浏览器禁用默认的双击缩放行为并且去掉300ms的点击延迟
   * 缺点：有的页面就是要使用双击缩放功能

~~~html
<meta name="viewport" content="user-scalable=no">
~~~
2.  利用touch事件自己封装这个事件解决300ms延迟
    * 缺点：只能给一个元素使用

* 原理就是:
  
     1. 当我们手指触摸屏幕，记录当前触摸时间
     2. 当我们手指离开屏幕，用离开的时间减去触摸的时间
     3. 如果时间小于150ms，并且没有滑动过屏幕，那么我们就定义为点击

* 代码：

~~~JavaScript
//封装tap，解决click 300ms 延时
function tap (obj, callback) {
        var isMove = false;
        var startTime = 0; // 记录触摸时候的时间变量
        obj.addEventListener('touchstart', function (e) {
            startTime = Date.now(); // 记录触摸时间
        });
        obj.addEventListener('touchmove', function (e) {
            isMove = true;  // 看看是否有滑动，有滑动算拖拽，不算点击
        });
        obj.addEventListener('touchend', function (e) {
            if (!isMove && (Date.now() - startTime) < 150) {  // 如果手指触摸和离开时间小于150ms 算点击
                callback && callback(); // 执行回调函数
            }
            isMove = false;  //  取反 重置
            startTime = 0;
        });
}
//调用  
tap(div, function(){   // 执行代码  });
~~~

3. 使用插件。fastclick插件解决300ms延迟
   * 推荐

* 代码：

~~~javascript
if ('addEventListener' in document) {
            document.addEventListener('DOMContentLoaded', function() {
                       FastClick.attach(document.body);
            }, false);
}
~~~



### 6.3 移动端常见开发插件

**插件的定义**

* JS插件是js文件，它遵循一定规范编写，方便程序展示效果，拥有特定功能且方便调用。如轮播图和瀑布流插件
* 特点:它一般是为了解决某个问题而专门存在，其功能单一，并且比较小



**插件的使用**

1. 确认插件实现的功能
2. 去官网查看使用说明
3. 下载插件
4. 打开demo实例文件，查看需要引入的相关文件，并且引入
5. 复制demo实例文件中的结构html，样式css以及js代码



**移动端常见插件**

* 解决延时：[ftlabs/fastclick: Polyfill to remove click delays on browsers with touch UIs (github.com)](https://github.com/ftlabs/fastclick)
* 轮播图：[Swiper中文网-轮播图幻灯片js插件,H5页面前端开发](https://www.swiper.com.cn/)
* [SuperSlide | TouchSlide 官方网站 大话主席 (superslide2.com)](http://www.superslide2.com/)
* [cubiq/iscroll: Smooth scrolling for the web (github.com)](https://github.com/cubiq/iscroll)



### 6.4 移动端常用开发框架

**框架概述**

* 框架，顾名思义就是一套架构，它会基于自身的特点向用户提供一套较为完整的解决方案。框架的控制权在框架本身，使用者要按照框架所规定的某种规范进行开发
* 插件一般是为了解决某个问题而专门存在，其功能单一，并且比较小
* **前端常用的框架有Bootstrap、Vue、Angular、React**等。既能开发PC端，也能开发移动端前端常用的移动端
* **插件有swiper、superslide、iscroll**等
* 框架:大而全，一整套解决方案
* 插件:小而专一，某个功能的解决方案



**Bootstrap**

* Bootstrap是一个简洁、直观、强悍的前端开发框架，它让web开发更迅速、简单。它能开发PC端，也能开发移动端
* Bootstrap JS插件使用步骤:
  1. 引入相关js文件
  2. 复制HTML结构
  3. 修改对应样式
  4. 修改相应JS参数



## 7、本地存储

### 7.1 本地存储 

1. 数据存储在用户浏览器中
2. 设置、读取方便、甚至页面刷新不丢失数据
3. 容量较大,sessionStorage约5M、localStorage约20M
4. 只能存储字符串，可以将对象JSON.stringify()编码后存储



### 7.2 window.sessionStorage

1. **生命周期为关闭浏览器窗口**
2. 在同一个窗口(页面)下数据可以共享
3. 以键值对的形式存储使用

* 存储数据：sessionStorage.setItem(key, value)
* 获取数据：sessionStorage.getItem(key)
* 删除数据：sessionStorage.removeItem(key)
* 删除所有数据：sessionStorage.clear()



### 7.3 window.localStorage

1. **声明周期永久生效，除非手动删除**否则关闭页面也会存在
2. 可以**多窗口(页面)共享**(同一浏览器可以共享)
3. 以键值对的形式存储使用

* 存储数据：localStorage.setItem(key, value)
* 获取数据：localStorage.getItem(key)
* 删除数据：localStorage.removeItem(key)
* 删除所有数据：localStorage.clear()
p (obj, callback) {
        var isMove = false;
        var startTime = 0; // 记录触摸时候的时间变量
        obj.addEventListener('touchstart', function (e) {
            startTime = Date.now(); // 记录触摸时间
        });
        obj.addEventListener('touchmove', function (e) {
            isMove = true;  // 看看是否有滑动，有滑动算拖拽，不算点击
        });
        obj.addEventListener('touchend', function (e) {
            if (!isMove && (Date.now() - startTime) < 150) {  // 如果手指触摸和离开时间小于150ms 算点击
                callback && callback(); // 执行回调函数
            }
            isMove = false;  //  取反 重置
            startTime = 0;
        });
}
//调用  
tap(div, function(){   // 执行代码  });
~~~

3. 使用插件。fastclick插件解决300ms延迟
   * 推荐

* 代码：

~~~javascript
if ('addEventListener' in document) {
            document.addEventListener('DOMContentLoaded', function() {
                       FastClick.attach(document.body);
            }, false);
}
~~~



### 6.3 移动端常见开发插件

**插件的定义**

* JS插件是js文件，它遵循一定规范编写，方便程序展示效果，拥有特定功能且方便调用。如轮播图和瀑布流插件
* 特点:它一般是为了解决某个问题而专门存在，其功能单一，并且比较小



**插件的使用**

1. 确认插件实现的功能
2. 去官网查看使用说明
3. 下载插件
4. 打开demo实例文件，查看需要引入的相关文件，并且引入
5. 复制demo实例文件中的结构html，样式css以及js代码



**移动端常见插件**

* 解决延时：[ftlabs/fastclick: Polyfill to remove click delays on browsers with touch UIs (github.com)](https://github.com/ftlabs/fastclick)
* 轮播图：[Swiper中文网-轮播图幻灯片js插件,H5页面前端开发](https://www.swiper.com.cn/)
* [SuperSlide | TouchSlide 官方网站 大话主席 (superslide2.com)](http://www.superslide2.com/)
* [cubiq/iscroll: Smooth scrolling for the web (github.com)](https://github.com/cubiq/iscroll)



### 6.4 移动端常用开发框架

**框架概述**

* 框架，顾名思义就是一套架构，它会基于自身的特点向用户提供一套较为完整的解决方案。框架的控制权在框架本身，使用者要按照框架所规定的某种规范进行开发
* 插件一般是为了解决某个问题而专门存在，其功能单一，并且比较小
* **前端常用的框架有Bootstrap、Vue、Angular、React**等。既能开发PC端，也能开发移动端前端常用的移动端
* **插件有swiper、superslide、iscroll**等
* 框架:大而全，一整套解决方案
* 插件:小而专一，某个功能的解决方案



**Bootstrap**

* Bootstrap是一个简洁、直观、强悍的前端开发框架，它让web开发更迅速、简单。它能开发PC端，也能开发移动端
* Bootstrap JS插件使用步骤:
  1. 引入相关js文件
  2. 复制HTML结构
  3. 修改对应样式
  4. 修改相应JS参数



## 7、本地存储

### 7.1 本地存储 

1. 数据存储在用户浏览器中
2. 设置、读取方便、甚至页面刷新不丢失数据
3. 容量较大,sessionStorage约5M、localStorage约20M
4. 只能存储字符串，可以将对象JSON.stringify()编码后存储



### 7.2 window.sessionStorage

1. **生命周期为关闭浏览器窗口**
2. 在同一个窗口(页面)下数据可以共享
3. 以键值对的形式存储使用

* 存储数据：sessionStorage.setItem(key, value)
* 获取数据：sessionStorage.getItem(key)
* 删除数据：sessionStorage.removeItem(key)
* 删除所有数据：sessionStorage.clear()



### 7.3 window.localStorage

1. **声明周期永久生效，除非手动删除**否则关闭页面也会存在
2. 可以**多窗口(页面)共享**(同一浏览器可以共享)
3. 以键值对的形式存储使用

* 存储数据：localStorage.setItem(key, value)
* 获取数据：localStorage.getItem(key)
* 删除数据：localStorage.removeItem(key)
* 删除所有数据：localStorage.clear()
