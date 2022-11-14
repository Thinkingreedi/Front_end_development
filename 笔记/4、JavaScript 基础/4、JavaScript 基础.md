# JavaScript 基础

## 1、JavaScript介绍

* JavaScript是一种运行在客户端（浏览器）的编程语言，实现人机交互效果
* 作用：
  * **网页特效**(监听用户的一些行为让网页作出对应的反馈)
  * **表单验证**(针对表单数据的合法性进行判断)
  * **数据交互**(获取后台的数据,渲染到前端)
  * **服务端编程**(node.js)


![在这里插入图片描述](https://img-blog.csdnimg.cn/5813312733ee4337a2f0866f58c83c26.png#pic_center)



* JavaScript组成：
  * ECMAScript:
    * 规定了js基础语法核心知识。比如:变量、分支语句、循环语句、对象等等
  * Web APls :
    * DOM操作文档，比如对页面元素进行移动、大小、添加删除等操作
    * BOM操作浏览器，比如页面弹窗，检测窗口宽度、存储数据到浏览器等等

![在这里插入图片描述](https://img-blog.csdnimg.cn/6833b1fc82554cf49b2f3f5108de119f.png#pic_center)




* JavaScript书写位置：

![在这里插入图片描述](https://img-blog.csdnimg.cn/f78251752ec44ce9a9de41a0dba1624e.png#pic_center)


1. 内部JavaScript：直接写在html文件里，用script标签包住，写在< /body>上面

   * 注意：我们将< script>放在HTML文件的底部附近的原因是浏览器会按照代码在文件中的顺序加载HTML。**如果先加载的JavaScript期望修改其下方的HTML，那么它可能由于HTML尚未被加载而失效。**

   * 代码：

~~~html
<script>
        alert('你好， js')
</script>
~~~

2. 外部JavaScript：代码写在以.js结尾的文件中，通过script标签，引入html页面中
   * 注意：**< script >标签中间无需写代码，否则会被忽略**
   * 代码：

~~~html
<script src="./my.js"></script>
~~~

3. 内联JavaScript：代码写在标签内部
   * 代码：

~~~html
<button onclick="alert('月薪过万')">点击我</button>
~~~



* JavaScript注释：
  
  1. 单行注释：
     * 符号：//
     * 作用：//右边这一行的代码会被忽略
     * 快捷键：ctrl + /
  2. 块注释：
     * 符号：/* */
     
     * 作用：在/* 和 */之间的所有内容都会被忽略
     
     * 快捷键：shift+alt+A
     
       
  
* JavaScript结束符
  
  * 代表语句结束
  * 英文分号；
  * 可写可不写
  * 换行符会被识别成结束符，所以一个完整的语句，不要手动换行
  
  
  
* JavaScript输入输出语法

~~~html
	<script>
        // 1.document 向body内输入内容
        document.write('我愿意')
        document.write('<h1>我愿意</h1>')
        // 2. alert 页面弹出警告对话框
        //alert('河工大')
        // 3. 控制台输出语法  程序员看的
        //console.log('我是用来测试的')
        // 4. 输入语句 prompt
        //prompt('您今年多大了？')
    </script>
~~~

* 字面量：在计算机科学中，字面量( literal)是在计算机中描述事/物；如数字字面量、字符串字面量，对象字面量...



## 2、变量

* 变量是计算机中用于存储数据的“容器”，它可以让计算机变得有记忆

![在这里插入图片描述](https://img-blog.csdnimg.cn/a49330ee555b4fd8967e5ea947b69da3.png#pic_center)

* 变量的基本使用
  1. 声明变量：声明关键字 变量名;(let age;)
  2. 变量赋值：(age = 18;)
  3. 更新变量：(let age = 18; age = 19;)
  4. 声明多个变量：(let age = 18,name = "haut")

* 变量的本质：是程序在内存中申请的一块用来存放数据的小空间

* 变量命名规则与规范：

  * 规则：
    * **不能用关键字（关键字:有特殊含义的字符，JavaScript内置的一些英语词汇。例如: let、var、if、for等）**
    * **只能用下划线、字母、数字、$组成，且数字不能开头**
    * **字母严格区分大小写，如Age和age是不同的变量**

  * 规范：
    * 起名要有意义
    * 遵守小驼峰命名法：第一个单词首字母小写，后面每个单词首字母大写。例: userName



**扩展：let和var的区别**

* let为了解决var的一些问题
* var声明：
  * 可以先使用再声明(不合理)
  * var声明过的变量可以重复声明(不合理)
  * 比如变量提升、全局变量、没有块级作用域等等

* 暂时统一声明变量时使用let



**扩展：数组**

* 数组是一种可以按顺序保存多个数据
* 声明代码：

~~~html
let 数组名 = [数据1，数据2，..，数据n]
~~~

* 取值代码：

~~~html
数组名[下标]
~~~



## 3、数据类型

![在这里插入图片描述](https://img-blog.csdnimg.cn/96f34c765afb4b6fb4c0413fa12547ba.png#pic_center)


* 数字类型：整数、小数、正数、负数...
* 代码：

~~~html
	<script>
        let age = 18//正整数
        let num = 3.141592653//小数
        let num2 = -12//负数
	</script>
~~~

* **注意：JS是弱数据类型，变量到底属于那种类型，只有赋值之后，我们才能确认**



* 字符串类型：通过单引号（'  ')、双引号（"  ")或反引号(')包裹的数据都叫字符串，单引号和双引号没有本质上的区别，推荐使用单引号。
* 代码：

~~~html
	<script>
        let num = 123
        console.log(num)
        console.log('num')
        let str1 = `老师`
        console.log(str1)
        // 外单内双  外双内单
        console.log('我是"德华"')
        console.log("我是'德华'")
        // console.log('我是\'德华\'') 转义符
    </script>
~~~

* 注意：
  1. 无论单引号或是双引号必须成对使用
  2. 单引号/双引号可以互相嵌套，但是不以自已嵌套自已（**口诀:外双内单，或者外单内双**)
  3. **必要时可以使用转义符\，输出单引号或双引号**
* 字符串拼接：

```html
	<script>      
		let uname = prompt('请输入您的名字')
        document.write('我的名字是：' + uname)
    </script>
```
* 模板字符串：用于拼接字符串和变量
* **符号: ``(内容拼接变量时，用${}包住变量)**

~~~html
	<script>
        // 模板字符串
        let age = 81
        document.write(`'我今年'+(age-20)+'岁了'`)
        document.write(`我今年${age - 20}岁了`)      
    </script>
~~~



* 布尔类型：它有两个固定的值true和false，表示肯定的数据用true(真)，表示否定的数据用false(假)
* 代码：

~~~html
	<script>
        // 布尔型 true false 
        console.log(true)
        console.log(false)
    </script>
~~~

* 注意：



* 未定义类型：只声明变量，不赋值的情况下，变量的默认值为undefined，一般很少【直接】为某个变量赋值为undefined
* 代码：

~~~html
	<script>
        // undefined  只声明不赋值
        let age
        console.log(age)
    </script>
~~~

* 注意：我们开发中经常声明一个变量，等待传送过来的数据。
  如果我们不知道这个数据是否传递过来，此时我们可以通过检测这个变量是不是undefined，就判断用户是否有数据传递过来。



* 空类型
* 代码：

~~~html
	<script>
        //null  空
        let obj = null
        console.log(obj)
    </script>
~~~

* 注意：undefined 表示没有赋值，null表示赋值了，但是内容为空；把null 作为尚未创建的对象



* 控制台输出语句：控制台语句经常用于测试结果来使用。可以看出**数字型和布尔型颜色为蓝色**，**字符串和undefined颜色为灰色**
* 通过typeof关键字检测数据类型：
* 代码：

~~~html
	<script>
        // 检测返回的什么类型  
        console.log(typeof 123)//number
        console.log(typeof '123')//string
        console.log(typeof true)//boolean
        console.log(typeof undefined)//undefined
        console.log(typeof null)//object
        let num = 10
        console.log(typeof num + '11')//number11(字符串拼接)
    </script>
~~~



**扩展：基本数据类型和引用数据类型**

* **简单类型又叫做基本数据类型或者值类型，复杂类型又叫做引用类型**
* 值类型:简单数据类型/基本数据类型，在存储时变量中存储的是值本身，因此叫做值类型string , number,boolean,undefined,null
* 引用类型:复杂数据类型，在存储时变量中存储的仅仅是地址（引用)，因此叫做引用数据类型通过new关键字创建的对象（系统对象、自定义对象），如Object、Array、Date等
* 堆栈空间分配区别:
  1. 栈（操作系统）︰由操作系统自动分配释放存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈;**简单数据类型存放到栈里面**
  2. 堆（操作系统）︰存储复杂类型(对象)，一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。**引用数据类型存放到堆里面**

![在这里插入图片描述](https://img-blog.csdnimg.cn/9304400a2ddd4cceb2e759907e940089.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/2ea3b8dbf0ec42b2a19e347f54542157.png#pic_center)


![在这里插入图片描述](https://img-blog.csdnimg.cn/2dce1e34943f429d910a3d83edabab03.png#pic_center)




## 4、类型转换

* **坑:使用表单、prompt 获取过来的数据默认是字符串类型的，此时就不能直接简单的进行加法运算。**
* 此时需要转换变量的数据类型。通俗来说，就是把一种数据类型的变量转换成我们需要的数据类型。
* 某些运算符被执行时，系统内部自动将数据类型进行转换，这种转换称为**隐式转换**。规则:
  
  * **＋号两边只要有一个是字符串，都会把另外一个转成字符串**
  * **除了+以外的算术运算符比如–、*、/等都会把数据转成数字类型**
  
  * 缺点:转换类型不明确，靠经验才能总结
  * **小技巧: +号作为正号解析可以转换成Number**
* 代码：

~~~html
	<script>
        // let num = prompt('请输入一个数字')
        // console.log(num, typeof num)
        // 内部悄悄的把 18 转换为了字符串的 '18'
        console.log('hauter' + 18)
        console.log(10 + '10')  //  1010
        // - *  / 把 字符串的 '10' 转换为 数字型 10
        console.log(10 - '10') // 0
        // 小技巧
        let num = '10'
        console.log(num)
        console.log(+num)
        // console.log(-num)
        console.log(10 + +'10')//20
    </script>
~~~

* 编写程序时过度依靠系统内部的隐式转换是不严禁的，因为隐式转换规律并不清晰，大多是靠经验总结的规律。为了避免因隐式转换带来的问题，通常根逻辑需要对数据进行**显示转换**。



* **转成数字类型**
  
  * Number(数据)
    * 转成数字类型
    * 如果字符串内容里有非数字，转换失败时结果为NaN(Not a Number）即不是一个数字
    * NaN也是number类型的数据，代表非数字
  * parselnt(数据)
      * 只保留整数
  * parseFloat(数据)
      * 可以保留小数 ，parseFloat 经常用于过滤px单位
  * 代码：
  
  ~~~html
  	<script>
          // let num = '10'  
          // Number(数据)
          console.log(Number('10.01'))
          // 转换为数字型，只保留整数，没有四舍五入
          console.log(parseInt('10'))
          console.log(parseInt('10.111'))
          console.log(parseInt('10.999px'))
          // 转换为数字型，会保留小数
          console.log(parseFloat('10.999'))
      </script>
  ~~~
  
  
  
* **转换为字符型:**
  
  * string(数据)
  * 变量.toString(进制)
  * 代码：

~~~html
	<script>
        console.log(String(10))
        let age = 10
        console.log(age.toString())
        // 括号里面如果是2 转换为 二进制
        console.log(age.toString(2))
    </script>
~~~



## 5、 运算符

**算数运算符**

* 数学运算符也叫算术运算符，主要包括加、减、乘、除、取余（求模)。
  * +：求和
  * -：求差
  * *：求积
  * /：求商
  * %:取模（取余数) -- 开发中经常作为某个数字是否被整除

* 代码：

~~~html
	<script>
        console.log(4 / 2)
        console.log(4 % 2)
        console.log(2 % 4)
        console.log(5 % 8)
    </script>
~~~



**赋值运算符**

* 已经学过的赋值运算符:=将等号右边的值赋予给左边，要求左边必须是一个容器
* 其他赋值运算符:
  * +=
  * -=
  * *=
  * /=
  * %=



**一元运算符**

* 自增:

  * 符号:++
  * 作用:让变量的值＋1

* 自减:
  * 符号:--
  * 作用:让变量的值-1

* 注意：前置自增 -- 先自增后运算；后置自增 -- 先运算后自增

~~~html
	<script>
        let i = 1 
        //			 1    3    3
        console.log(i++ + ++i + i)//7
    </script>
~~~



**比较运算符**

* (>):左边是否大于右边

* (<):左边是否小于右边

* (>=):左边是否大于或等于右边

* (<=):左边是否小于或等于右边

* (==):左右两边是否相等

* (===):**左右两边是否类型和值都相等**

* (!==):左右两边是否不全等

* 比较结果为boolean类型，即只会得到true或false

* 注意：
  * **字符串比较，是比较的字符对应的ASCII码，从左往右依次比较，如果第一位一样再比较第二位，以此类推**
  * **NaN不等于任何值，包括它本身**
  * **尽量不要比较小数，因为小数有精度问题**
  * **不同类型之间比较会发生隐式转换，最终把数据隐式转换转成number类型再比较，所以开发中，如果进行准确的比较我们更喜欢 = = = 或者 ! = =**



**逻辑运算符**

| 符号 |  名称  | 日常读法 |             特点             |   口诀   |
| :--: | :----: | :------: | :--------------------------: | :------: |
|  &&  | 逻辑与 |   并且   | 符号两边都为true结构才是true | 一假则假 |
| \|\| | 逻辑或 |   或者   |  符号两边有一个true就为true  | 一真则真 |
|  ！  | 逻辑非 |   取反   |   true变false/false变true    | 真假颠倒 |

* 短路：只存在于&&(左边为false就短路)和||(左边为true就短路)中，当满足一定条件会让右边代码不执行

* **有5个值是当 false 来看的  其余是真的： false  数字0  ''  undefined  null**



**运算符优先级**

![在这里插入图片描述](https://img-blog.csdnimg.cn/a4d0cfab51504068bbd4677ead41cabe.png#pic_center)



## 6、语句

### 6.1 表达式和语句

* 表达式:表达式是一组代码的集合，JavaScript解释器会将其计算出一个结果

* 语句:js整句或命令，js语句是以分号结束（可以省略)比如: if语句for循环语句

* 区别:表达式计算出一个值，但语句用来自行以使某件事发生(做什么事)


![在这里插入图片描述](https://img-blog.csdnimg.cn/eed7641c45654059b63ed368aee4f6b4.png#pic_center)



### 6.2 分支语句

**if语句**

* if语句有三种使用:单分支、双分支、多分支

* 单分支使用语法：

~~~html
if(条件){
	满足条件要执行的代码
}
~~~

* 括号内的条件为true时，进入大括号里执行代码
* 小括号内的结果若不是布尔类型时，会发生隐式转换转为布尔类型

* 双分支if语法：

~~~html
if(条件){
	满足条件要执行的代码
}else{
	不满足条件执行的代码
}
~~~

* 多分支语法：

~~~html
if(条件1){
	代码1
} else if(条件2){
	代码2
} 
......
else {
	代码n
}
~~~



**三元运算符**

* 语法：

~~~html
条件 ? 满足条件执行的代码 : 不满足条件执行的代码
~~~

* 代码：

~~~html
	<script>
        let num1 = 40
        let num2 = 30
        let re = num1 > num2 ? num1 : num2
        console.log(re)//40
    </script>
~~~



**switch语句**

* 语法：

~~~html
switch(数据){
	case 值1：
		代码1
		break
case 值2：
		代码2
		break
		......
default：
		代码n
		break
}
~~~

* 找到跟小括号里数据全等的case值，并执行里面对应的代码
* 若没有全等===的则执行default里的代码
* **switch case一般需要配合break关键字使用没有break会造成case穿透**



### 6.3 循环语句

**while循环**

* 语法：

~~~html
while(循环条件){
	要重复执行的代码(循环体)
}
~~~



**循环结束**

* continue:结束本次循环，继续下次循环
* break:跳出所在的循环

* 代码：

~~~html
	<script>
        let i = 1
        while (i <= 6) {
            if (i === 3) {
                i++
                // continue 结束本次循环 继续下一次循环
                continue
            }
            document.write(`我要吃第${i}个包子 <br>`)
            i++
        }
    </script>
~~~



**for循环**

* 语法：

~~~html
for(声明记录循环次数的变量;循环条件;变化值){
	循环体
}
~~~

* 当如果明确了循环的次数的时候推荐使用for循环；当不明确循环的次数的时候推荐使用while循环



**循环嵌套**

* 一个循环里再套一个循环，一般用在for循环里

~~~html
for(声明记录循环次数的变量;循环条件;变化值){
	for(声明记录循环次数的变量;循环条件;变化值){
		循环体
	}
}
~~~

* 代码：

~~~html
	<script>
        // 1. 外面的循环 记录第n天 
        for (let i = 1; i < 4; i++) {
            document.write(`第${i}天 <br>`)
            // 2. 里层的循环记录 几个单词
            for (let j = 1; j < 6; j++) {
                document.write(`记住第${j}个单词<br>`)
            }
        }
    </script>
~~~



## 7、数组

**数据简介**

* 数组(Array)是一种可以按顺序保存数据的数据类型

  * 元素:数组中保存的每个数据都叫数组元素
  * 下标:数组中数据的编号
  * 长度:数组中数据的个数，通过数组的length属性获得

  

**数据的基本使用**

* 声明语法：

~~~html
let 数组名 = [数据1，数据2，...，数据n]
~~~

* 数组是按顺序保存，所以每个数据都有自己的编号
* 计算机中的编号从0开始，所以数据1的编号为0，数据2编号为1，以此类推
* 在数组中，数据的编号也叫索引或下标
* 数组可以存储任意类型的数据

* 取值语法：

~~~html
数组名[下标]
~~~

* 遍历数组：

~~~html
for(let i = 0; i < 数组名.length; i++){
          数组名[i]                    
}
~~~

* 代码：

~~~html
<script>
        let arr = [2, 6, 1, 7, 4]
        // 求和变量
        let sum = 0
        // 求平均值变量
        let average = 0
        // 遍历数组
        for (let i = 0; i < arr.length; i++) {
            sum += arr[i]
        }
        average = sum / arr.length
        document.write(`这个同学的总分是: ${sum}, 平均分是:${average}`)
    </script>
~~~



**操作数组**

![在这里插入图片描述](https://img-blog.csdnimg.cn/631b920c98194557a33dc72387884a17.png#pic_center)


* **数组.push()方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度**

~~~html
arr.push(元素1, ... ,元素n)
~~~

* 数组.unshift(新增的内容)方法将一个或多个元素添加到数组的开头，并返回该数组的新长度

~~~html
arr.unshift(元素1, ... ,元素n)
~~~

* **数组. pop()方法从数组中删除最后一个元素，并返回该元素的值**

~~~html
arr.pop()
~~~

* **数组.shift()方法从数组中删除第一个元素，并返回该元素的值**

~~~html
arr.shift()
~~~

* **数组.splice()方法删除指定元素**
  * start 起始位置:指定修改的开始位置（从0计数)
  * deleteCount:表示要移除的数组元素的个数;如果省略则默认从指定的起始位置删除到最后

~~~html
arr.splice(起始位置,删除几个元素)
~~~

* 冒泡排序

~~~html
	<script>
        let arr = [2, 6, 4, 3, 5, 1]
        // 1. 外层循环控制  趟数   循环 4次   arr.length - 1
        for (let i = 0; i < arr.length - 1; i++) {
            // 2. 里层的循环 控制 一趟交换几次  arr.length - i - 1 次序
            for (let j = 0; j < arr.length - i - 1; j++) {
                // 交换两个变量
                // arr[j]   arr[j + 1]
                if (arr[j] > arr[j + 1]) {
                    let temp = arr[j]
                    arr[j] = arr[j + 1]
                    arr[j + 1] = temp
                }
            }
        }
        console.log(arr)
    </script>
~~~



## 8、函数

* 函数:function，是被设计为执行特定任务的代码块
* 说明:函数可以把具有相同或相似逻辑的代码“包裹”起来，通过函数调用执行这些被“包裹”的代码逻辑，这么做的优势是有利于精简代码方便复用。



**函数使用**

* 声明语法：

~~~html
function 函数名(){
	函数体
}
~~~

* 函数体:函数体是函数的构成部分，它负责将相同或相似代码“包裹”起来，直到函数调用时函数体内的代码才会被执行。函数的功能代码都要写在函数体当中
* 函数名命名规范
  * 和变量命名基本一致
  * 尽量小驼峰式命名法
  * 前缀应该为动词
  * 命名建议:常用动词约定

* 函数的调用语法：

~~~html
函数名()
~~~





**函数传参**

* 若函数完成功能需要调用者传入数据，那么就需要用有参数的函数，这样可以极大提高函数的灵活性

* 声明语法:

~~~html
function 函数名(参数列表){
	函数体
}
~~~

* 调用语法：

~~~html
函数名(传递的参数列表)
~~~



**形参与实参**

* 形参:**声明函数时写在函数名右边小括号里的叫形参**（形式上的参数)
* 实参:**调用函数时写在函数名右边小括号里的叫实参**（实际上的参数)
* 形参可以理解为是在这个函数内声明的变量（比如num1 = 10)实参可以理解为是给这个变量赋值
* 开发中尽量保持形参和实参个数一致
* 我们曾经使用过的alert('打印'), parseInt('11'),Number('11')本质上都是函数调用的传参

* 代码：

~~~html
	<script>
        // 声明函数
        function getScore(arr) {
            // arr = [99, 10, 100]
            let sum = 0
            for (let i = 0; i < arr.length; i++) {
                sum += arr[i]
            }
            document.write(sum + '<br>')
        }
        // 调用函数
        getScore([99, 10, 100])
        getScore([100, 100, 100])
    </script>
~~~



**函数返回值**

* 当调用某个函数，这个函数会返回一个结果出来，这就是有返回值的函数
* 当函数需要返回数据出去时，用return关键字
* 语法：

~~~html
return 数据
~~~

* 在函数体中使用return关键字能将内部的执行结果交给函数外部使用
* 函数内部只能出现1次return，并且return后面代码不会再被执行，所以return后面的数据不要换行写
* return会立即结束当前函数
* 函数可以没有return，这种情况函数默认返回值为undefined

* 代码：

~~~html
	<script>
        //返回多个值
        function fn(x, y) {
            let jia = x + y
            let jian = x - y
            return [jia, jian]
        }
        let re = fn(1, 2)   //  [3, -1]
        document.write(`相加之后的结果是：${re[0]},相减之后的结果是: ${re[1]} `)
    </script>
~~~



**作用域**

* 通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而限定这个名字的可用性的代码范围就是这个名字的作用域。作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

![在这里插入图片描述](https://img-blog.csdnimg.cn/d1de897439c34b4f89bdde58088c2e3e.png#pic_center)


* **特殊情况:如果函数内部或者块级作用域内部，变量没有声明，直接赋值，也当全局变量看，但是强烈不推荐；但是有一种情况，函数内部的形参可以看做是局部变量。**

* 变量访问原则-作用域链：
  * 只要是代码，就至少有一个作用域
  * 写在函数内部的局部作用域
  * 如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域
  * 根据在内部函数可以访问外部函数变量的这种机制，用链式查找决定哪些数据能被内部函数访问，就称作作用域链

* **作用域链:采取就近原则的方式来查找变量最终的值**

* 代码：

~~~html
	<script>
        let num = 10
        function fn() {
            let num = 20
            console.log(num)//就近原则 20
        }
        fn()
    </script>
~~~



**匿名函数**

![](https://img-blog.csdnimg.cn/2e1b514c37bd4fdd8860d829478060a2.png#pic_center)


* 将匿名函数赋值给一个变量，并且通过变量名称进行调用我们将这个称为函数表达式
* 语法:

~~~html
let fn = function(){
	//函数体
}
~~~

* 调用：

~~~html
fn()
~~~

* 立即执行函数：避免全局变量之间的污染
* 语法：

~~~html
//方式一
(function(){console.log(11)})();
//方式二
(function(){console.log(11)}());
//不需要调用，立即执行
~~~

* **注意:多个立即执行函数要用 ; 隔开，要不然会报错**



## 9、对象

**对象简介**

* 对象（object) : JavaScript里的一种数据类型，可以理解为是一种无序的数据集合
* 比如描述人信息:
  * 静态特征(姓名,年龄,身高,性别,爱好)=>可以使用数字,字符串,数组，布尔类型等表示
  * 动态行为(点名,唱，跳, rap)=>使用函数表示



**对象使用**

* 对象声明语法：

~~~html
let 对象名 = {
	属性名:属性值,
	方法名:函数
}
~~~

* 对象有属性和方法组成
  * 属性:信息或叫特征（名词)。比如手机尺寸、颜色、重量等..
    * 属性都是成对出现的，包括属性名和值，它们之间使用英文∶分隔
    * 多个属性之间使用英文，分隔
    * 属性就是依附在对象上的变量（外面是变量，对象内是属性)
    * 属性名可以使用""或"，一般情况下省略，除非名称遇到特殊符号如空格、中横线等
  * 方法:功能或叫行为（动词)。比如手机打电话、发短信、玩游戏...
    * 方法是由方法名和函数两部分构成，它们之间使用:分隔
    * 多个属性之间使用英文，分隔
    * 方法是依附在对象中的函数
    * 方法名可以使用""或"，一般情况下省略，除非名称遇到特殊符号如空格、中横线等

* 属性访问：声明对象，并添加了若干属性后，可以使用.或[]获得对象中属性对应的值，称之为属性访问
* 代码：

~~~html
<script>
	let person = {
        name:'andy',
        age:18,
        sex:'男'
    }
    console.log(person.name)//方式一
    console.log(person['name'])//方式二
</script>
~~~

* 方法访问：声明对象，并添加了若干方法后，可以使用﹒调用对象中函数，我称之为方法调用
* 代码：

~~~html
<script>
	let person = {
        name:'andy',
        sayHi:function(){
            document.write('hi~~')
        }
    }
    //对象名.方法名
    person.sayHi()
</script>
~~~



**对象操作**

![在这里插入图片描述](https://img-blog.csdnimg.cn/a06961a7ce314336be513e63201df184.png#pic_center)


* 增加属性：也可以动态为对象添加属性，动态添加与直接定义是一样的，只是语法上更灵活

* 代码：

~~~html
<script>
	let person = {
        name:'andy',
        age:18,
    }
	person.hobby = '足球'
    person['sex'] = '男'
    console.log(person)
</script>
~~~

* 增加方法：也可以动态为对象添加方法，动态添加与直接定义是一样的，只是语法上更灵活

* 代码：

~~~html
<script>
	let person = {
        name:'andy',
        age:18,
    }
	person.move = function(){
        document.write('移动一点点')
    }
</script>
~~~

* 注意:无论是属性或是方法，同一个对象中出现名称一样的，后面的会覆盖前面的。



**遍历对象**

* 对象没有像数组一样的length属性,所以无法确定长度
* 对象里面是无序的键值对，没有规律，不像数组里面有规律的下标
* 代码：

~~~html
<script>
	let obj = {
        uname:'andy',
        age:18,
        sex:'男'
    }
    for(let k in obj){
        console.log(k)//打印属性名
        console.log(obj[k])//打印属性值
    }
</script>
~~~



**内置对象**

* 内置对象Math：Math对象是JavaScript提供的一个“数学高手”对象，提供了一系列做数学运算的方法
* 方法有:
  * random:生成0-1之间的随机数（包含0不包括1)
    * 生成N-M之间的随机数： Math.floor(Math.random()*(M-N+1))+N
  * ceil:向上取整
  * floor:向下取整
  * max:找最大数
  * min:找最小数
  * pow︰幂运算
  * abs:绝对值



## 10、更多

**MDN Web Docs**（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的**免费网站**。

https://developer.mozilla.org/zh-CN/
