# 移动Web

## 1、字体图标

* 目标：使用字体图标实现网页中简洁的图标效果
* 字体图标
  * 字体图标展示的是图标，本质是字体
  * 处理简单的、颜色单一的图片
* 字体图标的优点︰
  * **灵活性∶灵活地修改样式，例如∶尺寸、颜色等**
  * **轻量级∶体积小、渲染快、降低服务器请求次数**
  * **兼容性:几乎兼容所有主流浏览器**
  * 使用方便︰
    1. 下载字体包
    2. 使用字体图标
* 图标库：[iconfont-阿里巴巴矢量图标库](https://www.iconfont.cn/)
* 下载字体包：登录--选择图标库--选择图标--加入购物车--购物车--添加至项目--下载至本地

![在这里插入图片描述](https://img-blog.csdnimg.cn/e91c0c1b3a324404b2f91f55e81d8d14.png#pic_center)






* 使用字体图标：

1. Unicode编码：

![在这里插入图片描述](https://img-blog.csdnimg.cn/6c929333e73c468e81d92b6559e6f8dc.png#pic_center)




* 引入样式表
* 复制粘贴图标对应的Unicode代码

![在这里插入图片描述](https://img-blog.csdnimg.cn/072fbf7bf82c4a47bea2b98b0e2b8258.png#pic_center)


* 设置文字字体

![在这里插入图片描述](https://img-blog.csdnimg.cn/be955e60bdfc4d4d8fbf4b3e4673ed47.png#pic_center)


   



2. 类名：

![在这里插入图片描述](https://img-blog.csdnimg.cn/4ab2f5f743e24e35aa06c0ee9c26e4de.png#pic_center)


* 引入字体图标样式表

![在这里插入图片描述](https://img-blog.csdnimg.cn/f5445dba8a684d0987a60137d6baf174.png)


* 调用图标对应的类名，必须调用2个类名

	* iconfont类：基本样式，包含字体的使用

	* icon-xxx：图标对应的类名

![在这里插入图片描述](https://img-blog.csdnimg.cn/3433c427e8d1417f9671a6fd12b944fb.png)




* 如果图标库没有项目所需的图标，在IconFont网站上传矢量图生成字体图标
  * 与设计沟通，得到SVG矢量图
  * IconFont网站上传图标，下载使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/b9d43a83f88f4e56b9f4d406bad1cd59.png#pic_center)




## 2、平面转换

* 平面转换
  * 改变盒子在平面内的形态（位移、旋转、缩放)
  * 2D转换
* 平面转换属性：transform

![在这里插入图片描述](https://img-blog.csdnimg.cn/c15396c022504466b28e4f8cf8a3a11e.png#pic_center)


* 语法：transform: translate(水平移动距离,垂直移动距离);
* 取值(正负均可)
  * 像素单位数值
  * 百分比(参照物为盒子自身尺寸)
  * **注意:X轴正向为右，Y轴正向为下**
* 技巧
  * translate()如果只给出一个值,表示x轴方向移动距离
  * 单独设置某个方向的移动距离: translatex() & translateY()
* 代码：

~~~html
	<style>
        .father {
            width: 500px;
            height: 300px;
            margin: 100px auto;
            border: 1px solid #000;
        }
        
        .son {
            width: 200px;
            height: 100px;
            background-color: pink;
            transition: all 0.5s;
        }
    
        /* 鼠标移入到父盒子，son改变位置 */
        .father:hover .son {
            /* transform: translate(100px, 50px); */

            /* 百分比: 盒子自身尺寸的百分比 */
            /* transform: translate(100%, 50%); */

            /* transform: translate(-100%, 50%); */

            /* 只给出一个值表示x轴移动距离 */
            /* transform: translate(100px); */

            transform: translateY(100px);
        }
    </style>
~~~



* **使用translate快速实现绝对定位的元素居中效果**
  * 原理：位移取值为百分比数值，参照盒子自身尺寸计算移动距离
* 代码：

~~~html
	<style>
        .father {
            position: relative;
            width: 500px;
            height: 300px;
            margin: 100px auto;
            border: 1px solid #000;
        }
        
        .son {
            position: absolute;
            left: 50%;
            top: 50%;
            /* margin-left: -100px;
            margin-top: -50px; */

            transform: translate(-50%, -50%);

            width: 203px;
            height: 100px;
            background-color: pink;          
        }
    </style>
~~~



* **使用translate实现元素位移效果**
  * left：向左侧移动自身宽度
  * right：向右侧移动自身宽度

![在这里插入图片描述](https://img-blog.csdnimg.cn/af6b243c6055422581b05ca45b9c22f9.png#pic_center)




* **使用rotate实现元素旋转效果**

* 语法：transform: rotate(角度);注意∶角度单位是deg
* 技巧:取值正负均可
  * 取值为正,则顺时针旋转
  * 取值为负,则逆时针旋转

* 代码：

~~~html
	<style>
        img {
            width: 250px;
            transition: all 2s;
        }
        
        img:hover {
            /* 顺 */
            transform: rotate(360deg);

            /* 逆 */
            /* transform: rotate(-360deg); */
        }
    </style>
~~~



* **使用transform-origin属性改变转换原点**
* 语法

  * 默认圆点是盒子中心点
  * transform-origin:原点水平位置原点垂直位置
* 取值
  * 方位名词( left、 top、right、bottom、center )
  * 像素单位数值
  * 百分比(参照盒子自身尺寸计算)

* 代码：

~~~html
	<style>
        img {
            width: 250px;
            border: 1px solid #000;
            transition: all 2s;
            transform-origin: right bottom;
            transform-origin: left bottom;
        }
        
        img:hover {
            transform: rotate(360deg);
        }
    </style>
~~~



* **使用transform复合属性实现多形态转换**
* 多重转换技巧：transform: translate() rotate();
* 多重转换原理
  * 旋转会改变网页元素的坐标轴向
  * 先写旋转，则后面的转换效果的轴向以旋转后的轴向为准，会影响转换结果

* 代码：

~~~html
	<style>
        .box {
            width: 800px;
            height: 200px;
            border: 1px solid #000;
        }
        
        img {
            width: 200px;
            transition: all 8s;
        }
        
        .box:hover img {
            /* 边走边转 */
            transform: translate(600px) rotate(360deg);

            /* 旋转可以改变坐标轴向 */
            /* transform: rotate(360deg) translate(600px); */
            
            /* 层叠性 */
            /* transform: translate(600px);
            transform: rotate(360deg); */
        }
    </style>
~~~



* **使用scale改变元素的尺寸**
* 语法：transform: scale(x轴缩放倍数,y轴缩放倍数);
* 技巧
  * 一般情况下,只为scale设置一个值,表示x轴和y轴等比例缩放
  * transform: scale(缩放倍数);
  * scale值大于1表示放大, scale值小于1表示缩小

* 代码：

~~~html
	<style>
        .box {
            width: 300px;
            height: 210px;
            margin: 100px auto;
            background-color: pink;
            
        }

        .box img {
            width: 100%;
            transition: all 0.5s;
        }
        
        .box:hover img {
            /* width: 150%; */

            transform: scale(1.2);
            transform: scale(0.8);
        }
    </style>
~~~



## 3、渐变

* 渐变是多个颜色逐渐变化的视觉效果
* 一般用于设置盒子的背景
* 代码：

~~~html
	<style>
        .box {
            width: 300px;
            height: 200px;
            /* background-image: linear-gradient(
                pink,
                green,
                hotpink
            ); */
            background-image: linear-gradient(
                transparent,
                rgba(0,0,0, .6)
            );
        }
    </style>
~~~



## 4、空间转换

**空间转换**

* 空间︰是从坐标轴角度定义的。x、y和z三条坐标轴构成了一个立体空间，z轴位置与视线方向相同。
* 空间转换也叫3D转换
* 属性:transform

![在这里插入图片描述](https://img-blog.csdnimg.cn/99855229e69d4807b6cabfadb4a8a534.png#pic_center)




**空间位移**

* 语法
  * transform: translate3d(x, y, z);
  * transform: translateX(值);
  * transform: translateY(值);
  * transform: translateZ(值);
* 取值（正负均可)
  * 像素单位数值
  * 百分比



**透视**

* 生活中，同一个物体观察距离不同，近小远大、近清楚远模糊，Z轴是视线方向，移动效果是距离的远和近

* 属性（添加给父级)

  * perspective:值;
  * 取值∶像素单位数值，数值一般在800 - 1200。
  * 透视距离也称为视距，所谓的视距就是人的眼睛到屏幕的距离。

![在这里插入图片描述](https://img-blog.csdnimg.cn/3c25fd9774ae410ca746d8179a5efd35.png#pic_center)


* 代码：

~~~html
	<style>
    body {
      perspective: 1000px;
      /* perspective: 200px; */
      /* perspective: 10000px; */
    }

    .box {
      width: 200px;
      height: 200px;
      margin: 100px auto;
      background-color: pink;
      transition: all 0.5s;
    }

    .box:hover {
      transform: translateZ(200px);
      /* transform: translateZ(-200px); */
    }
  </style>
~~~

* 作用
  * 空间转换时，为元素添加近大远小、近实远虚的视觉效果



**空间旋转**

* 语法
	* transform: rotateZ(值);
	* transform: rotateX(值);
	* transform: rotateY(值);

* 左手法则：判断旋转方向，左手握住旋转轴,拇指指向正值方向,手指弯曲方向为旋转正值方向

* rotate3d(x，y，z，角度度数)∶用来设置自定义旋转轴的位置及旋转的角度
* x，y，z取值为0-1之间的数字



**立体呈现**

* 实现方法
* 添加transform-style: preserve-3d;使子元素处于真正的3d空间

* 呈现立体图形步骤

  1. 盒子父元素添加transform-style: preserve-3d ;

  2. 按需求设置子盒子的位置（位移或旋转)

* 注意：**空间内，转换元素都有自已独立的坐标轴，互不干扰**

![在这里插入图片描述](https://img-blog.csdnimg.cn/af02fb4dc6be4878944fef080c22f7a4.png#pic_center)


## 5、动画

**使用animation添加动画效果**

* 过渡可以实现两个状态的变化过程
* **动画效果可以实现多个状态间的变化过程，动画过程可控(重复播放、最终画面、是否暂停)**
* 动画的本质是快速切换大量图片时在人脑中形成的具有连续性的画面

* 构成动画的最小单元︰帧或动画帧

* 实现步骤:

1. 定义动画

![在这里插入图片描述](https://img-blog.csdnimg.cn/676de27ca06841c4a9b11f8d139fa2f9.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/05fe58b678734a1888a3f3dd9c5112f3.png#pic_center)


2. 使用动画

![在这里插入图片描述](https://img-blog.csdnimg.cn/caa2e46279b248e0afe4165019e18514.png#pic_center)


* 代码：

~~~html
	<style>
        .box {
            width: 200px;
            height: 100px;
            background-color: pink;

            /* 使用动画 */
            animation: change 1s;
        }

        /* 一. 定义动画：从200变大到600 */
        /* @keyframes change {
            from {
                width: 200px;
            }
            to {
                width: 600px;
            }
        } */
        

        /* 二. 定义动画：200 到 500*300 到 800*500 */
        /* 百分比指的是动画总时长的占比 */
        @keyframes change {
            0% {
                width: 200px;
            }
            50% {
                width: 500px;
                height: 300px;
            }
            100% {
                width: 800px;
                height: 500px;
            }
        }
    </style>
~~~



**使用animation相关属性控制动画的执行过程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/3506438b1f864831b8551811d1eaba7f.png#pic_center)


* 注意:
  * **动画名称和动画时长必须赋值**
  * **取值不分先后顺序**
  * **如果有2个时间值，第一个时间表示动画时长，第二个时间表示延迟时间**

|           属性            |        作用        |                     取值                     |
| :-----------------------: | :----------------: | :------------------------------------------: |
|      animation-name       |      动画名称      |                                              |
|    animation-duration     |      动画时长      |                                              |
|      animation-delay      |      延迟时间      |                                              |
|    animation-fill-mode    | 动画执行完毕时状态 | forwards：最后一帧状态/backwards：第一帧状态 |
| animation-timing-function |      速度曲线      |              steps()：逐帧动画               |
| animation-iteration-count |      重复次数      |              infinite为无限循环              |
|    animation-direction    |    动画执行方向    |               alternate为反向                |
|   animation-play-state    |      暂停动画      |       paused为暂停，通常配合:hover使用       |



**使用steps实现逐帧动画**

|           属性            |   作用   |         取值         |
| :-----------------------: | :------: | :------------------: |
| animation-timing-function | 速度曲线 | steps(数字):逐帧动画 |

* 逐帧动画︰帧动画。开发中，一般配合精灵图实现动画效果。
* animation-timing-function: steps(N);
  * 将动画过程等分成N份



* 精灵动画制作步骤
* 准备显示区域
  * 设置盒子尺寸是一张小图的尺寸，背景图为当前精灵图
* 定义动画
  * 改变背景图的位置（移动的距离就是精灵图的宽度)
* 使用动画
  * 添加速度曲线steps(N)，N与精灵图上小图个数相同
  * 添加无限重复效果

**能够使用animation属性给一个元素添加多个动画效果**

* 多组动画
* 精灵动画的同时添加盒子位移动画
* 代码：

~~~html
	<style>
    .box {
      /* 1680/12 : 保证显示区域的尺寸和一个精灵小图的尺寸相同 */
      width: 140px;
      height: 140px;
      /* border: 1px solid #000; */
      background-image: url(./images/bg.png);

      /* 12: 净零小图的个数 */
      animation: 
        move 1s steps(12) infinite,
        run 1s forwards
      ;
    }


    @keyframes move {
        /* from {
          background-position: 0 0;
        } */
        to {
          /* 1680: 精灵图的宽度 */
          background-position:  -1680px 0;
        }
    }

    /* 定义一个盒子移动的动画  800px */
    @keyframes run {
      /* 动画的开始状态和盒子的默认样式相同的, 可以省略开始状态的代码 */
      /* from {
        transform: translateX(0);
      } */
      to {
        transform: translateX(800px);
      }
    }
  </style>
~~~



## 6、移动端特点

**移动端和PC端网页不同点**

* PC端网页和移动端网页的不同：
  * PC屏幕大，网页固定版心
  * 手机屏幕小，网页宽度多数为100%
* 在电脑里面边写代码边调试移动端网页效果 -- 谷歌模拟器



**谷歌模拟器**

![在这里插入图片描述](https://img-blog.csdnimg.cn/fb6970b41e434820b6bbd15deb36926f.png#pic_center)




**分辨率**

* 屏幕尺寸：指屏幕对角线的长度，一般用英寸来度量

![在这里插入图片描述](https://img-blog.csdnimg.cn/1b68379dbeb941a0a50b15ab8c6a1eda.png#pic_center)




* PC分辨率：
  * 1920*1080
  * 1366*768
  * ...
* 缩放150%：(1920/150%)*(1080/150%)

* 硬件分辨率(出厂设置)；缩放调节的分辨率(软件设置)

* 分辨率分类：

  * 物理分辨率是生产屏幕时就固定的，它是不可被改变的
  * 逻辑分辨率是由软件（驱动)决定的

![在这里插入图片描述](https://img-blog.csdnimg.cn/33da93cd654745719d1da097b3d82b52.png#pic_center)


* **制作网页参考逻辑分辨率**

* 常见移动端主流设备分辨率

![在这里插入图片描述](https://img-blog.csdnimg.cn/2b86e7c4fbd749c8a928c99ac5051598.png#pic_center)




**视口**

* 手机屏幕尺寸都不同，网页宽度为100%
* 网页的宽度和逻辑分辨率尺寸相同
* **默认情况下，网页宽度是980px，如果希望网页宽度和设备宽度(分辨率)相同，可以添加视口标签**
* 视口(viewport)：显示HTML网页的区域，用来约束HTML尺寸

![在这里插入图片描述](https://img-blog.csdnimg.cn/e1606062b64e46f880d8868c74535df3.png#pic_center)


* width = device - width：视口宽度 = 设备宽度
* initial - scale = 1.0：缩放1倍(不缩放)



**二倍图**

* 目标:能够使用像素大厨软件测量二倍图中元素的尺寸
* 图片分辨率,为了高分辨率下图片不会模糊失真
* 现阶段设计稿参考iPhone6/7/8，设备宽度375px产出设计稿
* 二倍图设计稿尺寸:750px



## 7、百分比布局

* 百分比布局，也叫流式布局
* 效果︰宽度自适应，高度固定。



## 8、Flex布局

**Flex**

* 多个盒子横向排列使用**浮动**属性
* 设置盒子间的间距使用**margin**属性
* 需要注意浮动的盒子**脱标问题**
* Flex布局/弹性布局:
  * 是─种浏览器提倡的布局模型
  * 布局网页更简单、灵活
  * **避免浮动脱标的问题**
* 作用：

  * 基于Flex精确灵活控制块级盒子的布局方式，**避免浮动布局中脱离文档流现象发生**。

  * Flex布局非常适合结构化布局
* 设置方式：父元素添加**display: flex**，子元素可以自动的挤压或拉伸

* 组成部分
  * 弹性容器
  * 弹性盒子
  * 主轴
  * 侧轴/交叉轴

![在这里插入图片描述](https://img-blog.csdnimg.cn/8d22c98ea95a4be3a13c0be81cb56a35.png#pic_center)




**主轴对齐方式**

* 在Flex布局模型中，调节主轴或侧轴的对齐方式来设置盒子之间的间距。

* 修改主轴对齐方式属性：justify-content

|    属性值     |                        作用                        |
| :-----------: | :------------------------------------------------: |
|  flex-start   |              默认值，起点开始依次排列              |
|   flex-end    |                  终点开始依次排列                  |
|    center     |                   沿主轴居中排列                   |
| space-around  | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子两侧 |
| space-between | 弹性盒子沿主轴均匀排列，空白间距均分在弹性盒子两侧 |
| space-evenly  | 弹性盒子沿主轴均匀排列，弹性盒子与容器之间间距相等 |

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;

            /* 居中 */
            justify-content: center;

            /* 间距在弹性盒子(子级)之间 */
            justify-content: space-between;

            /* 所有地方的间距都相等 */
            justify-content: space-evenly;

            /* 间距加在子级的两侧 */
            /* 视觉效果: 子级之间的距离是父级两头距离的2倍 */
            justify-content: space-around;
            
            height: 200px;
            margin: auto;
            border: 1px solid #000;
        }
        
        .box div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
~~~



**侧轴对齐方式**

* 修改侧轴对齐方式属性:
  * align-items(添加到弹性容器)
  * align-self:控制某个弹性盒子在侧轴的对齐方式(添加到弹性盒子)

|   属性值   |                   作用                   |
| :--------: | :--------------------------------------: |
| flex-start |         默认值，起点开始依次排列         |
|  flex-end  |             终点开始依次排列             |
|   center   |              沿侧轴居中排列              |
|  stretch   | 默认值，弹性盒子沿着主轴被拉伸至铺满容器 |

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;

            /* 居中 */
            /* align-items: center; */

            /* 拉伸,默认值(现有状态,测试的时候去掉子级的高度) */
            /* align-items: stretch; */

            height: 300px;
            margin: auto;
            border: 1px solid #000;
        }
        
        .box div {
            /* width: 100px; */
            /* height: 100px; */
            background-color: pink;
        }

        /* 单独设置某个弹性盒子的侧轴对齐方式 */
        .box div:nth-child(2) {
            align-self: center;
        }
        
    </style>
~~~



**伸缩比**

* 属性 - flex：值
* 取值分类：数值(整数)
* 注意：只占用父盒子剩余尺寸
* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;

            height: 300px;
            border: 1px solid #000;
        }

        .box div {
            height: 200px;
            margin: 0 20px;
            background-color: pink;
        }

        .box div:nth-child(1) {
            width: 50px;
        }

        .box div:nth-child(2) {
            /* 占用父级剩余尺寸的份数 */
            flex: 3;
        }

        .box div:nth-child(3) {
            flex: 1;
        }
        
    </style>
~~~



**主轴方向**

* 主轴默认是水平方向，侧轴默认是垂直方向
* 修改主轴方向属性: flex-direction

|     属性值     |       作用       |
| :------------: | :--------------: |
|      row       | 行，水平(默认值) |
|     column     |    *列，垂直     |
|  row-reverse   |   行，从右先左   |
| column-reverse |   列，从下向上   |

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style: none;
        }

        .box li {
            display: flex;
            /* 1. 先确定主轴方向; 2. 再选择对应的属性实现主轴或侧轴的对齐方式 */
            /* 修改主轴方向: 列 */
            flex-direction: column;

            /* 当前视觉效果: 实现盒子水平居中 */
            align-items: center;

            /* 当前视觉效果: 垂直居中 */
            justify-content: center;
            

            width: 80px;
            height: 80px;
            border: 1px solid #ccc;
        }
        
        .box img {
            width: 32px;
            height: 32px;
        }
    </style>
~~~



**弹性盒子换行**

* 弹性盒子换行显示: flex-wrap: wrap;
* 调整行对齐方式: align-content
  * 取值与justify-content基本相同

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;

            /* 默认值, 不换行 */
            /* flex-wrap: nowrap; */

            /* 弹性盒子换行 */
            flex-wrap: wrap;

            /* 调节行对齐方式 */
            /* align-content: center; */
            /* align-content: space-around; */
            align-content: space-between;

            height: 500px;
            border: 1px solid #000;
        }
        
        .box div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
~~~



## 9、移动适配

### 9.1 rem

**使用rem单位设置网页元素的尺寸**

* 网页效果：屏幕宽度不同，网页元素尺寸不同（等比缩放)
* px单位或百分比布局可以实现吗?
  * px单位是绝对单位
  * 百分比布局特点宽度自适应，高度固定
* 适配方案
  * **rem**
  * **vw / vh**

* rem单位
  * 相对单位
  * rem单位是**相对于HTML标签的字号**计算结果
  * **1rem = 1HTML字号大小**

*  代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }
        
        /* 1rem = 1html标签字号大小 */
        html {
            font-size: 20px;
        }
        
        .box {
            width: 5rem;
            height: 3rem;
            background-color: pink;
        }
    </style>
~~~



**媒体查询**

* 手机屏幕大小不同，分辨率不同，通过媒体查询设置不同的HTML标签字号
* 媒体查询能够检测视口的宽度，然后编写差异化的CSS样式
* 当某个条件成立,执行对应的CSS样式

* 写法：

![在这里插入图片描述](https://img-blog.csdnimg.cn/7000547bfede42458a06d69efef03d7d.png#pic_center)


* 设备宽度大，元素尺寸大；设备宽度小，元素尺寸小
* 代码：

~~~html
	<style>
        /* 使用媒体查询, 根据不同的视口宽度, 设置不同的根字号 */
        @media (width:375px) {
            html {
                font-size: 40px;
            }
        }

        /* 电脑缩放显示100%情况下 */
        @media (width:320px) {
            html {
                font-size: 30px;
            }
        }
    </style>
~~~



**rem移动适配和适配原理**

* 目前rem布局方案中，将网页等分成10份，**HTML标签的字号为视口宽度的1/10(width:375px -- font-size:37.5px)**

* rem单位尺寸

  1. 根据视口宽度，设置不同的HTML标签字号

  2. 书写代码，尺寸是rem单位
     * 确定设计稿对应的设备的HTML标签字号
     * 查看设计稿宽度→确定参考设备宽度(视口宽度)→确定基准根字号(1/10视口宽度)
     * 2.2 rem单位的尺寸
     * N*37.5 = 68→N= 68/ 37.5
     * rem单位的尺寸= px单位数值/基准根字号



**flexible**

* 使用flexible.js配合rem实现在不同宽度的设备中，网页元素尺寸等比缩放效果

* flexible.js是手淘开发出的一个用来适配移动端的js框架
* 核心原理就是根据不同的视口宽度给网页中html根节点设置不同的font-size

~~~~javascript
(function flexible (window, document) {
  var docEl = document.documentElement
  var dpr = window.devicePixelRatio || 1

  // adjust body font size
  function setBodyFontSize () {
    if (document.body) {
      document.body.style.fontSize = (12 * dpr) + 'px'
    }
    else {
      document.addEventListener('DOMContentLoaded', setBodyFontSize)
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  function setRemUnit () {
    var rem = docEl.clientWidth / 10
    docEl.style.fontSize = rem + 'px'
  }

  setRemUnit()

  // reset rem unit on page resize
  window.addEventListener('resize', setRemUnit)
  window.addEventListener('pageshow', function (e) {
    if (e.persisted) {
      setRemUnit()
    }
  })

  // detect 0.5px supports
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
~~~~



### 9.2 less

* 在px单位转换到rem单位过程中，除法运算比较麻烦，**因为CSS不支持计算写法**
* 解决方案:**可以通过Less实现**
* Less是一个CSS预处理器,Less文件后缀是.less
* 扩充了CSS语言,使CSS具备一定的逻辑性、**计算**能力。
* 注意︰浏览器不识别Less代码，目前阶段，网页要引入对应的CSS文件

* Easy Less :vscode插件
* 作用: less文件保存自动生成css文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/746dc14b44d24307a631d567524e1d77.png#pic_center)


* Less代码：

~~~less
.father {
    color: red;

    width: (68 / 37.5rem);

    .son {
        background-color: pink;
    }
}
~~~

* 自动生成的css代码：

~~~css
.father {
  color: red;
  width: 1.81333333rem;
}
.father .son {
  background-color: pink;
}
~~~



* 注释:
  * 单行注释：语法 ：//注释内容 ；快捷键: ctrl+/
  * 块注释：语法∶/ * 注释内容 */  ；快捷键: shift + alt +A

* 运算:

  * 加、减、乘直接书写计算表达式

  * 除法需要添加小括号 或 . 
* Less代码：

~~~less
.box {
    width: 100 + 10px;
    width: 100 - 20px;
    width: 100 * 2px;

    // 除法
    // 68  -> rem
    width: (68 / 37.5rem);
    height: 29 ./ 37.5rem;
}
~~~

* 自动生成的css代码：

~~~css
.box {
  width: 110px;
  width: 80px;
  width: 200px;
  width: 1.81333333rem;
  height: 0.77333333rem;
}
~~~

* 注意︰表达式存在多个单位以第一个单位为准



**嵌套**

* 作用：**快速生成后代代码**

* 注意：&不生成后代选择器，表示当前选择器，通常配合伪类或伪元素使用

* Less代码：

~~~less
.father {
    width: 100px;

    .son {
        color: pink;

        // & 表示当前选择器
        &:hover {
            color: green;
        }
    }

    &:hover {
        color: orange;
    }
}
~~~

* 自动生成的css代码：

~~~css
.father {
  width: 100px;
}

.father .son {
  color: pink;
}

.father .son:hover {
  color: green;
}

.father:hover {
  color: orange;
}
~~~



**变量**

* 网页中文字颜色基本同一，如果网站改版，变换文字颜色，修改代码方式：
  1. 逐一修改属性值(繁琐)
  2. 把颜色提前存储到一个容器，设置属性值为这个容器名(推荐)

* 把颜色提前存储到一个容器，设置属性值为这个容器名
* 变量:存储数据，方便使用和修改。
* 语法︰
  * 定义变量：**@变量名：值;**
  * 使用变量：CSS属性：**@变量名;**

* Less代码：

~~~less
// 1. 定义. 2.使用
@colora: green;

.box {
    color: @colora;
}

.father {
    background-color: @colora;
}

.aa {
    color: @colora;
}
~~~

* 自动生成的css代码：

~~~css
.box {
  color: green;
}

.father {
  background-color: green;
}

.aa {
  color: green;
}
~~~



**文件操作**

* 开发网站时

  1. CSS：书写link标签
  2. Less：导入

* 导入方式：**@import '文件路径'**

* 导出方式：

  1. 配置EasyLess插件，实现所有Less有相同的导出路径

     * 配置插件︰设置→搜索EasyLess→在setting.json中编辑→添加导出代码（注意，必须是双引号)

  2. 控制当前Less文件导出路径

     * Less文件第一行添加如下代码,注意文件夹名称后面添加/

~~~markdown
// out: ./css/
// out: ./css/common.css
~~~

* 禁止导出：在less文件第一行添加：//out.false

~~~markdown
// out: false
~~~




### 9.3 vw/vh

* 相对单位
  * **相对视口的尺寸**计算结果
  * vw : viewport width；1vw = 1/100视口宽度
  * vh : viewport height；1vh = 1/100视口高度

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        /* 1. vw = 1/100视口宽度 */
        /* .box {
            width: 50vw;
            height: 30vw;
            background-color: pink;
        } */

        /* 2. vh = 1/100视口高度 */
        .box {
            width: 50vh;
            height: 30vh;
            background-color: pink;
        }
    </style>
~~~



**vw适配原理**

* vw单位尺寸
  1. 确定设计稿对应的vw尺寸( 1/100视口宽度)
     * 查看设计稿宽度→确定参考设备宽度(视口宽度)→确定vw尺寸(1/100视口宽度)
  2.  vw单位的尺寸= px单位数值/( 1/100视口宽度)



**vh适配原理**

* vh单位尺寸
  1. 确定设计稿对应的vh尺寸( 1/100视口高度)
     * 查看设计稿宽度→确定参考设备高度(视口高度)→确定vh尺寸( 1/100视口高度)
  2. vh单位的尺寸= px单位数值/( 1/100视口高度)



* 开发中不会混用vw和vh，vh是1/100视口高度，全面屏视口高度尺寸大，如果混用可能会导致盒子变形。



**rem和vw/vh的区别**

* rem：市场比较常见
  1. 需要不断修改html文字大小
  2. 需要媒体查询media
  3. 需要flexible.js

* vw/vh：将来(马上)趋势（推荐）
  1. 省去各种判断和修改
  2. ......



## 10、媒体查询

**基本语法**

* 开发常用写法：max-width(从小到大)、min-width(从大到小)
![在这里插入图片描述](https://img-blog.csdnimg.cn/46a8487b058141f6b25f1439ca977324.png#pic_center)


* 代码：

~~~html
<style>
        /*
            视口宽度 >= 768px，网页背景色是 粉色
            视口宽度 >= 992px，网页背景色是 绿色
            视口宽度 >= 1200px，网页背景色是 skyblue
         */
        @media (min-width: 768px) {
            body {
                background-color: pink;
            }
        }

        @media (min-width: 992px) {
            body {
                background-color: green;
            }
        }

        @media (min-width: 1200px) {
            body {
                background-color: skyblue;
            }
        }
    </style>
~~~

* 书写具有顺序：

![在这里插入图片描述](https://img-blog.csdnimg.cn/5088a14046a24822b84212030cc262f4.png)




**完整写法**

![在这里插入图片描述](https://img-blog.csdnimg.cn/a1f43bff4e2445d68ab9ffe5d5a3a15e.png)


* 关键词：and/only/not

* 媒体类型:媒体是用来区分设备类型的，如屏幕设备、打印设备等，其中手机、电脑、平板都属于屏幕设备

|  类型名称  |   值   |         描述         |
| :--------: | :----: | :------------------: |
|    屏幕    | screen |     带屏幕的设备     |
|  打印预览  | print  |     打印预览模式     |
|   阅读器   | speech |     屏幕阅读模式     |
| 不区分类型 |  all   | 默认值，包含以上三种 |

|    特性名称    |         属性          |              值               |
| :------------: | :-------------------: | :---------------------------: |
|  视口的宽和高  |     width、height     |             数值              |
| 视口最大宽或高 | max-width、max-height |             数值              |
| 视口最大宽或高 | min-width、min-height |             数值              |
|    屏幕方向    |      orientation      | portrait:竖屏/landscape：横屏 |



**外链式引入**

![在这里插入图片描述](https://img-blog.csdnimg.cn/11f903cd595a47e8863090e9bd5df70f.png)


* 代码：

~~~html
	<!-- 视口宽度 >= 992px，网页背景色为粉色 -->
    <!-- 视口宽度 >= 1200px，网页背景色为绿色 -->
    <link rel="stylesheet" href="./one.css" media="(min-width: 992px)">
    <link rel="stylesheet" href="./two.css" media="(min-width: 1200px)">
~~~



**隐藏**

* 代码：

~~~html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;
            width: 100%;
        }

        .left {
            width: 300px;
            min-height: 500px;
            background-color: pink;
        }

        .main {
            flex: 1;
            min-height: 500px;
            background-color: skyblue;
        }

        /* 如果检测到视口宽度小于768px, 认为是手机端, left隐藏 */
        @media (max-width: 768px) {
            .left {
                display: none;
            }
        }
    </style>
~~~



## 11、BootStrap

**UI框架**

* 将常见效果进行统一封装后形成的一套代码,例如:BootStrap
* 作用：基于框架开发，效率高，稳定性高。



**BootStrap简介**

* Bootstrap是由Twitter公司开发维护的前端UI框架，它提供了大量编写好的CSS样式，允许开发者结合一定HTML结构及JavaScript，快速编写功能完善的网页及常见交互效果。

* 中文官网: https://www.bootcss.com/

* 使用：

  1. 下载

![在这里插入图片描述](https://img-blog.csdnimg.cn/470335e2b2b542bbbc04ab95a604d314.png#pic_center)


  2. 引入
  
  ~~~html
  <link rel="stylesheet" href="./bootstrap-03.3.7/css/bootstrap.css">
  ~~~
  
  3. 调用类：使用BootStrap提供的样
     * container :响应式布局版心类
  
  

**BootStrap栅格系统**

![在这里插入图片描述](https://img-blog.csdnimg.cn/701601e1912d497da82a1e063c3dc14c.png#pic_center)


* 栅格化是指将整个网页的宽度分成若干等份
* BootStrap3默认将网页分成12等份

|          | 超小屏幕 |  小屏幕  | 中等屏幕 |  大屏幕  |
| :------: | :------: | :------: | :------: | :------: |
| 响应断点 |  <768px  | >=768px  | >=992px  | >=1200px |
|   别名   |    xs    |    sm    |    md    |    lg    |
| 容器宽度 |   100%   |  750px   |  970px   |  1170px  |
|  类前缀  | col-xs-* | col-sm-* | col-md-* | col-lg-* |
|   列数   |    12    |    12    |    12    |    12    |
|  列间隙  |   30px   |   30px   |   30px   |   30px   |

* 代码：

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>栅格系统</title>
    <link rel="stylesheet" href="./bootstrap-3.4.1-dist/css/bootstrap.min.css">

    <style>
        .container div {
            height: 50px;
            background-color: pink;
        }
    </style>
</head>
<body>
    <!-- 需求: 大屏: 一行排列4个内容; 中屏:一行排列2个内容 -->
    <div class="container">
        <div class="col-lg-3 col-md-6">1</div>
        <div class="col-lg-3 col-md-6">2</div>
        <div class="col-lg-3 col-md-6">3</div>
        <div class="col-lg-3 col-md-6">4</div>
    </div>
    
</body>
</html>
~~~

* .container是Bootstrap中专门提供的类名，所有应用该类名的盒子，默认已被指定宽度且居中
* .container-fluid也是Bootstrap 中专门提供的类名，所有应用该类名的盒子，宽度均为100%
* 分别使用.row类名和.col类名定义栅格布局的行和列。
* 注意：container类自带间距15px；row类自带间距-15px

* 代码：

~~~html
	<!-- 版心样式:自带左右各15px的padding -->
    <div class="container">1</div>

    <!-- row类作用就是抵消container类的15px的内边距(padding), row有-15px的外边距(margin) -->
    <div class="container">
        <div class="row">2</div>
    </div>

    <!-- 宽度100%:自带左右各15px的padding -->
    <div class="container-fluid">3</div>
~~~



**全局样式**

* BootStrap预定义了大量类用来美化页面，掌握手册的查找方法是学习全局样式的重点
* 网站首页→BootStrap3中文文档→全局CSS样式→按分类导航查找目标类

* 布局类：表格
  * table:基本类名,初始化表格默认样式
  * table-bordered :边框线
  * table-striped:隔行变色
  * table-hover:鼠标悬停效果
  * table-responsive :表格宽溢出滚动
  * ......
* 代码：

~~~html
<table class="table table-striped table-bordered table-hover">
~~~

* 美化内容类：按钮
  * btn:基准样式
  * btn-info; btn-success:设置按钮背景色
  * btn-block :设置按钮为块元素
  * btn-lg; btn-sm; btn-xs:设置按钮大小
  * ......

* 代码：

~~~html
<button class="btn btn-success btn-lg">成功</button>
~~~

* 布局类：辅助类
  * pull-right:强制元素右浮动
  * pull-left :强制元素左浮动
  * clearfix:清除浮动元素的影响
  * text-left文:本左对齐
  * text-right :文本右对齐
  * text-center : 文本居中对齐
  * center-block :块元素居中
  * ......



**组件**

* BootStrap提供的常见功能，包含了HTML结构和CSS样式
* 使用方法：
  1. 引入BootStrap样式
  2. 复制结构，修改内容

* 字体图标使用步骤：
  1. HTML页面引入BootStrap样式文件
  2. 准备字体文件(注意路径)
  3. 空标签调用对应类名
     * glyphicon
     * 图标类
* 代码：

~~~html
<i class="glyphicon glyphicon-user"></i>
~~~



**插件**

* 使用方法：

1. 引入BootStrap样式
~~~html
<script src="./js/jquery.js"></script>
<script src="./bootstrap-3.3.7-dist/js/bootstrap.min.js"></script>
~~~

  2.引入js文件: jQuery.js +BootStrap.min.js
  3.复制HTML结构,并适当调整结构或内容



**定制**

* 使用方法：
  1. 导航菜单→定制
  2. 输入目标变量值
  3. 编译并下载，使用定制后的框架



**总结**

* 响应式适用:
  1. 企业站
  2. 内容较少的网站

* 电商站两套布局，移动端用rem/vh、vw适配，企业站用响应式布局

