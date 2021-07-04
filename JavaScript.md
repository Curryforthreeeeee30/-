# JavaScript

 发表于 2020-10-25  Valine： [0](https://wyqian.top/2020/10/25/JavaScript/JavaScript/#valine-comments)
 本文字数： 19k  阅读时长 ≈ 17 分钟

### 1、什么是JavaScript?



#### 1.1、概述

JavaScript是一门世界上最流行的脚本语言。

Java、JavaScript

10天~

```
一个合格的后端人员，必须要精通JavaScript
```

#### 1.2、JavaScript历史

https://blog.csdn.net/kese7952/article/details/79357868

ECMAScript可以理解成是JavaScript的一个标准。

最新版本已经到ES6了。

但是大部分浏览器还只停留在支持es5代码上！

开发环境（ES6）与线上环境（ES5）版本不一致。

### 2、快速入门

2.1、引入JavaScript

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>js基本入门</title>

    <!--方式一：script标签内，写script代码-->
    <script>
        alert('hello, nju');
    </script>

    <!--方式二：外部引入-->
    <!--需要注意的是：script标签需要成对出现-->
    <script src="js/wyqian.js"></script>

    <!--方式三：加上type属性-->
    <!--这种写法其实没有必要，因为不声明的话，默认也是JavaScript-->
    <script type="text/javascript">

    </script>
</head>
<body>

</body>
</html>
```

#### 2.2、基本语法

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基本入门</title>
    <script>
        //定义变量 变量类型 变量名 = 变量值
        var score = 98;

        //流程控制
        if(score >= 60 && score <70){
            alert('及格');
        }else if(score >= 70 && score < 90){
            alert('良好');
        }else if(score >= 90){
            alert('优秀');
        }
    </script>
</head>
<body>

</body>
</html>
```

经常要使用到的浏览器工具是（浏览器调试必备须知）：

Elements：查看html和CSS；

Console：控制台;

Sources: 调试JavaScript代码;

Network：网络

Application：查看cookies等。

![img](https://i.loli.net/2020/10/25/WJuK1pE3khxrg5B.png)

#### 2.3、数据类型

数值、文本、图形、音频、视频……

***变量\***

```
//支持中文命名，和java一样
var 王者荣耀 = "倔强青铜";
```

***number\***

js不区分小数和整数， Number

```
123//整数123
123.1//浮点数123.1
1.123e3//科学计数法
-99//负数
NaN//not a number
Infinity//表示无限大
```

***字符串\***

‘abs’，”abs”

***布尔值\***

true，false

***逻辑运算\***

```
&&
    
||

!
```

***比较运算符(!!!重要)\***

```
= 
== 等于（类型不一样，值一样，也会判断为true）
=== 绝对等于（类型一样，值一样，结果为true）
```

这是一个JS的缺陷，坚持不要使用`==`比较

须知：

- NaN===NaN，这个与所有的数值都不相等，包括自己。
- 只能通过**isNaN(NaN)**来判断这个数是否是NaN。

***浮点数问题\***

```
1/3 === (1-2/3)//false
```

尽量避免使用浮点数进行运算，存在精度问题。

```
Math.abs(1/3 - (1-2/3)) < 0.00000001
```

***null和undefined\***

- null 空
- undefined 未定义

***数组\***

java：一系列相同类型的对象

Js中不需要这样！

```
//为了保证代码可读性，建议使用[]
var a = [1,2,3,4,5,null,"abc",true];
var b = new Array(1,2,3,true,null,'hello');
```

取数组下标，如果越界了，就会：

```
undefined
```

***对象\***

对象是大括号，数组是中括号。

每个属性之间使用逗号隔开，最后一个不需要添加。

```
var person = {
    name: "wyqian",
    age: 21,
    tags: ["java开发", "科研菜鸟"]
}
```

取对象的值

![img](https://i.loli.net/2020/10/27/wVu6OR8xDvqakiy.png)

#### 2.4、严格检查模式

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>严格检查模式</title>
    <script>
        'use strict'
        /*
        *use strict使用严格检查模式，预防JavaScript的随意性导致的一些问题，前提是IDEA设置了支持ES6语法
        *use strict必须写在javaScript的第一行。
        * */
        //全局变量
        i = 1;
        //局部变量，建议使用let去定义,let-->ES6语法
        let j = 0;
    </script>
</head>
<body>

</body>
</html>
```

### 3、数据类型

#### 3.1、字符串

1、正常字符串我们使用单引号，或者双引号包裹。

2、注意转义字符

```
\'
\n
\t
\u4e2d   \u**** Unicode字符
\x41 ASCll字符
```

3、多行字符串

```
var hi = `
Hello
NJU
你好呀
南大
`;
console.log(hi);
```

4、模板字符串

```
let name="30号公园";
let age = 22;
let str = `你好呀， ${name}，你今年${age}岁了吧`;
console.log(str);
```

5、字符串长度

```
str.length;//str是某一个具体字符串
```

6、字符串可变性—–>不可变

![img](https://i.loli.net/2020/10/27/VnlsyUwf6czTdR1.png)

7、大小写转换

注意这是方法，要包括括号！

```
console.log(Student.toUpperCase())
console.log(Student.toLowerCase())
```

8、子字符串

```
console.log(Student.substring(1,3))//[1，3)，和java一样
console.log(Student.substring(2))//从第2个字符截取到最后一个字符
```

9、indexOf()方法

```
a.indexOf(1);
```

#### 3.2、数组

**Array可以包含任意的数据类型。**

```
var a = [1,2,3,4,5];
```

1、长度

数组的长度是可变的，可以直接给**a.length**赋值，如果值比原数组长度大，那么会多出几个undefined值，如果值比原数组长度小，那么元素会丢失。

![img](https://i.loli.net/2020/10/27/I2zbVLmQX3ZKvRA.png)

2、indexOf()，通过元素获得下标索引

```
a.indexOf(2);
```

字符串的”1”和数字1是不同的。

3、slice()，截取Array的一部分，返回一个新数组，类似于String中的subString()。

```
b.slice(2)
b.slice(3,5)
```

4、push()和pop()，push()向数组尾部添加元素，pop()弹出数组尾部元素。

5、unshift()和shift()方法，unshift()方法向数组头部添加元素，shift()向数组头部添加元素。

![img](https://i.loli.net/2020/10/27/ceyCkUBs8pEI7A2.png)

6、排序 sort()

```
arr = ["B", "D", "C"]
-->["B", "D", "C"]
arr.sort()
-->["B", "C", "D"]
```

7、元素反转 reverse()

```
arr
-->["B", "C", "D"]
arr.reverse()
-->["D", "C", "B"]
```

8、concat()，数组拼接

```
arr
-->["D", "C", "B"]
arr.concat([1,2,3])
-->["D", "C", "B", 1, 2, 3]
```

需要注意的是，arr.sort()和arr.reverse()都是原地操作，但是concat()并没有修改数组，只是会返回一个新数组。

9、连接符

```
arr
-->["D", "C", "B"]
arr.join('~')
-->"D~C~B"
```

10、多维数组

```
arr = [[1,2], [3,4], ["5", "6"]]
arr[1][1]
-->4
```

数组：存储数据（如何存和如何取，方法都可以自己实现！）

#### 3.3、对象

若干个键值对

```
var 对象名 = {
    属性名：属性值,
    属性名：属性值，
    属性名：属性值
}
var person = {
    name: "Durant",
    age: 23,
    address: "NewYork"
}
```

js中对象，{……}表示一个对象，键值对描述属性XXXX：xxxx，多个属性之间用逗号隔开，最后一个属性不加逗号！

**js中所有的键都是字符串，值是任意对象。**

1、对象赋值

```
person.name = "Curry"
person
-->{name: "Curry", age: 23, address: "NewYork"}
```

2、使用一个不存在的对象属性不会报错，会返回undefined

```
person.haha
-->undefined
```

3、动态删减对象属性

```
delete(person.name)
person
-->{age: 23, address: "NewYork"}
delete person.address
person
-->{age: 23}
```

4、动态添加对象属性，直接给新属性添加值就行

```
person.hometown = "夏洛特"
person
-->{age: 23, hometown: "夏洛特"}
```

5、判断某属性是否在对象中

![img](https://i.loli.net/2020/10/27/WhIvpCQM7bRemk3.png)

注意：要加上引号，因为**js中所有的键都是字符串，值是任意对象。**

```
'toString' in person//继承
-->true
```

6、判断一个属性是否是这个对象自身拥有的->使用hasOwnProperty()

![img](https://i.loli.net/2020/10/27/LdHpuI1NmJx92Dw.png)

#### 3.4、流程控制

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>流程控制</title>
    <script>

        var age = 3;
        //if判断
        if(age <= 3){
            console.log("宝贝，你还小，还可以玩~");
        }else if(age >= 5){
            console.log("孩子，你不小了，该学习了");
        }
        //while循环
        //避免程序死循环
        while(age < 100){
            age++;
            console.log(age);
        }
        //do-while循环
        do{
            age++
            console.log(age);
        }while(age < 100);
        //for循环
        var a = [1,2,3,4,5,5,6,6,7];
        for (let i = 0; i < a.length; i++) {
            console.log(a[i]);
        }
        //for-Each循环 es5.1新特性
        var a = [1,2,3,4,5,5,6,6,7];
        a.forEach(function (value) {
            console.log(value);
        });
        //for-in 循环
        var a = [1,2,3,4,5,5,6,6,7];
        for(var num in a){
            console.log(a[num]);
        }
    </script>
</head>
<body>

</body>
</html>
```

#### 3.5、Map和Set

ES6新特性

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Map和Set</title>
    <script>
        'use strict'
        //Map
        var map  = new Map([["Curry",30],["Durant",35],["Klay",11]]);
        console.log(map.get('Curry'));
        //取值
        let curry = map.get('Curry');
        console.log(curry);
        //设置值
        map.set("Lebron",23);
        console.log(map);
        //删除
        map.delete("Lebron");
        
        
        //Set
        var set = new Set();
        set = [1,2,3];
        //添加值
        set.add(4);
        console.log(set);
        //删除值
        set.delete(4);
        console.log(set);
        //是否包含
        console.log(set.has(1));
    </script>
</head>
<body>

</body>
</html>
```

#### 3.6、iterator

> ES6新特性

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Iterator新特性</title>
    <script>
        let arr = [3,4,5];
        //使用for of遍历数组
        console.log("使用for of遍历数组");
        for(let x of arr){
            console.log(x);
        }
        //遍历Map
        let map = new Map([["Curry",30], ["Durant", 35], ["James", 13]]);
        console.log("使用for of遍历Map");
        for(let x of map){
            console.log(x);
        }
        //遍历Set
        let set = new Set([2,4,6]);
        console.log("使用for of遍历Set");
        for(let x of set){
            console.log(x);
        }
    </script>
</head>
<body>

</body>
</html>
```

### 4、函数及面向对象

#### 4.1、定义函数

> 定义函数—-方式一：类似java中的定义方式

```
function abs(x){
    if(x <= 0){
        return -x;
    }else{
        return x;
    }
}
```

> 定义函数—-方式二：前端程序员喜欢用的，将函数赋给一个变量~

```
var abs = function (x){
    if(x <= 0){
        return -x;
    }else{
        return x;
    }
}
```

方式一和方式二是等价的！

> 调用函数

```
abs(10);//10
abs(-10);//-10
abs(); //undefined
abs(2,-3);//2
```

参数问题：js可以传任意个参数，也可以不传递参数~

参数进来是否存在的问题？

假设不存在参数，如何规避？

> 抛出异常的问题

```
var abs = function (x){
    if(typeof x !== 'number'){
        throw '输入的不是一个数！'
    }
    if(x <= 0){
        return -x;
    }else{
        return x;
    }
}
```

> arguments—-知道调用函数者传进来的所有参数！

`arguments`是一个JS免费赠送的关键字；

代表传递进来的所有参数，是一个数组！

```
var abs = function (x){
    for(let i = 0; i < arguments.length; i++){
        console.log("传进来的参数有：" + arguments[i]);
    }
    if(x <= 0 ){
        return -x;
    }else{
        return x;
    }

}
```

![img](https://i.loli.net/2020/10/28/wevrk9B1FDqsybI.png)

`arguments`包含所有的参数，我们有时候想使用多余的参数来进行附加操作，需要排除已有参数。

> rest

`rest`是ES6引入的新特性，获取除了已经定义的参数之外的所有参数，也是一个数组~

`rest`参数只能写在最后面，必须要用…标识，就像下面这种写法就阔以~~~~~

```
var abs = function (x,y,...rest){
    console.log("x=" + x);
    console.log("y=" + y);
    console.log(rest);
}
```

![img](https://i.loli.net/2020/10/28/t84aYsTVeD3qlvy.png)

#### 4.2、作用域和let、const详解

传送门：https://github.com/muzqi/you-dont-know-js。

#### 4.3、方法

对象：属性和方法，把函数赋给一个属性就成了方法。

> 第一种写法

```
let wyqian = {
    name: "wyqian",
    school: "nju",
    birth: 1998,
    age : function (){
        let now = new Date().getFullYear();
        return now - this.birth;
    }
}
wyqian.name;//属性
//调用的时候一定要加上括号
wyqian.age();//方法
而不是：wyqian.age;
```

还可以将函数写在外面，于是乎，就出现了第二种写法：

> 第二种写法

```
function getAge(){
    var now = new Date().getFullYear();
    return now - this.birth;
}
var wyqian = {
    name: 'wyqian',
    school: "nju",
    birth: 1998,
    age: getAge
}
调用：
wyqian.age();
```

由于函数还有一种写法，于是乎也可以这样写：

```
var getAge = function (){
    var now = new Date().getFullYear();
    return now - this.birth;
}
var wyqian = {
    name: 'wyqian',
    school: "nju",
    birth: 1998,
    age: getAge
}
```

> apply的使用

this是无法指向的，是默认指向调用它的那个对象，但是在js中，apply可以this指向。

```
var getAge = function (){
    var now = new Date().getFullYear();
    return now - this.birth;
}
var wyqian = {
    name: 'wyqian',
    school: "nju",
    birth: 1998,
    age: getAge
}
//apply
getAge.apply(wyqian, []);
```

### 5、内部对象

> 标准对象

```
typeof 123
"number"
typeof '123'
"string"
typeof true
"boolean"
typeof NaN
"number"
typeof []
"object"
typeof {}
"object"
typeof undefined
"undefined"
typeof Math.abs
"function"
```

#### 5.1、Date

> 基本使用

```
var now = new Date();
now.getFullYear();//年
now.getMonth();//月
now.getDate();//日
now.getDay();//星期几
now.getHours();//时
now.getMinutes();//分
now.getSeconds();//秒
```

> 转换

```
now.getTime();//时间戳，1970年1月1日 0：00：00 开始至今的毫秒数
var time = new Date(1604125227285);
time.toLocaleString();//转化成当地时间
time.toGMTString();//GMT时区表示
time.toISOString();//ISO表示
```

#### 5.2、JSON

> JSON是什么

早期，所有数据传输习惯使用XML文件！

- [JSON](https://baike.baidu.com/item/JSON)([JavaScript](https://baike.baidu.com/item/JavaScript) Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。
- 简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

在JavaScript中，一切皆为对象，任何JS支持的类型都可以用JSON来表示。

格式：

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用key:value

JSON字符串和JS对象的转化

```
//先定义一个对象
var person = {
    name: "wyqian",
    age: 22,
    school: "NJU"
};
console.log(person);
//对象转换成JSON
let jsonUser = JSON.stringify(person);
console.log(jsonUser);
//JSON转换成对象
let parse = JSON.parse(jsonUser);
console.log(parse);
//实际上jsonUser是一个字符串，于是也可以这样写：
let parse = JSON.parse('{"name":"wyqian","age":22,"school":"NJU"}');
```

总结一下JSON和JS对象的区别：

```
var obj = {a: 'helloa', b: 'hellob'};
var json = '{"a": "helloa", "b":"hellob"}';
```

#### 5.3、Ajax

- 原生的js写法 xhr异步请求
- jQuery封装好的方法 $(“#name”).ajax(“”)
- axios 请求

### 6、面向对象编程

JavaScript、Java、C#。。。。面向对象；javascript有些区别！

- 类：模板 原型对象
- 对象：具体的实例

在JavaScript中需要大家换一下思维方式！

> 面向原型继承

```
var Student = {
    name: "kuangshen",
    age: 24,
    run: function (){
        console.log(this.name + "run...");
    }
}

var xiaoming = {
    name: "xiaoming"
}
xiaoming.__proto__ = Student;
var Bird = {
    fly: function () {
        console.log(this.name + "fly...");
    }
}
xiaoming.__proto__ = Bird;
```

> class继承

类的定义与实例化

```
class Student {
    constructor(name) {
        this.name = name;
    }
    Hello(){
        alert("hello,nju");
    }
}

var xiaoming = new Student(xiaoming);
```

类的继承

```
<script>

    //类的定义与实例化
    class Student {
        constructor(name) {
            this.name = name;
        }
        Hello(){
            alert("hello,nju");
        }
    }

var xiaoming = new Student(xiaoming);

//类的继承
class pupil extends Student{
    constructor(name, age) {
        super(name)
        this.age = age;
    }
    Hello() {
        super.Hello();
        alert("我是一名" + this.age + "岁的小学生");
    }
}

var xiaohong = new pupil(xiaohong, 10);
</script>
```

本质：查看对象原型

![img](https://i.loli.net/2020/11/01/IW87sHpEOehLfRK.png)

> 原型链

![img](https://i.loli.net/2020/11/01/VSKgDlNPL9dehEo.png)

![img](https://i.loli.net/2020/11/01/aFhMpkGQuHBes9U.png)

![img](https://i.loli.net/2020/11/01/slAjtBzeupf1VEZ.png)

### 7、操作BOM对象（重点）

> 浏览器介绍

JavaScript和浏览器关系？

JavaScript诞生就是为了让他在浏览器中运行！

BOM：浏览器对象模型

- IE 6~11
- Chorme
- Safari
- Firefox

三方

- QQ浏览器
- 360浏览器

> Window（重要）

window代表浏览器窗口

```
window.alert(1)
undefined
window.innerHeight
334
window.innerWidth
1920
window.outerWidth
1920
window.outerHeight
1040
//可以调整浏览器窗口试试...
```

> Navigator

Navigator，封装了浏览器的信息

```
navigator.appName
"Netscape"
navigator.appVersion
"5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36"
navigator.userAgent
"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.83 Safari/537.36"
navigator.platform
"Win32"
```

大多数时候，我们不会去使用`navigator`对象，因为会被认为修改！

不建议使用这些属性来判断和编写代码。

> Screen

代表屏幕尺寸

```
screen.height
1080px
screen.width
1920px
```

> Location（重要）

Location代表当前页面的URL信息

```
host: "www.baidu.com"//主机
href: "https://www.baidu.com/"//链接
protocol: "https:"//协议
reload: ƒ reload()//刷新
location.reload();
location.assign("https://www.wyqian.top/");//重定向，面向监狱编程。。。
```

> document

document代表当前页面，HTML DOM文档树

```
document.title
"列表标签学习"
document.title = "wyqian.top"
"wyqian.top"
```

![img](https://i.loli.net/2020/11/01/Qdt4wL3h5KTrpoa.png)

获得具体的文档树节点

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作BOM对象</title>

</head>
<body>

<dl id="app">
    <dt>JAVA</dt>
    <dd>JAVASE</dd>
    <dd>JAVAEE</dd>
</dl>
<script>
    var dl = document.getElementById('app');
</script>

</body>
</html>
```

获取cookie

![img](https://i.loli.net/2020/11/01/y4VABFwY6XHr9JC.png)

劫持cookie原理

[www.taobao.com](http://www.taobao.com/)

```
<script src="aa.js"></script>
//恶意人员：获取你的cookie上传到他的服务器
```

服务器端可以设置cookie：httpOnly.

> history

history代表浏览器的历史记录

```
history.back();//后退
history.forward();//前进
```

### 8、操作DOM对象（重点）

DOM：文档对象模型

> 核心

浏览器网页就是一个DOM树形结构！

- 更新：更新DOM节点
- 遍历Dom节点：得到Dom节点
- 删除：删除一个Dom节点
- 添加：添加一个新的节点

要操作一个DOM节点，就必须先获得这个DOM节点！

![img](https://i.loli.net/2020/11/01/mxytSvBw8LXkcMj.png)

> 获得Dom节点

```
<script>
    let h1 = document.getElementsByTagName("h1");
    let p1 = document.getElementById("p1");
    let p2 = document.getElementsByClassName("p2");

    let father = document.getElementById("father");

    let children = father.children;//获取父节点下所有子节点
    father.firstChild;
    father.lastChild;
</script>
```

> 更新节点

首先获取节点：

```
var id1 = document.getElementById("id1");
```

然后可以给节点赋值：

```
id1.innerText = 'wyqian';
id1.innerHTML = '<a href="http://wyqian.top">博客网址</a>';//可以解析HTML文本标签
```

还可以修改样式：

```
id1.style.color = 'red'//属性使用字符串包装
id1.style.fontSize = '40px'//下划线需要转驼峰命名
```

> 删除节点

删除节点的步骤：先获取父节点，再通过父节点删除自己！

```
<div id="father">
    <h1>标题一</h1>
	<p id="p1">p1</p>
	<p class="p2">p2</p>
</div>

<script>
    let h1 = document.getElementsByTagName("h1");
	let p1 = document.getElementById("p1");
	let p2 = document.getElementsByClassName("p2");

	let father = document.getElementById("father");

	//删除元素
	father.removeChild(p1);
	father.removeChild(p2[0]);
	father.removeChild(h1[0]);
</script>
```

或者使用：对标签、id和class都有效。

```
document.querySelector();
//删除时：
father.removeChild("h1");
father.removeChild("#p1");
father.removeChild(".p2");
```

还有一个经常使用：

```
father.removeChild(father.children[0]);
```

注意：删除多个节点时，children是在时刻变化的！删除节点时一定要注意！

> 插入节点

我们获得了某个DOM节点，假设这个DOM节点是空的，我们通过innerHTML就可以增加一个元素了，但是如果这个DOM节点已经存在元素了，我们就不能这么干了!会产生覆盖。

***追加\***

```
<body>
    <p id="js">JavaScript</p>
    <div id="list">
        <p id="se">JavaSE</p>
        <p id="ee">JavaEE</p>
        <p id="me">JavaME</p>
    </div>
    <script>
        //追加新的节点
        var js = document.getElementById('js');
        var list = document.getElementById('list');
        list.appendChild(js);        
    </script>
</body>
```

这种方式相当于将原来的节点移到了新的地方！

![img](https://i.loli.net/2020/11/04/pWsnFyIgZNPwBb6.png)

***创建新的节点\***

```
//创建新的节点
let newP = document.createElement('p');
newP.id = 'newP';
newP.innerText = '我是一个新节点';
list.append(newP);
```

![img](https://i.loli.net/2020/11/04/u2GygWCjXVhPEQ5.png)

设置id属性也可以使用通用的方法：

```
newP.setAttribute('id', 'newP');
```

***创建一个标签节点\***

```
//创建一个标签节点
let myScript = document.createElement('script');
myScript.setAttribute('type', 'text/javascript');
myScript.setAttribute('id', 'myScript');
list.append(myScript);
```

![img](https://i.loli.net/2020/11/04/VAhJn7s4Hto6MPi.png)

***创建一个style标签\***

```
//创建一个style标签
let myStyle = document.createElement('style');
myStyle.innerHTML = 'body{background-color: blue}';
list.append(myStyle);
```

所以是可以用js而不用html和css写网页的。。。但是我们不会这么干。。。代码可读性不好！

***insertBefore\***

```
//insertBefore
var js = document.getElementById('js');
var list = document.getElementById('list');
var ee = document.getElementById('ee');
list.insertBefore(js, ee);
```

### 9、操作表单（验证）

> 表单是什么 DOM树

- 文本框 text
- 下拉框 
- 单选框 radio
- 多选框 checkbox
- 隐藏域 hidden
- 密码框 password
- ……

表单的目的：提交信息

> 获得要提交的信息

```
<form action="post">
    <p>
        <span>用户名：</span> <input type="text" id="input_text">
    </p>

    <p>
        <span>性别</span> <input type="radio" value="man">男
         <input type="radio" value="woman">女
    </p>
</form>

<script>
    let input_text = document.getElementById('input_text');
    //获取值
    input_text.value;
    //修改值
    input_text.value = 'top';
</script>
```

对于单选框或者复选框，value是固定的，只能使用checked属性去修改是否选中，这一点和文本框不一样！

比如：

```
let man_radio = document.getElementById('man');
//获取值
man_radio.checked;
//修改值
man_radio.checked = true;
```

> 提交表单

使用MD5算法加密

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>提交表单</title>
    <!--MD5工具类-->
    <script src="https://cdn.bootcss.com/blueimp-md5/2.10.0/js/md5.js"></script>
</head>
<body>
<form action="https://www.baidu.com/" method="post" onsubmit="return onClick()">
    <p>
        <span>用户名：</span> <input type="text" id="username" name="username">
    </p>

    <p>
        <span>密码：</span> <input type="password" id="password">
    </p>

    <input type="hidden" name="md5-password" id="md5-password">
    <!--绑定事件：onclick-->
    <button type="submit">提交</button>
</form>
<script>
    function onClick() {
        var uname = document.getElementById('username');
        var pwd = document.getElementById('password');
        var md5_pwd = document.getElementById('md5-password');
        md5_pwd.value = md5(pwd.value);
        return true;
    }
</script>
</body>
</html>
```

### 10、jQuery

JavaScript

jQuery库，里面存在大量的JavaScript函数

> 获取jQuery

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>初识jQuery</title>
<!--    <script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>-->
    <script src="lib/jquery-3.5.1.js"></script>
</head>
<body>
//选择器就是css的选择器
<a href="#" id="a_id">点击跳转</a>
<script>
    $('#a_id').click(function (){
        alert('加油，wyqian');
    })
</script>

</body>
</html>
```

公式：**$(selector).action()**!!!

> 选择器

```
<script>
    //原生js
    document.getElementById('id1');
    document.getElementsByClassName('class1');
    document.getElementsByTagName('h1');
    //jQuery
    $('#id1').click();
    $('.class1').click();
    $('h1').click();
</script>
```

> 事件

鼠标事件、键盘事件、其他事件

举个例子：鼠标移动，实时显示鼠标的位置

效果：

![img](https://i.loli.net/2020/11/05/seDkgnVrvBpiz7F.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件</title>
    <script src="lib/jquery-3.5.1.js"></script>
    <style>
        #divMove{
            width: 500px;
            height: 500px;
            border: 5px solid #3e0653;
        }
    </style>
</head>
<body>

<p>mouse实时位置:<span id="mouseMove"></span></p>
<div id="divMove">
    在这里移动鼠标试试...
</div>

<script>
    //当网页加载完就执行
    $(function (){
        $('#divMove').mousemove(function (e){
            $('#mouseMove').text('x：' + e.pageX + 'y：' + e.pageY);
        })
    })
</script>
</body>
</html>
```

> 操作DOM元素

节点文本操作

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作DOM元素</title>
    <script src="lib/jquery-3.5.1.js"></script>
</head>
<body>
<ul id="ul_id">
    <li id="li_id1">JavaScript</li>
    <li name="JavaSE">JavaSE</li>
</ul>
<script>
    $('#ul_id li[id="li_id1"]').text();//获得值
    $('#ul_id li[id="li_id1"]').text('GO');//设置值
    $('#ul_id li[name="JavaSE"]').html();//获得值
    $('#ul_id li[name="JavaSE"]').html('<strong>youshisinianyuqiandeyitian</strong>');//设置值
</script>
</body>
</html>
```

css操作

```
//css操作
    $('#ul_id li[name="JavaSE"]').css({"color": "red", "fontSize": "30px"});
```

元素的隐藏和显示

```
$('#ul_id li[id="li_id1"]').show();
$('#ul_id li[id="li_id1"]').hide();
$('#ul_id li[id="li_id1"]').toggle();//切换显示隐藏
```

> 小技巧

1、如何巩固JS(看jQuery源码，看游戏源码！)

2、巩固HTML.CSS(扒网站，全部down下来，然后对应修改看效果~)