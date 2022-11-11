# CSS

## 1、基础认知

* **CSS：层叠样式表(Cascading style sheets)，给页面中的HTML标签设置样式**
* CSS写在style标签中，style标签一般写在head标签里面，title标签下面
* CSS引入方式：
  * **内嵌式:** CSS 写在style标签中
    提示: style标签虽然可以写在页面任意位置，但是通常约定写在head 标签中
  * **外联式:** CSS 写在一个单独的.css文件中
    提示:需要通过link标签在网页中引入
  * **行内式:** CSS 写在标签的style属性中
    提示:不推荐使用，之后会配合js使用



## 2、基础选择器

* 选择器的作用：选择页面中对应的标签，方便后续设置样式



### 2.1 标签选择器

* 结构：标签名 {css属性名：属性值；}
* 作用：通过标签名，找到页面中**所有**这类标签，设置样式

![在这里插入图片描述](https://img-blog.csdnimg.cn/d9aba768cc584975ad0bb453e95b740f.png)


* 注意点：
  * **标签选择器选择的是一类标签，而不是单独某一个**
  * **标签选择器无论嵌套关系有多深，都能找到对应的标签**



### 2.2 类选择器

* 结构：. 类名 {css属性名：属性值}
* 作用：通过类名，找到页面中**所有**带有这个类名的标签，设置样式

![在这里插入图片描述](https://img-blog.csdnimg.cn/e8cef28ec6854041922b53a9a5e2ff0a.png#pic_center)


* 注意点：
  * **所有标签上都有class属性，class属性的属性值称为类名**
  * **类名可以有数字、字母、下划线、中划线组成，但不能由数字或中划线开头**
  * **一个标签可以同时有多个类名，类名之间以空格隔开**
  * **类名可以重复，一个类选择器可以同时选中多个标签**



### 2.3 id选择器

* 结构：#id属性值 {css属性名：属性值；}
* 作用：通过id属性值，找到页面中带有这个id属性值的标签，设置样式

![在这里插入图片描述](https://img-blog.csdnimg.cn/3813b1d72ce14f2db9968ff8edf667f9.png#pic_center)


* 注意点：
  * **所有标签上都有id属性**
  * **id属性值类似于身份证号码，在一个页面中是唯一的，不可重复的！（强行使用会展示效果，但是不符合语法规范！！！）**
  * **一个标签上只能有一个id属性值**
  * **一个id选择器只能选中一个标签**

* 类与id的区别：

  * **class类名相当于姓名，可以重复，一个标签可以同时有多个class类名**
  * **id属性值相当于身份证号码，不可重复，一个标签只能有一个id属性值**


* 实际开发的情况
  * 类选择器用的最多
  * id一般配合js使用，除非特殊情况，否则不要使用id设置样式
  * 实际开发中会遇到冗余代码的抽取(可以将一些公共的代码抽取到一个公共的类中去)



### 2.4 通配符选择器

* 结构：* {css属性名：属性值；}
* 作用：找到页面中所有的标签，设置样式

![在这里插入图片描述](https://img-blog.csdnimg.cn/0bc0071180b74cf98b79e219ffee1d9c.png#pic_center)


* 注意点：
  * **开发中使用极少，只会在特殊情况下使用**
  * **用于去除标签默认的margin和padding**

![在这里插入图片描述](https://img-blog.csdnimg.cn/196bbfc5922648c0973eb8d40bdcc41e.png#pic_center)




## 3、字体和文本样式

### 3.1 字体样式

**字体大小**

* 属性名：font-size
* 取值：数字+px
* 代码：

~~~html
<style>
       p {
            font-size: 30px;
        }
</style>
~~~

* 注意点：
  * **谷歌浏览器默认文字大小是16px**
  * **单位需要设置，否则无效**



**字体粗细**

* 属性名：font-weight
* 取值：
  * 关键字：正常 - - normal，加粗 - - bold
  * 纯数字：100~900的整百数，正常 - - 400，加粗 - - 700
* 代码：

~~~html
	<style>	
	div {
            /* 加粗 */
            font-weight: 700;
        }

        h1 {
            /* 不加粗 */
            font-weight: 400;
        }
    </style>
~~~

* 注意点：
  * **不是所有的字体都提供了九种粗细，因此部分取值页面无变化**
  * **实际开发中正常、加粗两种取值使用最多**



**字体样式**

* 属性名：font-style
* 取值：正常(默认)：normal，倾斜：italic
* 代码：

~~~html
	<style>
        div {
            /* 倾斜 */
            font-style: italic;
        }

        em {
            /* 正常的, 不倾斜 */
            font-style: normal;
        }
    </style>
~~~



**常见字体系列**

* 无衬线字体(sans-serif)
1. 特点:文字笔画粗细均匀，并且首尾无装饰
2. 场景:**网页中大多采用无衬线字体**
3. 常见该系列字体:黑体、Arial



* 衬线字体( serif)
1. 特点:文字笔画粗细不均，并且首尾有笔锋装饰
2. 场景:报刊书籍中应用广泛
3. 常见该系列字体:宋体、Times New Roman



* 等宽字体(monospace)
1. 特点:每个字母或文字的宽度相等
2. 场景:一般用于程序代码编写，有利于代码的阅读和编写
3. 常见该系列字体:Consolas、fira code



**字体系列**

* 属性名: font-family
* 常见取值:具体字体1,具体字体2,具体字体3,具体字体4....字体系列
	* 具体字体:"Microsoft YaHei"、微软雅黑、黑体、宋体、楷体等.......
	* 字体系列: sans-serif、serif、monospace等......
* 渲染规则:
  1. **从左往右按照顺序查找，如果电脑中未安装该字体，则显示下一个字体**
  2. **如果都不支持，此时会根据操作系统，显示最后字体系列的默认字体**
* 代码：

~~~html
	<style>
        div {
            /* 如果用户电脑没有安装微软雅黑, 就按黑体显示文字 */
            /* 如果电脑没有安装黑体, 就按任意一种非衬线字体系列显示 */
            font-family: 微软雅黑, 黑体, sans-serif;
        }
    </style>
~~~

* 注意点:
  1. **如果字体名称中存在多个单词，推荐使用引号包裹**
  2. **最后一项字体系列不需要引号包裹**
  3. **网页开发时，尽量使用系统常见自带字体，保证不同用户浏览网页都可以正常浏览**



**字体属性连写**

* 属性名：font（复合属性）
* 取值：font：style weight size family;
* 省略要求：只能省略前两个，如果省略了相当于设置了默认值
* 代码：

~~~html
	<style>
        p {         
            /* font: italic 700 66px 宋体;*/
            font: 100px 微软雅黑;
        }
    </style>
~~~

* 注意点：**如果需要同时设置单独和连写形式，要么把单独的样式写在连写下面，要么把单独的样式写在连写里面**



### 3.2 文本样式

**文本缩进**

* 属性名：text-indent
* 取值：
  * 数字+px;
  * **数字+em；（1em = 当前标签的font-size的大小）**
* 代码：

~~~html
	<style>
        p {
            /* 默认字号: 16px ; 32 */

            /* em: 一个字的大小 */
            text-indent: 2em;
            font-size: 40px;
        }
    </style>
~~~



**文本水平对齐**

* 属性名：text-align
* 取值：

| 属性值 |   效果   |
| :----: | :------: |
|  left  |  左对齐  |
| center | 居中对齐 |
| right  |  右对齐  |

* 注意点：**如果需要让文本水平居中，text-aligh属性给文本所在标签（文本的父元素）设置**
* text-align：center能让哪些元素水平居中
  * 文本
  * span标签、a标签
  * input标签、img标签
* 代码：

~~~html
	<style>
        h1 {
            text-align: center;
        }

        body {
            text-align: right;
        }
    </style>
~~~



**文本修饰**

* 属性名：text-decoration
* 取值：

|    属性值    |        效果        |
| :----------: | :----------------: |
|  underline   |   下划线（常用）   |
| line-through |  删除线（不常用）  |
|   overline   | 上划线（几乎不用） |
|     none     |  无装饰线（常用）  |

* 代码：

~~~html
	<style>
        div {
            text-decoration: underline;
        }

        p {
            text-decoration: line-through;
        }

        h2 {
            text-decoration: overline;
        }

        a {
            text-decoration: none;
        }
    </style>
~~~

* **注意点:开发中使用text-decoration：none；清除a标签默认的下划线**



### 3.3 line-height行高

* 作用:控制一行的上下行间距
* 属性名:line-height
* 取值:数字+px；倍数（当前标签font-size的倍数)
* 应用:
  1. 让单行文本垂直居中可以设置line-height :文字父元素高度
  2. 网页精准布局时，会设置line-height ，可以取消上下间距
* 代码：

~~~html
	<style>
        p {
            /* line-height: 50px; */
            /* 自己字号的1.5倍 */
            /* line-height: 1.5; */

            /* 66px 宋体 倾斜 加粗 行高是2倍 */
            font: italic 700 66px/2 宋体;
        }
    </style>
~~~

~~~html
	<style>
        div {
            width: 552px;
            height: 400px;
            background-color: pink;
            /* background-color: green; */
            text-align: center;
            /* 文字是单行的 */
            /* 垂直居中技巧: 设置行高属性值 = 自身高度属性值 */
            line-height: 400px;
            font-size: 61px;
        }
    </style>
~~~

* 行高与font连写的注意点:
  * 如果同时设置了行高和font连写，注意覆盖问题
  * font : style weight size/line-height family ;

![在这里插入图片描述](https://img-blog.csdnimg.cn/b0dadabbd264475799cad6aff8c21595.png#pic_center)




## 4、扩展 -  颜色、居中

### 4.1 颜色常见取值

**关键词**

* 常见颜色取值：red：红色、green：绿色、pink：粉色...



**rgb表示法**

* 每项取值范围：0~255
* 常见颜色取值：rgb（255,0,0）：红色、rgb（0,255,0）：绿色、rgb（0,0,255）：黑色...



**rgba表示法**

* 比rgb表示法多一个a，a表示透明度
* a的取值范围：0~1；1-完全不透明，0-完全透明
* 省略写法：raga（0,0,0,0.5）可以省略写成rgba（0,0,0,.5）



**十六进制表达式**

* 取值范围：两个数字为一组，每个数字的取值范围：0~9，a,b,c,d,e,f
* 省略写法：
  * 三组中每个数字都相同，此时可以每组可以省略只写一个数字
  * 正确写法：#ffaabb改写成#fab
* 常见取值
  * #fff:白色
  * #000：黑色
* 注意点
  * 类似于：#ffaabc不能改写成#fabc
  * 实际开发中会直接使用测量工具直接得到颜色，不需要前端自己设置颜色



### 4.2 标签水平居中

* 通过设置margin: 0 auto;实现div、p、h水平居中
* 代码：

~~~html
	<style>
        div {
            width: 300px;
            height: 300px;
            background-color: pink;
            margin: 0 auto;
        }
    </style>
~~~

* 注意点：
  * 让div、p、 h (大盒子)水平居中，直接给当前元素本身设置即可
  * **margin: 0 auto一般针对于固定宽度的盒子，如果大盒子没有设置宽度，此时会默认占满父元素的宽度**



## 5、选择器进阶

### 5.1 复合选择器

**后代选择器:空格**

* 作用:根据HTML标签的嵌套关系，选择父元素后代中满足条件的元素
* 选择器语法:选择器1选择器2{ css }
* 代码：

~~~html
	<style>
        /* 找到div的儿子p设置文字颜色是红色 */
        /* 父选择器   后代选择器 {} */
        div p {
            color: red;
        }
    </style>
~~~

* 结果:
    * 在选择器1所找到标签的后代(儿子.孙子、重孙子...）中，找到满足选择器2的标签，设置样式
* 注意点:
    1. **后代包括:儿子、孙子、重孙子......**
    2. **后代选择器中，选择器与选择器之前通过空格隔开**



**子代选择器:>**

* 作用:根据HTML标签的嵌套关系，选择父元素子代中满足条件的元素
* 选择器语法:选择器1>选择器2{ css }
* 代码：

~~~html
	<style>
        /* 只想选中儿子a */
        /* div的儿子a文字颜色是红色 */
        div>a {
            color: red;
        }
    </style>
~~~

* 结果:
  * 在选择器1所找到标签的子代(儿子)中，找到满足选择器2的标签，设置样式
* 注意点:
  1. **子代只包括:儿子**
  2. **子代选择器中，选择器与选择器之前通过>隔开**



### 5.2 并集选择器

**并集选择器:，**

* 作用:同时选择多组标签，设置相同的样式
* 选择器语法:选择器1 ，选择器2{ css }
* 代码：

~~~html
	<style>
        /* p div span h1 文字颜色是红色 */
        /* 选择器1, 选择器2 {} */
        p, 
        div, 
        span, 
        h1 {
            color: red;
        }
    </style>
~~~

* 结果:找到选择器1和选择器2选中的标签，设置样式

* 注意点:

  1. **并集选择器中的每组选择器之间通过，分隔**

  2. **并集选择器中的每组选择器可以是基础选择器或者复合选择器**
  3. **并集选择器中的每组选择器通常一行写一个，提高代码的可读性**



### 5.3 交集选择器

**交集选择器:紧挨着**

* 作用:选中页面中同时满足多个选择器的标签
* 选择器语法:选择器1选择器2{ css }
* 代码：

~~~html
	<style>
        /*必须是p标签,而且添加了box类 */
        p.box {
            color: red;
        }
        /* .box是类选择器 */
    </style>
~~~

* 结果:**(既又原则)**找到页面中**既**能被选择器1选中，又能被选择器2选中的标签，设置样式
* 注意点:
  1. **交集选择器中的选择器之间是紧挨着的，没有东西分隔**
  2. **交集选择器中如果有标签选择器，标签选择器必须写在最前面**



### 5.4 hover伪类选择器

**hover伪类选择器**

* 作用:选中鼠标悬停在元素上的状态，设置样式
* 选择器语法:选择器:hover { css }
* 代码：

~~~html
	<style>
        /* 悬停的时候文字颜色是红色 */
        a:hover {
            color: red;
            background-color: green;
        }
    </style>
~~~

* 注意点:**伪类选择器选中的元素的某种状态**



### 5.5 Emmet语法

* 作用：通过简写语法，快速生成代码
* 语法：

|    记忆    |        示例         |                     效果                     |
| :--------: | :-----------------: | :------------------------------------------: |
|   标签名   |         div         |                < div>< /div>                 |
|  类选择器  |        .red         |          < div class="red">< /div>           |
|  id选择器  |        #one         |            < div id="one">< /div>            |
| 交集选择器 |      p.red#one      |       < p class="red" id ="one">< /p>        |
| 子代选择器 |        ui>li        |            < ul>< li>< /li>< /ul>            |
|  内部文本  | ul>li(li的文本内容) |      < ul>< li>li的文本内容< /li>< /ul>      |
|  创建多个  |       ul>li*3       | < ul>< li>< li>< li>< /li>< /li>< /li>< /ul> |



## 6、背景相关属性

### 6.1 背景颜色

* 属性名: background-color (bgc)
* 属性值:颜色取值:关键字、rgb表示法、rgba表示法、十六进制......
* 代码：

~~~html
	<style>
        div {
            width: 400px;
            height: 400px;
            /* background-color: pink; */
            /* background-color: #ccc; */
            /* 红绿蓝三原色, a是透明度0-1 */
            background-color: rgba(0, 0, 0, .5);
        }
    </style>
~~~

* 注意点:

  * **背景颜色默认值是透明: rgba(0,0,0,0). transparent**

  * 背景颜色不会影响盒子大小，并且还能看清盒子的大小和位置，一般在布局中会习惯先给盒子设置背景颜色



### 6.2 背景图片

* 属性名: background-image (bgi)
* 属性值: background-image: url('图片的路径');
* 代码：

~~~html
	<style>
        div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
        }
    </style>
~~~

* 注意点:

  * **背景图片中url中可以省略引号**
  * **背景图片默认是在水平和垂直方向平铺的**
  * **背景图片仅仅是指给盒子起到装饰效果，类似于背景颜色，是不能撑开盒子的**



**(拓展) img标签和背景图片的区别**

* 需求:需要在网页中展示—张图片的效果
* 方法一:直接写上img标签即可
  * img标签是一个标签，不设置宽高默认会以原尺寸显示
* 方法二:div标签＋背景图片
  * 需要设置div的宽高，因为背景图片只是装饰的CSS样式，不能撑开div标签



### 6.3 背景平铺

* 属性名：background-repeat(bgr)
* 属性值:

|   取值    |             效果             |
| :-------: | :--------------------------: |
|  repeat   | 水平和垂直方向都平铺（默认） |
| no-repeat |            不平铺            |
| repeat-x  |   沿着水平方向（x轴）平铺    |
| repeat-y  |   沿着垂直方向（y轴）平铺    |

* 代码：

~~~html
	<style>
        div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
            /* background-repeat: repeat; */
            /* 不平铺: 图片只显示一个 */
            /* background-repeat: no-repeat; */
            /* background-repeat: repeat-x; */
            /* background-repeat: repeat-y; */
        }
    </style>
~~~



### 6.4 背景位置

* 属性名：background-position（bgp）

* 属性值：background-position:水平方向位置 垂直方向位置；

![在这里插入图片描述](https://img-blog.csdnimg.cn/2e6d95d2037a40929ce32c521dba0d9d.png#pic_center)


* 代码：

~~~html
	<style>
        div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
            background-repeat: no-repeat;
            /* background-position: right 0; */
            /* background-position: center center; */
            /* background-position: 50px 100px; */
            background-position: -50px -100px;
            /* 正数: 向右向下移动; 负数:向左向上移动 */
            /* 注意: 背景色和背景图只显示在盒子里面 */
        }
    </style>
~~~

* 注意点：方位名词取值和坐标取值可以混使用，第一个取值表示水平，第二个取值表示垂直



### 6.5 背景相关属性连写

* 属性名: background (bg）
* 属性值:单个属性值的合写，取值之间以空格隔开
* 书写顺序:推荐: background: color image repeat position
* 代码：

~~~html
	<style>
        div {
            width: 400px;
            height: 400px;
            /* 不分先后顺序 背景色  背景图  背景图平铺  背景图位置 */
            /* background: pink url(./images/1.jpg) no-repeat center bottom; */
            /* 背景图位置如果是英文单词可以颠倒顺序 */
            background: pink url(./images/1.jpg) no-repeat bottom center ;
            /* 测试背景图位置如果是数值 不要颠倒顺序 */
            /* 水平50px, 垂直100px */
            /* background: pink url(./images/1.jpg) no-repeat 50px 100px; */
            background: pink url(./images/1.jpg) no-repeat 100px 50px;
        }
    </style>
~~~

* 省略问题:
    * 可以按照需求省略
    * 特殊情况:在pc端，如果盒子大小和背景图片大小一样，此时可以直接写background: url（)
* 注意点
    * 如果需要设置单独的样式和连写
    * ① 要么把单独的样式写在连写的**下面**
    * ② 要么把单独的样式写在连写的**里面**



## 7、元素显示模式

### 7.1 块级元素

* 显示特点:

	1. **独占一行（一行只能显示一个)**
	2. **宽度默认是父元素的宽度，高度默认由内容撑开**
	3. **可以设置宽高**
* 代表标签:div、p、 h系列、ul、 li、dl、dt、dd、form、header、nav、footer......
* 代码：

~~~html
	<style>
        /* 块: 独占一行; 宽度默认是父级100%; 添加宽度都生效 */
        div {
            width: 300px;
            height: 300px;
            background-color: pink;

            /* 行内块 */
            /* display: inline-block; */

            /* 行内 */
            /* display: inline; */
        }
    </style>
~~~



### 7.2 行内元素

* 显示特点:

	1. **一行可以显示多个**
	2. **宽度和高度默认由内容撑开**
	3. **不可以设置宽高**
* 代表标签: a、span、b、u、i、 s、strong、ins、em、del......
* 代码：

~~~html
	<style>
        /* 行内: 不换行; 设置宽高不生效; 尺寸和内容的大小相同 */
        span {
            width: 300px;
            height: 300px;
            background-color: pink;

            /* 行内块 */
            /* display: inline-block; */

            /* 块 */
            /* display: block; */
        }
    </style>
~~~



### 7.3 行内块元素

* 显示特点:

  1. **一行可以显示多个**

  2. **可以设置宽高**

* 代表标签:
     * input、textarea、button、select.....
     * 特殊情况: img标签有行内块元素特点，但是Chrome调试工具中显示结果是inline
     
* 代码：
  
     ~~~html
     <style>
             /* 行内块: 一行显示多个; 加宽高生效 */
             img {
                 width: 100px;
                 height: 100px;
             }
         </style>
     ~~~
     
     

### 7.4 元素显示模式转换

* 目的改变元素默认的显示特点，让元素符合布局要求
* 语法;

|         属性         |       效果       | 使用频率 |
| :------------------: | :--------------: | :------: |
|    display:block     |  转换成块级元素  |   较多   |
| display:inline-block | 转换成行内块元素 |   较多   |
|    display:inline    |  转换成行内元素  |   较少   |



**拓展：HTML嵌套规范注意点**

1. 块级元素一般作为大容器，可以嵌套:文本、块级元素、行内元素、行内块元素等等.......**但是:p标签中不要嵌套div、p、h等块级元素**

2. a标签内部可以嵌套任意元素，**但是:a标签不能嵌套a标签**



**扩展：居中方法总结：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/1f0058cef00649ed907bf327751f3bec.png#pic_center)




## 8、CSS特性

### 8.1 继承性

* 特性:子元素有默认继承父元素样式的特点（子承父业)
* 可以继承的常见属性**(文字控制属性都可以继承)**

1. color
2. font-style、font-weight、font-size、font-family
3. text-indent、text-align
4. line-height
5. ......

* 代码：

~~~html
	<style>
        /* 控制文字的属性都能继承; 不是控制文字的都不能继承 */
        div {
            color: red;
            font-size: 30px;
            height: 300px;
        }
    </style>
~~~

* 注意点:可以通过调试工具判断样式是否可以继承



**拓展：继承的应用**

* 好处:可以在—定程度上减少代码
* 常见应用场景:
1. **可以直接给ul设置list-style:none属性，从而去除列表默认的小圆点样式**
2. **直接给body标签设置统一的font-size，从而统一不同浏览器默认文字大小**



**拓展：继承失效的特殊情况**

* **如果元素有浏览器默认样式，此时继承性依然存在，但是优先显示浏览器的默认样式**
* a标签的color会继承失效
  * 其实color属性继承下来了，但是被浏览器默认设置的样式给覆盖掉了
*  h系列标签的font-size会继承失效
  * 其实font-size属性继承下来了，但是被浏览器默认设置的样式给覆盖掉了



### 8.2 层叠性

* 特性:
  1. 给同一个标签设置不同的样式→此时样式会层叠叠加→会共同作用在标签上
  2. 给同一个标签设置相同的样式→此时样式会层叠覆盖→最终写在最后的样式会生效
* 代码：

~~~html
	<style>
        div {
            color: red;
            color: green;
        }
		/*颜色显示为绿色*/
        .box {
            font-size: 30px;
        }
    </style>
~~~



* 注意点:当样式冲突时，只有当选择器优先级相同时，才能通过层叠性判断结果



### 8.3 优先级

**优先级介绍**

* 特性:不同选择器具有不同的优先级，优先级高的选择器样式会覆盖优先级低选择器样式
* 优先级公式:
  * **继承<通配符选择器<标签选择器<类选择器< id选择器<行内样式< !limportant**
* 代码：

~~~html
	<style>
        #box {
            color: orange;
        }

        .box {
            color: blue;
        }

        div {
            color: green !important;
        }

        body {
            color: red;
        }

        /* !important不要给继承的添加, 自己有样式无法继承父级样式 */
    </style>
~~~

* 注意点:
1. **!important写在属性值的后面，分号的前面!**
2. **!important不能提升继承的优先级，只要是继承优先级最低!**
3. **实际开发中不建议使用!important **



**权重叠加计算**

* 场景:如果是复合选择器，此时需要通过权重叠加计算方法，判断最终哪个选择器优先级最高会生效
* 权重叠加计算公式:(每—级之间不存在进位)

![在这里插入图片描述](https://img-blog.csdnimg.cn/77275cfe5a5541da863defe6b49b51a7.png#pic_center)


* 比较规则:
  1. 先比较第一级数字，如果比较出来了，之后的统统不看
  2. 如果第一级数字相同，此时再去比较第二级数字，如果比较出来了，之后的统统不看
  3. ...
  4. **如果最终所有数字都相同，表示优先级相同，则比较层叠性（谁写在下面，谁说了算!)**
     * 注意点: **!important如果不是继承，则权重最高，天下第一!**



**权重叠加计算**

* 权重计算题解题步骤:
  1. 先判断选择器是否能直接选中标签，如果不能直接选中→是继承，优先级最低→直接pass
  2. 通过权重计算公式，判断谁权重最高
* 注意点:实际开发中选择标签需要精准，尽量避免多个选择器同时选中一个标签的情况，不要自己难为自己



**查错流程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/032b652db9ef42bf91a72e213349baf4.png#pic_center)


## 9、盒子模型

### 9.1 盒子模型简介

* 盒子的概念
  1. 页面中的每一个标签，都可看做是一个“盒子”，通过盒子的视角更方便的进行布局
  2. 浏览器在渲染（显示)网页时，会将网页中的元素看做是一个个的矩形区域，我们也形象的称之为盒子
* 盒子模型
   * CSS中规定每个盒子分别由:内容区域(content)、内边距区域(padding)、边框区域(border)、外边距区域(margin)构成，这就是盒子模型
* 记忆:可以联想现实中的包装盒

![在这里插入图片描述](https://img-blog.csdnimg.cn/ccc4622f770a4074a0b848862091918d.png#pic_center)




### 9.2 内容区域的宽度和高度

* 作用:利用width 和height属性默认设置是盒子内容区域的大小
* 属性: width / height
* 代码：

~~~html
	<style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
~~~

* 常见取值:数字+px

![在这里插入图片描述](https://img-blog.csdnimg.cn/f7f2d5afd187472899a4c6fba15a0256.png#pic_center)




### 9.3 边距(border)

**边框--单个属性**

* 作用：给设置边框粗细、边框样式、边框颜色效果
* 单个属性：

|   作用   |    属性名    |              属性值               |
| :------: | :----------: | :-------------------------------: |
| 边框粗细 | border-width |              数字+px              |
| 边框样式 | border-style | 实线solid、虚线dashed、点线dotted |
| 边框颜色 | border-color |             颜色取值              |



**边框--连写形式**

* 属性名：border

* 属性值：单个取值的连写，取值之间以空格隔开。如border：10px solid red；

* 快捷键：bd+tab



**边框--单方向设置**

* 场景：只给盒子某个方向单独设置边框
* 属性名：bord - 方位名词
* 属性值：连写的取值
* 代码：

~~~html
	<style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            
            border-left: 5px dotted #000;
            border-right: 5px dotted #000;
            border-top: 1px solid red;
            border-bottom: 1px solid red;
        }
    </style>		
~~~



### 9.4 内边距(padding)

**内边距--取值**

* 作用：设置边框与内容区域之间的距离
* 属性名：padding
* 常见取值：

|  取值  |             示例              |              含义              |
| :----: | :---------------------------: | :----------------------------: |
| 一个值 |        padding：10px;         |          上下左右10px          |
| 两个值 |      padding：10px 20px;      |       上下10px，左右20px       |
| 三个值 |   padding：10px 20px 30px;    |    上10px，左右20px，下30px    |
| 四个值 | padding：10px 20px 30px 40px; | 上10px，右20px，下30px，左40px |



**内边距--单方向设置**

* 场景：只给盒子的某个方向单独设置内边距
* 属性名：padding - 方位名词
* 属性值：数字+px
* 代码：

~~~html
    <style>
        div {
            width: 300px;
            height: 300px;
            background-color: pink;

            padding-left: 10px;
            padding-bottom: 50px;
        }
    </style>
~~~



**盒子实际大小计算公式**

* 需求:盒子尺寸300*300，背景粉色，边框10px实线黑色，上下左右20px的内边距，如何完成?

* 注意点:①设置width和height是内容的宽高!②设置border会撑大盒子③设置padding会撑大盒子

* 盒子实际大小终极计算公式:
  * 盒子宽度=左边框＋左padding +内容宽度＋右padding +右边框
  * 盒子高度=上边框＋上padding +内容宽度＋ 下padding+下边框

* 代码：

~~~html
	<style>
        div {
            /* 撑大盒子的都有哪些? border + padding */
            /* width: 300px;
            height: 300px; */
            width: 240px;
            height: 240px;
            background-color: pink;
            border: 10px solid #000;
            padding: 20px;
        }
    </style>
~~~





**扩展：不会撑大盒子的特殊情况**（块级元素）

* 如果子盒子没有设置宽度，此时宽度默认是父盒子的宽
* 此时给子盒子设置左右的padding或者左右的border，此时不会撑大子盒子



**CSS3盒模型（自动内减)**

* 需求:盒子尺寸300*300，背景粉色，边框10px实线黑色，上下左右20px的内边距，如何完成?
* 给盒子设置border或padding时，盒子会被撑大，如果不想盒子被撑大?
* 解决方法①∶手动内减
  * 操作:自己计算多余大小，手动在内容中减去
  * 缺点:项目中计算量太大，很麻烦
* 解决方法②︰自动内减
  * 操作:**给盒子设置属性box-sizing : border-box;即可**
  * 优点:浏览器会自动计算多余大小，自动在内容中减去

*  代码：

~~~html
	<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px solid #000;
            padding: 20px;

            /* 內减模式 */
            /* 变成CSS3的盒子模型, 好处: 加了border和padding不需要手动减法 */
            box-sizing: border-box;
        }
    </style>
~~~



### 9.5 外边距(margin)

**外边距-取值**

* 作用：设置边框以外，盒子与盒子之间的距离

* 属性名：margin
* 常见取值：

|  取值  |             示例             |              含义              |
| :----: | :--------------------------: | :----------------------------: |
| 一个值 |        margin：10px;         |          上下左右10px          |
| 两个值 |      margin：10px 20px;      |       上下10px，左右20px       |
| 三个值 |   margin：10px 20px 30px;    |    上10px，左右20px，下30px    |
| 四个值 | margin：10px 20px 30px 40px; | 上10px，右20px，下30px，左40px |



**外边距--单方向设置**

* 场景：只给盒子的某个方向单独设置内边距
* 属性名：margin - 方位名词
* 属性值：数字+px

* 代码：

~~~html
	<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            margin: 50px;
            margin-left: 100px;
        }
    </style>
~~~



**清除默认内外边距**

* 场景:浏览器会默认给部分标签设置默认的margin和padding，但一般在项目开始前需要先清除这些标签默认的margin和padding，后续自己设置

* 解决方法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/e4162fa9be29440792022f3bab899c56.png)


![在这里插入图片描述](https://img-blog.csdnimg.cn/96e064b064f24845ba3c0036c2ec321f.png)


* 代码

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }
    </style>
~~~



**版型居中**

* 代码：

~~~html
	<style>
        div {
            width: 1000px;
            height: 300px;
            background-color: pink;
            margin: 0 auto;
        }
    </style>
~~~



**外边距正常情况**

* 场景:水平布局的盒子，左右的margin正常，互不影响
* 结果:最终两者距离为左右margin的和



**外边距折叠现象一①合并现象**

* 场景:垂直布局的块级元素，上下的margin会合并
* 结果:**最终两者距离为margin的最大值**
* 解决方法:**避免就好，只给其中一个盒子设置margin即可**
* 代码：

~~~html
	<style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        .one {
            /* margin-bottom: 50px; */
            margin-bottom: 60px;
        }

        .two {
            margin-top: 50px;
        }
    </style>
~~~



**外边距折叠现象一②塌陷现象**

* 场景:互相嵌套的块级元素，子元素的margin-top会作用在父元素上
* 结果:导致父元素—起往下移动
* 解决方法:
  1. **给父元素设置border-top 或者padding-top(分隔父子元素的margin-top)**
  2. **给父元素设置overflow: hidden**
  3. **转换成行内块元素**
  4. **设置浮动**

* 代码：

~~~html
	<style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
            /* padding-top: 50px; */
            /* 如果设计稿没有border, 不能使用这个解决办法 */
            /* border: 1px solid #000; */

            /* overflow: hidden; */
        }

        .son {
            width: 100px;
            height: 100px;
            background-color: skyblue;

            margin-top: 50px;

            display: inline-block;
        }
    </style>
~~~



**行内元素的margin和padding无效情况**

* 场景:给行内元素设置margin和padding时
* 结果:
  1. **水平方向的margin和padding布局中有效!**
  2. **垂直方向的margin和padding布局中无效!**

* 代码：

~~~html
	<style>
        span {
            /* margin: 100px; */
            /* padding: 100px; */
            line-height: 100px;
        }
    </style>
~~~



## 10、结构伪类选择器

* 作用与优势:
  1. 作用:根据元素在HTML中的结构关系查找元素
  2. 优势:减少对于HTML中类的依赖，有利于保持代码整洁
  3. 场景: 常用于查找某父级选择器中的子元素选择器

* 选择器：

|        选择器         |                   说明                   |
| :-------------------: | :--------------------------------------: |
|    E:first-child{}    |  匹配父元素中第一个子元素，并且是E元素   |
|    E:last-child{}     | 匹配父元素中最后一个子元素，并且是E元素  |
|   E:nth-child(n){}    |   匹配父元素中第n个子元素，并且是E元素   |
| E:nth-last-child(n){} | 匹配父元素中倒数第n个子元素，并且是E元素 |

* 代码：

~~~html
	<style>
        /* 选中第一个 */
        /* li:first-child {
            background-color: green;
        } */

        /* 最后一个 */
        /* li:last-child {
            background-color: green;
        } */

        /* 任意一个 */
        /* li:nth-child(5) {
            background-color: green;
        } */

        /* 倒数第xx个 */
        li:nth-last-child(1) {
            background-color: blue;
        }
    </style>
~~~

* n的注意点
  * n为：0、1 、2 、 3...
  * 通过n可以组成常见公式

|     功能      |      公式       |
| :-----------: | :-------------: |
|     偶数      |    2n、even     |
|     奇数      | 2n+1、2n-1、odd |
|   找到前5个   |      -n+5       |
| 找到第5个往后 |       n+5       |

* 代码：

~~~html
	<style>
        /* ** 偶数 */
        /* li:nth-child(2n) { */

            /* *** 奇数 */
        /* li:nth-child(2n+1) { */
            /* 找到前3个 */
        /* li:nth-child(-n+3) { */

            /* *** 4的倍数 */
        li:nth-child(4n) {
            background-color: green;
        }
    </style>
~~~



**扩展：nth-of-type结构伪类子元素**

* 选择器：

|       选择器        |                     说明                     |
| :-----------------: | :------------------------------------------: |
| E：nth-of-type(n){} | 只在父元素的同类型(E)子元素范围内，匹配第n个 |

* 区别
  * :nth-child →直接在所有孩子中数个数
  * :nth-of-type→先通过该类型找到符合的一堆子元素，然后在这一堆子元素中数个数

* 代码：

~~~html
	<style>
        /* 找到第一个li 里面的  第三个a  设置文字颜色是红色 */
        li:first-child a:nth-child(3) {
            color: red;
        }
    </style>
~~~



## 11、伪元素

* 伪元素:一般页面中的非主体内容可以使用伪元素
* 区别:
  1. 元素:HTML设置的标签
  2. 伪元素:CSS模拟出的标签效果
* 种类:
|伪元素|作用|
| :--: | :--: |
|::before |在父元素内容的最前添加一个伪元素|
|::after|在父元素内容的最后添加一个伪元素|
* 代码：

~~~html
	<style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
        }

        .father::before {
            /* 内容 */
            /* content属性必须添加, 否则伪元素不生效 */
            content: '老鼠';
            color: green;
            background-color: blue;
        }

        .father::after {
            content: '大米';
        }
    </style>
~~~

* 注意点:
  1. **必须设置content属性才能生效**
  2. **伪元素默认是行内元素**



## 12、标准流

* 标准流︰又称文档流，是浏览器在渲染显示网页内容时默认采用的一套排版规则，规定了应该以何种方式排
* 元素常见标准流排版规则:
  1．**块级元素:从上往下，垂直布局，独占一行**
  2．**行内元素或行内块元素:从左往右，水平布局，空间不够自动折行**



## 13、浮动

### 13.1 浮动的作用

* 早期的作用：图文环绕

![在这里插入图片描述](https://img-blog.csdnimg.cn/19936144c0c84c05beb4349b22e4c1c6.png#pic_center)


* 现在的作用：网页布局
  * 场景：让垂直布局的盒子变成水平布局，如：一个在左，一个在右

![在这里插入图片描述](https://img-blog.csdnimg.cn/e54e55bd2c854bf4bfdb0ea8144789b2.png#pic_center)




### 13.2 浮动的代码

* 属性名：float
* 属性值：

| 属性名 |  效果  |
| :----: | :----: |
|  left  | 左浮动 |
| right  | 右浮动 |

* 代码：

~~~html
	<style>
        div {
            width: 100px;
            height: 100px;
        }

        .one {
            background-color: pink;
            float: left;
        }

        .two {
            background-color: skyblue;
            /* flr */
            float: right;
            /* float: left; */
        }
    </style>
~~~



### 13.3 浮动的特点

* **浮动元素会脱离标准流(简称:脱标)，在标准流中不占位置**
  * 相当于从地面飘到了空中
* 浮动元素比标准流高半个级别，可以覆盖标准流中的元素
* 浮动找浮动，下一个浮动元素会在上一个浮动元素后面左右浮动
* 浮动元素有特殊的显示效果
    * 一行可以显示多个
    * **可以设置宽高**
* 注意点:
    * 浮动的元素不能通过text-align:center或者margin:0 auto



### 13.4 清除浮动

* 含义:清除浮动带来的影响
  * 影响∶如果子元素浮动了，此时子元素不能撑开标准流的块级父元素

* 原因:
  * 子元素浮动后脱标→不占位置

* 目的:
  * 需要父元素有高度，从而不影响其他网页元素的布局



**清除浮动的方法一- -直接设置父元素高度**

* 特点:
  * 优点:简单粗暴，方便
  * 缺点:有些布局中不能固定父元素高度。



**清除浮动的方法二- -额外标签法**

* 操作:

  1. 在父元素内容的最后添加一个块级元素

  2. 给添加的块级元素设置clear:both特点:
* 代码：

~~~html
	<style>
	.clearfix {
            /* 清除左右两侧浮动的影响 */
            clear: both;
        }
    </style>
~~~

* 缺点: 会在页面中添加额外的标签，会让页面的HTML结构变得复杂



**清除浮动的方法三- -单伪元素清除法**

* 操作：用伪元素替代了额外标签

  1. 基本写法

![在这里插入图片描述](https://img-blog.csdnimg.cn/0315cbbc76a04be999e3f6573c3d7e85.png#pic_center)


  2. 补充写法

![在这里插入图片描述](https://img-blog.csdnimg.cn/de3c616f364d4b69870a48001f1e4935.png#pic_center)


* 特点：项目中使用，直接给标签加类即可清除



**清除浮动的方法四- -双伪元素清除法**

* 操作：

![在这里插入图片描述](https://img-blog.csdnimg.cn/9ba9cd04e2a24f13ab23ff1dfd673f50.png#pic_center)


* 特点：在项目中使用，直接给标签加类即可清除浮动



**清除浮动的方法五- -给父元素设置overflow:hidden**

* 操作：直接给父元素设置overflow:hidden
* 代码：

~~~html
	<style>
        .top {
            margin: 0 auto;
            width: 1000px;
            height: 600px;
            background-color: pink;

            overflow: hidden;
        }
	</style>
~~~

* 特点：方便



**扩展：BFC的介绍**

* 块格式化上下文(Block Formatting Context) : BFC
  * 是Web页面的可视CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

* 创建BFC方法:
  1. html标签是BFC盒子
  2. 浮动元素是BFC盒子
  3. 行内块元素是BFC盒子
  4. overflow属性取值不为visible。如: auto、hidden...
  5. ……
* BFC盒子常见特点:
	1. **BFC盒子会默认包裹住内部子元素（标准流、浮动)→应用:清除浮动**
	2. **BFC盒子本身与子元素之间不存在margin的塌陷现象→应用:解决margin的塌陷**
	3. ...



## 14、定位

### 14.1 定位概述

* 定位：
  * 可以让元素自由的摆放在网页的任意位置
  * 一般用于盒子之间的层叠情况

* 场景：
  * 定位之后的元素层级最高，可以层叠在其他盒子上面
  * 可以让盒子始终固定在屏幕中的某个位置

* 定位的使用步骤：

1. 设置定位方式：

     * 属性名：position；
     * 常见属性值：

| 定位方式 |  属性值  |
| :------: | :------: |
| 静态定位 |  static  |
| 相对定位 | relative |
| 绝对定位 | absolute |
| 固定定位 |  fixed   |

2. 设置偏移量
	*   偏移值设置分为两个方向，水平和垂直方向各选一个使用即可
	*   选取的原则一般是就近原则（离哪边近用哪个)

| 方向 | 属性名 | 属性值  |      含义      |
| :--: | :----: | :-----: | :------------: |
| 水平 |  left  | 数字+px | 距离左边的距离 |
| 水平 | right  | 数字+px | 距离右边的距离 |
| 垂直 |  top   | 数字+px | 距离上边的距离 |
| 垂直 | bottom | 数字+px | 距离下边的距离 |



### 14.2 静态定位

* 介绍:静态定位是默认值,就是之前认识的标准流。
* 代码:

~~~html
	<style>
        /* css书写: 1. 定位 / 浮动 / display ; 2. 盒子模型; 3. 文字属性 */
        .box {
            /* 静态定位, 默认值, 标准流 */
            position: static;
        }
    </style>
~~~

* 注意点:
  1. 静态定位就是之前标准流,不能通过方位属性进行移动
  2. 之后说的定位不包括静态定位，一般特指后几种:相对、绝对、固定



### 14.3 相对定位

* 介绍:自恋型定位，相对于自己之前的位置进行移动
* 代码:

~~~html
	<style>
        /* 如果left和right都有, 以left为准; top和bottom都有以top 为准 */
        .box {
            position: relative;
            right: 200px;
            bottom: 400px;
            left: 100px;
            top: 200px;
        }
    </style>
~~~

* 特点:
  1. 需要配合方位属性实现移动
  2. 相对于自己原来位置进行移动
  3. 在页面中占位置→没有脱标
* 应用场景:
  1. 配合绝对定位组CP(子绝父相)
  2. 用于小范围的移动



### 14.4 绝对定位

* 介绍:拼爹型定位，相对于非静态定位的父元素进行定位移动
* 代码:

~~~html
	<style>
        .box {

            position: absolute;
            /* left: 50px; */
            left: 0;
            top: 0;  
        }
    </style>
~~~

* 特点:
  1. 需要配合方位属性实现移动
  2. 默认相对于浏览器可视区域进行移动
  3. 在页面中不占位置→已经脱标
* 应用场景:配合绝对定位组CP(子绝父相)
* 绝对定位偏移参照物
  * **祖先元素中没有定位，默认相当于浏览器进行移动**
  * **祖先元素中有定位，相对于最近的有定位的祖先元素进行移动**



### 14.5 子绝父相

* 场景:让子元素相对于父元素进行自由移动
* 特殊场景：使用子绝父相的时候，发现父元素已经有相对定位了，此时直接子绝即可，因为父元素已经有定位满足需求，如果盲目修改父元素定位方式，可能会影响之前写好的布局
* 代码：

~~~html
	<style>
        .father {
            position: relative;
        }
        .son {
            position: absolute;
            /* left: 20px;
            top: 30px; */
            right: 20px;
            bottom: 50px;
        }
    </style>
~~~

* 含义:
  * 子元素:绝对定位
  * 父元素:相对定位
  * 子绝父相好处:
    * 父元素是相对定位，则对网页布局影响最小



### 14.6 固定定位

* 介绍:死心眼型定位，相对于浏览器进行定位移动
* 代码: 

~~~html
	<style>
        .box {
            position: fixed;
            left: 0;
            top: 0;
        }
    </style>
~~~

* 特点:

  1. 需要配合方位属性实现移动

  2. **相对于浏览器可视区域进行移动**

  3. 在页面中不占位置→已经脱标

应用场景:让盒子固定在屏幕中的某个位置



### 14.7 元素的层级关系

* 不同布局方式元素的层级关系:**标准流<浮动<定位**

* 不同定位之间的层级关系:
  * 相对、绝对、固定默认层级相同
  * 此时HTML中写在下面的元素层级更高，会覆盖上面的元素

* 场景:改变定位元素的层级
* 属性名:z-index
* 属性值:数字
  * 数字越大，层级越高

* 代码：

~~~html
	<style>
        div {
            width: 200px;
            height: 200px;
        }

        .one {
            position: absolute;
            left: 20px;
            top: 50px;
            
            z-index: 1;

            background-color: pink;
        }

        .two {
            position: absolute;
            left: 50px;
            top: 100px;
            
            background-color: skyblue;
        }

        /* 
            默认情况下, 定位的盒子  后来者居上 ,
            z-index:整数; 取值越大, 显示顺序越靠上, z-index的默认值是0
            注意: z-index必须配合定位才生效
        */
    </style>
~~~



## 15、装饰

### 15.1 垂直对齐方式

* 基线：浏览器文字类型元素排版中存在用于对齐的基线(baseline)

![在这里插入图片描述](https://img-blog.csdnimg.cn/0ce3120d64eb46daa0e60555bc2e3128.png)




**垂直对齐方式**

* 属性名：vertical-align
* 属性值：

|  属性值  |      效果      |
| :------: | :------------: |
| baseline | 默认，基线对齐 |
|   top    |    顶部对齐    |
|  middle  |    中部对齐    |
|  bottom  |    底部对齐    |



**项目中垂直居中可以解决的问题**

1. 文本框和表单按钮无法对齐问题
* 代码：

~~~html
	<style>
    /* 浏览器遇到行内和行内块标签当做文字处理, 默认文字是按基线对象 */
    input {
      height: 50px;
      box-sizing: border-box;

      vertical-align: middle;
    }

  </style>
~~~

2. input和img无法对齐问题
* 代码：

~~~html
	<style>
   img {
     vertical-align: middle;
   }
  </style>
~~~


3. div中的文本框，文本框无法贴顶问题
* 代码：

~~~html
	<style>
    .father {
      width: 400px;
      height: 400px;
      background-color: pink;
    }

    input {
      /* vertical-align: middle; */
      vertical-align: top;
    }

  </style>
~~~


4. div不设高度由img标签撑开，此时img标签下面会存在额外间隙问题
* 代码：

~~~html
	<style>
    .father {
      width: 400px;
      background-color: pink;
    }

    img {
      /* 浏览器把行内和行内块标签当做文字处理,默认基线对齐 */
      /* vertical-align: middle; */
      display: block;
    }

  </style>
~~~

5. 使用line-heigh解决img标签垂直居中问题
* 代码：

~~~html
	<style>
    .father {
      width: 600px;
      height: 600px;
      background-color: pink;
      line-height: 600px;
      text-align: center;
    }

    img {
      vertical-align: middle;
    }
  </style>
~~~

* 注意点:
  * 学习浮动之后，不推荐使用行内块元素让div一行中显示，因为可能会出现垂直对齐问题
  * 推荐优先使用浮动完成效果



### 15.2 光标类型

* 场景：设置鼠标光标在元素上时显示的样式
* 属性名：cursor
* 常见属性值：

| 属性值  |             效果             |
| :-----: | :--------------------------: |
| default |      默认值、通常是箭头      |
| pointer |  小手效果，提示用户可以点击  |
|  text   | 工子型，提示用户可以选择文字 |
|  move   |  十字光标，提示用户可以移动  |

* 代码：

~~~html
	<style>
        div {
            /* 手型 */
            /* cursor: pointer; */

            /* 工字型, 表示可以复制 */
            /* cursor: text; */

            /* 十字型, 表示可以移动 */
            cursor: move;
        }
    </style>
~~~



### 15.3 边框圆角

* 场景:让盒子四个角变得圆润，增加页面细节，提升用户体验

* 属性名: border-radius

* 常见取值:数字+px、百分比

* 原理:

![在这里插入图片描述](https://img-blog.csdnimg.cn/e99cff145ffa4fb2a3e326318ac221bc.png#pic_center)


* 赋值规则:从左上角开始赋值，然后顺时针赋值，没有赋值的看对角!

* 代码：

~~~html
	<style>
        .box {
            margin: 50px auto;
            width: 200px;
            height: 200px;
            background-color: pink;

            /* 一个值: 表示4个角是相同的 */
            border-radius: 10px;

            /* 4值: 左上  右上   右下   左下 -- 从左上顺时针转一圈 */
            /* border-radius: 10px 20px 40px 80px; */

            /* border-radius: 10px 40px 80px; */

            /* border-radius: 10px 80px; */
        }
    </style>
~~~



**边框圆角的常见应用**

* 画一个正圆:

  1. 盒子必须是正方形

  2. 设置边框圆角为盒子宽高的一半→border-radius:50%

* 胶囊按钮:

  1. 盒子要求是长方形
  2. 设置→border-radius:盒子高度的一半

* 代码：

~~~html
	<style>
        /* 第一个盒子样式 */
        .one {
            width: 200px;
            height: 200px;
            background-color: pink;

            /* border-radius: 100px; */
            /* 50% : 取盒子尺寸的一半 */
            border-radius: 50%;
        }

        /* 第二个盒子样式 */
        /* 胶囊状: 长方形, border-radius取值是高度的一半 */
        .two {
            width: 400px;
            height: 200px;
            background-color: skyblue;

            border-radius: 100px;
        }
    </style>
~~~



### 15.4 overflow溢出部分显示效果

* 溢出部分:指的是盒子内容部分所超出盒子范围的区域
* 场景:控制内容溢出部分的显示效果，如:显示、隐藏、滚动条......
* 属性名: overflow
* 常见属性值:

| 属性值  |                效果                |
| :-----: | :--------------------------------: |
| visible |        默认值，溢出部分可见        |
| hidden  |            溢出部分隐藏            |
| scroll  |     无论是否溢出，都显示滚动条     |
|  auto   | 根据是否溢出，自动显示或隐藏滚动条 |

* 代码：

~~~html
	<style>
        .box {
            width: 300px;
            height: 300px;
            background-color: pink;

            /* 溢出隐藏 */
            overflow: hidden;

            /* 滚动: 无论内容是否超出都显示滚动条的位置 */
            /* overflow: scroll; */

            /* auto: 根据内容是否超出, 判断是否显示滚动条 */
            /* overflow: auto; */
        }
    </style>
~~~



### 15.5 元素本身隐藏

* 场景:让某元素本身在屏幕中不可见。如:鼠标:hover之后元素隐藏
* 常见属性:

1.  visibility: hidden

2. display: none

* 区别:

1. visibility: hidden隐藏元素本身，并且在网页中占位置
2. display: none隐藏元素本身，并且在网页中不占位置
* 注意点:
  * 开发中经常会通过display属性完成元素的显示隐藏切换
  *  display: none;(隐藏)、display: block;(显示)



**扩展：元素整体透明度**

* 场景:让某元素整体（包括内容)一起变透明
* 属性名: opacity
* 属性值:0~1之间的数字
  * 1:表示完全不透明
  * 0:表示完全透明
*  注意点:
  * opacity会让元素整体透明，包括里面的内容，如:文字、子元素等...



**扩展：边框合并**

* 场景:让相邻表格边框进行合并，得到细线边框效果
* 代码: border-collapse: collapse



**扩展：用CSS画三角形技巧**

* 实现原理：利用盒子边框完成
* 实现步骤：
  1. 设置一个盒子
  2. 设置四周不同的颜色
  3. 将盒子宽高设置为0，仅保留边框
  4. 得到四个三角形，选择其中一个后，其他三角形（边框）设置颜色为透明

![在这里插入图片描述](https://img-blog.csdnimg.cn/930bf9a8d4654dc8befae4c40cee7a1b.png#pic_center)


* 代码：

~~~html
	<style>
        div {
            /* width: 100px;
            height: 100px; */
            width: 0;
            height: 0;
            /* background-color: pink; */
            /* transparent: 透明 */
            border-top: 10px solid transparent;
            border-right: 10px solid transparent;
            border-bottom: 10px solid transparent;
            border-left: 10px solid orange;
        }
    </style>
~~~

* 通过调整不同边框的宽度，可以调整三角形的形态



## 16、选择器扩展

### 1、链接伪类选择器

* 场景：常用于选中超链接的不同状态
* 选择器语法：

|  选择器语法   |            功能             |
| :-----------: | :-------------------------: |
|   a:link{ }   | 选中a链接**未访问过**的状态 |
| a:visited { } | 选中a链接**访问之后**的状态 |
|  a:hover{ }   |   选中**鼠标悬停**的状态    |
|  a:active{ }  |   选中**鼠标按下**的状态    |

* 注意点：同时实现四种伪类状态，需要按照LVHA的顺序书写



### 2、焦点伪类选择器

* 场景：用于选中元素获取焦点时状态，常用于表单控件
* 选择器语法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/16f70b5d36fb4505b5e5f4a61c04794b.png#pic_center)


* 效果：表单控件获取焦点时默认会显示外部轮廓线



### 3、属性选择器

* 场景：
* 选择器语法：

|     选择器      |                   功能                   |
| :-------------: | :--------------------------------------: |
|     E[attr]     |         选择具有attr属性的E元素          |
| E[attr = "val"] | 选择具有attr属性并且属性值等于val的E元素 |

* 代码：

~~~html
	<style>
        /* text:背景色是粉色; password背景色是skyblue */
        input[type='text']  {
            background-color: pink;
        }

        input[type="password"] {
            background-color: skyblue;
        }
    </style>
~~~



## 17、CSS样式补充

### 17.1 精灵图

* 场景:项目中将多张小图片，合并成一张大图片，这张大图片称之为精灵图
* 优点:减少服务器发送次数，减轻服务器的压力，提高页面加载速度
* 例如:需要在网页中展示8张小图片
  * 8张小图片分别发送→发送8次
  * 合成一张精灵图发送→发送1次

* 步骤：
1. 创建一个盒子
2. 量取小图片大小，将小图片的宽高设置给盒子
3. 将精灵图设置为盒子的背景图片
4. 通过量小图片左上角坐标，分别取负值设置给盒子的background-position: x y

* 代码

~~~html
	<style>
        span {
            display: inline-block;
            width: 18px;
            height: 24px;
            background-color: pink;
            background-image: url(./images/taobao.png);
            /* 背景图位置属性: 改变背景图的位置 */
            /* 水平方向位置  垂直方向的位置 */
            /* 想要向左侧移动图片, 位置取负数;  */
            background-position: -3px 0;
        }
    </style>
~~~



### 17.2 背景图片大小

* 作用:设置背景图片的大小

* 语法: background-size: 宽度 高度 
* 取值:

|  取值   |                           场景                           |
| :-----: | :------------------------------------------------------: |
| 数字+px |                      简单方便，常用                      |
| 百分比  |              相当于当前盒子自身的宽高百分比              |
| contain |    包含，将背景图片等比例缩放，直到不会超出盒子的最大    |
|  cover  | 覆盖，将背景图片等比例缩放，直到刚好填满整个盒子没有空白 |



**扩展：background连写**

* 完整连写：

~~~html
background: color image repeat position/size
~~~

* 注意点：background-size和background连写同时设置时，需要注意覆盖问题

* 解决：
  1. 要么单独的样式写连写的下面
  2. 要么单独的样式写在连写的里面



### 17.3 文字阴影

* 作用:给文字添加阴影效果，吸引用户注意
* 属性名: text-shadow
* 取值:

|   参数   |                            |
| :------: | :------------------------: |
| h-shadow | 必须，水平偏移量，允许负值 |
| v-shadow | 必须，垂直偏移量，允许负值 |
|   blur   |        可选，模糊度        |
|  color   |       可选，阴影颜色       |

* 扩展：阴影可以叠加设置，每组阴影取值之间以逗号隔开



### 17.4 盒子阴影

* 作用:给盒子添加阴影效果，吸引用户注意，体现页面的制作细节
* 属性名:box-shadow
* 取值:

|   参数   |                            |
| :------: | :------------------------: |
| h-shadow | 必须，水平偏移量，允许负值 |
| v-shadow | 必须，垂直偏移量，允许负值 |
|   blur   |        可选，模糊度        |
|  spread  |       可选，阴影扩大       |
|  color   |       可选，阴影颜色       |
|  inset   |  可选，将阴影改为内部阴影  |

* 代码：

~~~html
	<style>
        .box {
            width: 200px;
            height: 200px;
            background-color: pink;

            box-shadow: 5px 10px 20px 10px green inset;

            /* 注意: 外阴影, 不能添加outset, 添加了会导致属性报错 */
            /* box-shadow: 5px 10px 20px 10px green outset; */
        }
    </style>
~~~



### 17.5 过渡

* 作用:让元素的样式慢慢的变化，常配合hover使用，增强网页交互体验
* 属性名: transition
* 常见取值:

|    参数    |                             取值                             |
| :--------: | :----------------------------------------------------------: |
| 过渡的属性 | all：所有能过渡的属性都过渡;具体属性名width：只有width有过渡 |
| 过渡的时长 |                          数字+s(秒)                          |

* 代码：

~~~html
	<style>
        /* 过渡配合hover使用, 谁变化谁加过渡属性 */
        .box {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* 宽度200, 悬停的时候宽度600, 花费1秒钟 */
            /* transition: width 1s, background-color 2s; */

            /* 如果变化的属性多, 直接写all,表示所有 */
            transition: all 1s;
        }

        .box:hover {
            width: 600px;
            background-color: red;
        }
    </style>
~~~

* 注意点:
1. 过渡需要∶默认状态和hover状态样式不同，才能有过渡效果
  
2. transition属性给需要过渡的元素本身加
  
3. transition属性设置在不同状态中，效果不同的
  
   * 给默认状态设置，鼠标移入移出都有过渡效果
   
   * 给hover状态设置，鼠标移入有过渡效果，移出没有过渡效果



## 18、项目扩展

### 18.1 网页和网站

* 网页:相当于是每页纸
* 网站:相当于一本书籍
  * 用户翻阅的时候，看的是每页纸上的内容
  * 由多页纸整合在一起，就是完整的一本书籍了

* 在互联网中，网站类似于是一本书，网页就是这本书的每一页
  * 比如:淘宝、京东、等就是一个网站，类似于是一本书
  * 这些网站中的每一个网页，如:主页、登录页面、商品页面就是每一个单独的页面，类似于每一页纸
  * 多个同主题网页整合在一起，就称之为网站。

* 网页:**网站中的每一“页”。**例如:淘宝的主页、淘宝的登录页、淘宝的商品页等。
* 网站:**提供特定服务的一组网页集合。**例如:百度、淘宝、京东等;



### 18.2 骨架结构标签

**DOCTYPE文档说明**

* <！DOCTYPE html>文档类型声明，告诉浏览器该网页的HTML版本
* 注意点:**DOCTYPE需要写在页面的第一行，不属于HTML标签**



**网页语言**

* < html lang="en">标识网页使用的语言
* 作用:搜索引擎归类＋浏览器翻译
* 常见语言:**zh-CN简体中文/en英文**



**字符编码**

* < meta charset="UTF-8">标识网页使用的字符编码
* 作用:保存和打开的字符编码需要统一设置，否则可能会出现乱码
* 常见字符编码︰
  1. UTF-8:万国码，国际化的字符编码，收录了全球语言的文字
  2. GB2312: 6000+汉字
  3. GBK: 20000+汉字
* 注意点:**开发中统一使用UTF-8字符编码即可**



* 代码：

~~~html
<!DOCTYPE html>
<!-- 中文网站 -->
<html lang="zh-CN">
<head>
    <!--charset="UTF-8" 规定网页的字符编码  -->
    <meta charset="UTF-8">

    <!-- ie(兼容性差) / edge -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <!-- 宽度 = 设备宽度 : 移动端网页的时候要用 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
~~~





### 18.3 SEO三大标签

* SEO ( Search Engine Optimization):搜索引擎优化
* 作用:让网站在搜索引擎上的排名靠前
* 提升SEO的常见方法:
  1. 竞价排名
  2. 将网页制作成html后缀
  3. 标签语义化(在合适的地方使用合适的标签)
  4. ...

* SEO三大标签
  1. title:网页标题标签
  2. description:网页描述标签
  3. keywords:网页关键词标签

* 代码：

~~~html
<head>
    <!-- meta:desc -->
    <meta name="description" content="京东JD.COM-专业的综合网上购物商城，为您提供正品低价的购物选择、优质便捷的服务体验。商品来自全球数十万品牌商家，囊括家电、手机、电脑、服装、居家、母婴、美妆、个护、食品、生鲜等丰富品类，满足各种购物需求。">
    <!-- meta:kw -->
    <meta name="keywords" content="网上购物,网上商城,家电,手机,电脑,服装,居家,母婴,美妆,个护,食品,生鲜,京东">
    <title>京东(JD.COM)-正品低价、品质保障、配送及时、轻松购物</title>
</head>
~~~



### 18.4 ico图标的设置

* 场景:显示在标签页标题左侧的小图标，习惯使用.ico格式的图标
* 代码:

~~~html
<head>
    <link rel="shortcut icon" href="ico图标路径" type="image/x-icon">
</head>
~~~



### 18. 版心

* 场景:把页面的主体内容约束在网页中间
* 作用:让不同大小的屏幕都能看到页面的主体内容
* 代码:

~~~html
<style>
    .container {
        width:1240px;
        margin:0 auto;
    }
</style>
~~~

* 注意点:版心类名常用:container、wrapper、w等



**扩展：CSS书写顺序**

* 不同的CSS书写顺序会影响浏览器的渲染性能，推荐前端工程师使用专业的书写顺序习惯

| 顺序 |     类别      |                         属性                          |
| :--: | :-----------: | :---------------------------------------------------: |
|  1   |   布局属性    | display、position、float、clear、visibility、overflow |
|  2   | 盒子模型+背景 |  width、height、margin、padding、border、background   |
|  3   | 文本内容属性  | color、font、text-decoration、text-align、line-height |
|  4   |   点缀属性    |    cursor、border-radius、text-shadow、box-shadow     |

* 注意点：开发中推荐多用类＋后代，但不是层级越多越好，一个选择器中的类选择器的个数推荐不要超过3个



### 18.5 文件和目录

* 新建项目文件夹demo-pc-client，在VScode中打开
  * 在实际开发中，项目文件夹不建议使用中文
  * 所有项目相关文件都保存在demo-pc-client目录中
  
* 复制favicon.ico到demo-pc-client目录
  
    * 一般习惯将ico图标放在项目根目录
    
* 复制images和uploads目录到demo-pc-client目录中
  
    * images :存放网站固定使用的图片素材，如: logo、样式修饰图片...等. 
    * uploads:存放网站非固定使用的图片素材，如:商品图片、宣传图片...等
    
* 新建index.html在根目录

* 新建css文件夹保存网站的样式，并新建以下CSS文件: 

    * base.css:基础公共样式

    * common.css:该网站中多个网页相同模块的重复样式，如:头部、底部
    * index.css:首页样式



![在这里插入图片描述](https://img-blog.csdnimg.cn/708f3ca3d87f4ff6847422bcf767506c.png)




### 18.6 基础公共样式

* 场景∶一般项目开始前，首先会**去除掉浏览器默认样式**，设置为 **当前项目需要的初始化样式**
* 作用︰防止不同浏览器中标签默认样式不同的影响，统一不同浏览器的默认显示效果，方便后续项目开发
* 要求:需要认识已有代码，项目中可以直接引入使用



## 19、更多

**MDN Web Docs**（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的**免费网站**。

https://developer.mozilla.org/zh-CN/



