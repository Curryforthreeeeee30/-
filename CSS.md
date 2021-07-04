# CSS

### 什么是CSS



![img](https://i.loli.net/2020/10/13/l1GEOmWrdhVHRzY.png)

#### 什么是CSS

![img](https://i.loli.net/2020/10/13/gBRrYq5WzIlKAU3.png)

#### CSS的发展史

![img](https://i.loli.net/2020/10/13/BV5Oks1mYR3hX8L.png)

#### 快速入门

style

基本入门：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>我的第一个css程序</title>

<!--规范，<style>可以编写css的代码，每一个声明最好使用分号结尾
语法：
    选择器{
        声明1;
        声明2;
        声明3;
    }
-->
    <style>
        h1{
            color: aqua;
        }
    </style>
</head>
<body>
    <h1>你好，CSS！</h1>
</body>
</html>
```

不过还是建议把内容与表现分离：

![img](https://i.loli.net/2020/10/13/6l2MTuaDYpyCLSI.png)

css的优势：

- 内容与表现分离
- 网页结构表现统一，可以实现复用
- 样式十分地丰富
- 建议使用独立于html的css文件
- 利用SEO，容易被搜索引擎收录

### 四种CSS导入方式

1.行内样式

```
<!--1.行内样式表-->
<h1 style="color: aqua">Hello,NJU!</h1>
```

2.内部样式表

```
<style>
   h1{
      color: blue;
   }
</style>
```

3.外部样式表（链接式）

![img](https://i.loli.net/2020/10/13/mViOsctT7k43Uq9.png)

4.外部样式表（导入式），这是CSS2.1特有的，现在更推荐使用链接式。转载一篇博文介绍@import和link之间的区别https://www.cnblogs.com/passkey/p/10141553.html

```
<style>
   @import "css/style.css";
</style>
```

这里有一个优先级问题，遵循的是就近原则，也就是说离代码近的样式会生效，所以行内样式是优先级最高的。另外几个的话就是谁近谁生效。

### 三种基本选择器

1.标签选择器

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>1.标签选择器</title>

    <style>
        h1{
            /*标签选择器，会选择页面上所有这个标签的元素*/
            background: rosybrown;
            padding-left: 20px;
            border-radius: 20px;
        }
    </style>
</head>
<body>
<h1>Hello, NJU!</h1>
<p>这里是九乡河文理学院</p>
</body>
</html>
```

2.类选择器

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>2.类选择器</title>
    <style>
        /*类选择器：.class名称{}
        好处是将多个标签归类，是同一个class，可以复用
        */
        .curry{
            color: #2121d0;
        }
        .Durant{
            color: bisque;
        }
    </style>
</head>
<body>
<h1 class="curry">斯蒂芬库里</h1>
<h1 class="Durant">杜兰特</h1>
<h1 class="Durant">杜兰特小号</h1>
</body>
</html>
```

3.id选择器

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>id选择器</title>
    <style>
        /*id选择器：id必须全局唯一！使用#id名{}
        优先级：遵循一个原则：id 选择器> 类选择器 > 标签选择器
        */
        .wyqian{
            color: blue;
        }
        #yq{
            color: brown;
        }
        #jz{
            color: cadetblue;
        }
    </style>
</head>
<body>
<h1 class="wyqian" id="jz">标题1</h1>
<h1 id="yq">标题2</h1>
<h1>标题3</h1>
</body>
</html>
```

### 层次选择器

![img](https://i.loli.net/2020/10/19/VqNe3UaJLQCfARr.png)

1、后代选择器：在某个元素的后面，祖爷爷、爷爷、爸爸、你

```
/*后代选择器 选择所有后代元素，不挑~*/
body p{
	background-color: blue;
}
```

2、子选择器，儿子，只有一代

```
/*子代选择器，只选择子代，就是它的“儿子”*/
body > p{
	background-color: chartreuse;
}
```

3、相邻兄弟选择器，只有一个，同辈，相邻（向下）

```
/*相邻兄弟选择器，选择同辈，相邻（向下）*/
.wyqian + p{
    background-color: brown;
}
```

4、通用选择器，当前选中元素的向下的所有兄弟元素

```
/*通用选择器，选择向下所有兄弟元素*/
.wyqian ~ p{
	background-color: darkmagenta;
}
```

### 结构伪类选择器

伪类：条件

```
/*选择的是li父元素的第一个孩子*/
ul li:first-child{
    background-color: #8e1f76;
}
/*选择的是li父元素的最后一个孩子*/
ul li:last-child{
    background-color: #ea25d1;
}
/*选择的是p的父元素的第一个孩子，但是限制是：选中的那个孩子必须得是p标签的*/
p:nth-child(1){
    background-color: #d196ea;
}
/*选择的是第2个p标签的元素*/
p:nth-of-type(2){
    background-color: cyan;
}
```

当然，也可以将标签选择器、类选择器和伪类选择器混合在一起使用，比如：

这种情况也可以使用后面要介绍的属性选择器来实现。

```
a.wyqian:hover{
    color: darkmagenta;
}
<a href="" class="wyqian">Stephen Curry</a>
<br>
<a href="">Stephen Curry</a>
```

### 属性选择器（常用）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>属性选择器</title>

    <style>
        .demo a{
            float: left;
            display: block;
            width: 50px;
            height: 50px;
            background-color: darkmagenta;
            text-align: center;
            text-decoration: none;
            /*line-height: 25px;*/
            margin-right: 5px;
            font: bold 5px/50px Arial;
            border-radius: 5px;
            color: black;
        }

        /*属性选择器：标签名[属性名=属性值]
        =：绝对等于
        *=：通配等于
        ^=：开头等于
        $=：结尾等于
        */

        a[id]{
            background-color: coral;
        }
        a[id="first"]{
            background-color: black;
        }
        a[class="links item"]{
            background-color: coral;
        }
        a[class*="links"]{
            background-color: coral;
        }
        a[href^="http"]{
            background-color: coral;
        }
        a[href$="doc"]{
            background-color: darkcyan;
        }
    </style>
</head>
<body>
    <p class="demo">
        <a href="http://www.baidu.com" class="links item first" id="first">1</a>
        <a href="http:www.wyqian.top/" class="links item active" target="_blank">2</a>
        <a href="images/123.html" class="links item">3</a>
        <a href="images/123.png" class="links item">4</a>
        <a href="images/123.jpg" class="links item">5</a>
        <a href="abc" class="links item">6</a>
        <a href="/a.pdf" class="links item">7</a>
        <a href="/abc.pdf" class="links item">8</a>
        <a href="abc.doc" class="links item">9</a>
        <a href="abcd.doc" class="links item last">10</a>
    </p>
</body>
</html>
```

### CSS的作用及字体样式

#### 为什么要美化网页？

------

1. 有效地传递页面信息
2. 美化网页，页面漂亮，才能吸引用户
3. 凸显页面的主题
4. 提升用户的体验

#### 字体样式

**span**标签：重点要突出的字，使用**span**套起来

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>span标签</title>
    <style>
        #java{
            font-size: 50px;
        }
    </style>
</head>
<body>

<p>欢迎学习<span id="java">java<span/></p>

</body>
</html>
```

设置字体：使用**font**及相关属性

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>font学习</title>

    <style>
        /*
        字体种类：font-family
        字体大小：font-size
        字体粗细：font-weight
        字体颜色：color
        */
        body{
            font-family: 华文楷体;
        }
        h1{
            font-size: 30px;
        }
        .first{
            font-weight: bold;
        }
        .first{
            color: #8e1f76;
        }

    </style>
</head>
<body>

<h1>吹小号的天鹅的童话故事</h1>
<p class="first">
    我正在看我最喜欢的《吹小号的天鹅》，突然，一阵风吹来，书里的主人--小天鹅路易丝出现在了我面前，我惊讶地合不拢嘴，我知道它是一只天生就不会说话的小天鹅，现在，它居然从书里穿越出来了!
</p>

<p>
    我好奇地看着它，说：“路易丝，你好!你居然能从书里穿越出来，你真是太厉害了!”
</p>

<p>
    路易丝点点头，表示同意。我又说：“要不然，我教你学写字吧!”然后，我从我的小黑板旁边的粉笔盒里拿出两支白色的粉笔，一支自己用，一支给路易丝用。我先教它拼音，我写一个字它也照我的写了一个字，我发现，路易丝虽然不会发音，但它的模仿能力非常强。渐渐地，它学会了写拼音，我就教它写字，几个星期后，它就学会了写汉字。
</p>

</body>
</html>
```

当然，也可以使用单独的一个font属性：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>font学习</title>
    <style>
        p{
            font: oblique 100 15px/20px "Times New Roman";
        }
    </style>
</head>
<body>

    <p>
        Dora, the chubby baby panda wasn’t very happy. Because her Milk Tooth was falling out and she did not want to lose it.
    </p>

</body>
</html>
```

font的属性顺序可以按照下面的顺序进行：

font-style–>font-varient–>font-weight–>font-size/line-height–>font-family，font-varient可参考https://www.w3school.com.cn/cssref/pr_font_font-variant.asp

#### 文本样式

1. 颜色：color rgb rgba
2. **文本对齐方式：text-align**
3. **首行缩进：text-indent:2em;**
4. **行高：line-height 单行文字上下居中**line-height = height;
5. 装饰:text-decoration
6. 文本图片水平对齐：vertical-align: middle;

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>文本样式</title>
    <style>
        /*
        颜色：
            单词
            #rgb  0~F
            rgb()
            rgba()  a表示透明度 0~1
        text-align：排版居中
        text-indent:：2em 段落首行缩进
        height: 200px;
        line-height: 200px;
        让height和line-height相等就是垂直居中
        */
        .title_1{
            /*color: #8e1f76;*/
            /*color: red;*/
            /*color: rgb(0,0,255);*/
            color: rgba(0,0,255,0.5);
            text-align: center;
        }
        .first{
            text-indent: 2em;
        }
        .last{
            background-color: rgba(0,255,255, 0.2);
            height: 200px;
            line-height: 200px;
        }
        /*
        下划线：text-decoration: underline;
        中划线：text-decoration: line-through;
        上划线：text-decoration: overline;
        */
        .l1{
            text-decoration: underline;
        }
        .l2{
            text-decoration: line-through;
        }
        .l3{
            text-decoration: overline;
        }
    </style>
</head>
<body>
    <p class="l1">112233</p>
    <p class="l2">112233</p>
    <p class="l3">112233</p>
    <h1 class="title_1">吹小号的天鹅的童话故事</h1>
    <p class="first">
        我正在看我最喜欢的《吹小号的天鹅》，突然，一阵风吹来，书里的主人--小天鹅路易丝出现在了我面前，我惊讶地合不拢嘴，我知道它是一只天生就不会说话的小天鹅，现在，它居然从书里穿越出来了!
    </p>

    <p>
        我好奇地看着它，说：“路易丝，你好!你居然能从书里穿越出来，你真是太厉害了!”
    </p>

    <p class="last">
        路易丝点点头，表示同意。我又说：“要不然，我教你学写字吧!”然后，我从我的小黑板旁边的粉笔盒里拿出两支白色的粉笔，一支自己用，一支给路易丝用。我先教它拼音，我写一个字它也照我的写了一个字，我发现，路易丝虽然不会发音，但它的模仿能力非常强。渐渐地，它学会了写拼音，我就教它写字，几个星期后，它就学会了写汉字。
    </p>
</body>
</html>
```

#### 超链接伪类和文本阴影

超链接伪类主要记住：**a:hover**，然后文本阴影使用的text-shadow属性，属性值的设置可参考该网站https://www.w3school.com.cn/cssref/pr_text-shadow.asp

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>超链接伪类和文本阴影</title>
    <style>

        a{
            color: #000000;
        }
        a:hover{
            color: #8e1f76;
            font-size: 30px;
        }
        #last{
            text-shadow: 0px 5px rgba(0,255, 255, 0.2);
        }
    </style>
</head>
<body>
    <a href="#"><img src="images/a.jpg" alt=""></a>
    <p><a href="#">码出高效-java开发手册</a></p>
    <p><a href="#">作者：孤尽老师</a></p>
    <p id="last">￥99</p>


</body>
</html>
```

#### 列表样式练习

仿京东部分页面

**html文件**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表样式练习</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<div class="nav">
    <h1 class="title_1">全部商品分类</h1>
    <ul class="JS_navCtn cate_menu">
        <li>
            <a href="#">家用电器</a>
        </li>
        <li>
            <a href="#">手机</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">运营商</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">数码</a>
        </li>
        <li>
            <a href="#">电脑</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">办公</a>
        </li>
        <li>
            <a href="#">家居</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">家具</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">家装</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">厨具</a>
        </li>
        <li>
            <a href="#">男装</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">女装</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">童装</a>
            &nbsp;&nbsp;&nbsp;
            <a href="#">内衣</a>
        </li>
    </ul>
</div>

</body>
</html>
```

**style.css文件**

```
.nav{
    background-color: #e9f1e0;
    width: 400px;
}
.title_1{
    font-weight: bold;
    background-color: red;
    text-indent: 1.2em;
}
/*
list-style:
none:去掉圆点
square: 正方形
decimal: 有序列表
*/
ul{
    list-style: none;
}

ul li{
    font-size: 25px;
    height: 40px;
}

a{
    text-decoration: none;
    color: black;
}
a:hover{
    text-decoration: underline;
    color: #ea7d1d;
}
```

#### 背景图像应用及渐变

背景图像使用的是**background-image**属性

然后默认的是平铺，也就是**background-repeat**属性值为**repeat**，但是我们可以改动，比如调整为repeat-x，repeat-y等等。

然后可以在**background-image**属性值中设置图像摆放的位置，具体怎么摆放，建议使用浏览器调试至最佳位置才好。

渐变的话，推荐一个网站：https://www.grabient.com/。 导出的css代码就是**background-image**，比如：

```
background-color: #D9AFD9;
background-image: linear-gradient(315deg, #D9AFD9 0%, #97D9E1 100%);
```

### 盒子模型及边框使用

#### 什么是盒子

![img](https://i.loli.net/2020/10/21/zuEC72wAGsVTNkF.png)

margin: 外边距

padding: 内边距

border: 边框

#### 边框

1. 边框的粗细
2. 边框的样式
3. 边框的颜色

**说明一下：很多标签会自带margin和padding，所以我们经常会将很多标签的margin和padding初始化为0.**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子模型及边框使用</title>
    <style>
        body{
            margin: 0;
            padding: 0;
            text-decoration: none;
        }
        #app{
            /*border: 粗细、样式、颜色*/
            border: 1px solid red;
            width: 300px;
        }
        #first{
            background-color: #b8e5d6;
        }
        div:nth-of-type(1) input{
            border: 1px solid #0a553b;
        }
        div:nth-of-type(2) input{
            border: 1px dashed coral;
        }
    </style>
</head>
<body>

<div id="app">
    <div id="first">
        <h1>京东会员登录</h1>
    </div>
    <form action="">
        <div>
            <span>用户名：</span>
            <input type="text">
        </div>
        <div>
            <span>密码：</span>
            <input type="text">
        </div>

    </form>
</div>

</body>
</html>
```

#### 外边距内边距

margin的写法有：（padding同理）

margin:0;

margin: 0 1px;

margin: 0 2px 3px 4px（顺时针，即上，右，下，左）

如果需要设置某一个方向的margin(padding)，就可以写成：

margin-left，margin-right，margin-top，margin-bottom。

tips:外边距的妙用，可以居中。

```
margin:0 auto;
```

#### 盒子的计算方式：

![img](https://i.loli.net/2020/10/21/APm8WOIHvMRbhTp.png)

margin + border + padding + 内容宽度（高度）

#### 圆角边框

4个角

使用的属性是border-radius，如果写四个值的话，也是顺时针顺序，即左上，右上，右下和左下。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>圆角边框</title>
    <style>
        /*<!--实现的是1/4圆-->*/
        div[class="div1"]{
            width: 50px;
            height: 50px;
            background-color: #8e1f76;
            border-radius: 0 50px 0 0;
        }
        /*实现的是半圆*/
        div[class="div2"]{
            width: 100px;
            height: 50px;
            background-color: #8e1f76;
            border-radius: 50px 50px 0 0;
        }
        /*让图片实现圆形化,具体圆形化多少可以自己调整*/
        img{
            width: 100px;
            height: 100px;
            background-color: #8e1f76;
            border-radius: 50px;
        }
    </style>
</head>
<body>
    <div class="div1"></div>
    <br/>
    <div class="div2"></div>
    <br/>
    <div class="div3"></div>
    <br/>
    <img src="images/wechatTouxiang.jpg" alt="">
</body>
</html>
```

#### 盒子阴影

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>盒子阴影</title>
    <style>
        div[class="first"]{
            width: 100px;
            height: 100px;
            box-shadow: 10px 10px 1px orangered;
        }
    </style>
</head>
<body>
    <div>
        <div class="first" style="margin:0 auto;">
            <img src="images/wechatTouxiang.jpg" alt="">
        </div>
    </div>
</body>
</html>
```

### 浮动

#### 标准文档流

![image-20201023160337946](https://i.loli.net/2020/10/23/tpPMydTxZkYrCQw.png)

块级元素：独占一行

```
h1~h6,p,div,列表
```

行内元素：不独占一行

```
span,a,img,strong
```

行内元素可以被包含在块级元素中，反之，则不可以。

#### display

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>display和浮动</title>
    <style>
        /*
        display取值有：
        block:块级元素
        inline:行内元素
        inline-block:是块元素，但是可以内联，在一行
        none:消失
        */
        div{
            width: 200px;
            height: 200px;
            border: 1px dashed orangered;
            display: none;
        }
        span{
            width: 200px;
            height: 200px;
            border: 1px dashed orangered;
            display: inline-block;
        }
    </style>
</head>
<body>
    <div>div块元素</div>
    <span>span行内元素</span>
</body>
</html>
```

这个是一种实现行内元素排列的方式，但是很多情况都是用**float**。

#### float

```
div{
    margin: 0px;
    padding: 0px;
    border: 1px solid red;
}
.layer1{
    width: 100px;
    height: 100px;
    border: 1px solid black;
    display: inline-block;
    float: right;
}
.layer2{
    width: 50px;
    height: 50px;
    border: 1px solid blue;
    display: inline-block;
    float: right;
    clear: both;
}
.layer3{
    width: 30px;
    height: 30px;
    border: 1px solid yellow;
    display: inline-block;
    float: right;
    clear: both;
}
```

#### 父级边框塌陷的问题

clear

```
/*
clear: right; 右侧不允许有浮动元素，如果有的话就排到下一行
clear: left;  左侧不允许有浮动元素，如果有的话就排到下一行
clear: both;  两侧不允许有浮动
clear: none;
*/
```

解决方案：
1、增加父级元素的高度

```
.outside{
    border: 5px solid red;
    height: 800px;
}
```

2、增加一个空的div标签，清除浮动

```
<div class="clear"></div>

.clear{
    clear: both;
    margin: 0;
    padding: 0;
}
```

3、**overflow**

在父级元素中添加一个overflow属性：

```
overflow: hidden;
```

4、父类添加一个伪类: **after**

```
.outside:after{
    content: '';
    display: block;
    clear: both;
}
```

总结：

- 增加父级高度：简单，但是受限制
- 增加一个空的div标签：简单，但是代码中尽量要避免空div
- overflow：简单，下拉的场景要避免使用
- 父类添加一个伪类after：推荐使用，写法稍微复杂一些，但是没有副作用，推荐使用。

#### display和float对比

- **display**:方向不可以控制
- **float**:方向可以控制，但是要解决父级边框塌陷的问题。

### 定位

#### 相对定位

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>相对定位</title>
    <style>
        div{
            margin: 5px;
            padding: 10px;
            line-height: 25px;
        }
        #father{
            border: 1px solid red;
            background-color: #8e1f76;
        }
        #first{
            border: 1px dashed blue;
            background-color: #b8e5d6;
            position: relative;
            bottom: -50px;
        }
        #second{
            border: 1px dashed #62af63;
            background-color: #787f7d;
            position: relative;
            top: -50px;
        }
        #third{
            border: 1px dashed #b17332;
            background-color: #2f2c2b;
            position: relative;
            right: -20px;
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">
        第一个盒子
    </div>
    <div id="second">
        第二个盒子
    </div>
    <div id="third">
        第三个盒子
    </div>
</div>
</body>
</html>
```

相对定位：position:relative;

相对于原来的位置，进行指定的偏移，相对定位的话，他仍然在标准文档流中，原来的位置会被保留。

#### 相对定位练习

实现的效果如图，有鼠标高亮显示。

![img](https://i.loli.net/2020/10/23/BkT8xSHvVcKOZEo.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>方块定位练习</title>
    <style>
        div{
            width: 600px;
            height: 600px;
            padding: 20px;
        }
        #father{
            border: 2px solid #381b7b;
        }
        a{
            display: block;
            width: 150px;
            height: 150px;
            line-height: 150px;
            background-color: #9a689e;
            text-decoration: none;
            font-size: 20px;
            text-align: center;
        }
        a:hover{
            background-color: orangered;
        }

        #a2, #a5{
            position: relative;
            left: 450px;
            top: -150px;
        }
        #a3{
            position: relative;
            left: 220px;
            top: -80px;
        }
        
    </style>
</head>
<body>
    <div id="father">
        <a href="#" id="a1">链接1</a>
        <a href="#" id="a2">链接2</a>
        <a href="#" id="a3">链接3</a>
        <a href="#" id="a4">链接4</a>
        <a href="#" id="a5">链接5</a>
    </div>
</body>
</html>
```

#### 绝对定位

定位：基于✖✖✖定位，上下左右~

1、没有父级元素定位的前提下，相对于浏览器定位；

2、假设父级元素存在定位，我们通常会相对于父级元素进行偏移；

3、在父级元素范围内移动

相对于父级或者浏览器的位置，进行指定的偏移，绝对定位的话，它不在标准文档流中，原来的位置不会被保留

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>绝对定位</title>
    <style>
        body{
            margin: 0px;
            padding: 0px;
        }
        div{
            margin: 5px;
            padding: 10px;
            line-height: 25px;
        }
        #father{
            border: 1px solid red;
            background-color: #8e1f76;
            padding: 0px;
            position: relative;
        }
        #first{
            border: 1px dashed blue;
            background-color: #b8e5d6;
            position: absolute;
            margin: 0px;
            top: 0px;
        }
        #second{
            border: 1px dashed #62af63;
            background-color: #787f7d;
            /*position: relative;*/
            /*top: -50px;*/
        }
        #third{
            border: 1px dashed #b17332;
            background-color: #2f2c2b;
            /*position: relative;*/
            /*right: -20px;*/
        }
    </style>
</head>
<body>
<div id="father">
    <div id="first">
        第一个盒子
    </div>
    <div id="second">
        第二个盒子
    </div>
    <div id="third">
        第三个盒子
    </div>
</div>
</body>
</html>
```

#### 固定定位

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>固定定位</title>
    <style>
        body{
            height: 1000px;
        }
        div:nth-of-type(1){
            height: 100px;
            width: 100px;
            background-color: #8e1f76;
            position: absolute;
            right: 0;
            bottom: 0;
        }
        div:nth-of-type(2){
            height: 70px;
            width: 70px;
            background-color: #62af63;
            position: fixed;
            right: 0;
            bottom: 0;
        }
    </style>
</head>
<body>

<div>绝对定位</div>
<div>固定定位</div>

</body>
</html>
```

#### z-index

![img](https://i.loli.net/2020/10/25/C4OmMu7Q5nT2API.png)

z-index:默认是0，最高无限~999。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>图层和z-index</title>
    <style>
        body,ul,div{
            margin: 0px;
            padding: 0px;
        }
        #pic ul{
            width: 533px;
            /*父级元素是相对定位，子元素绝对定位*/
            height: 500px;
            overflow: hidden;
        }
        #pic ul{
           position: relative;
        }
        ul li{
            list-style: none;
        }
        .pictext{
            width: 533px;
            height: 25px;
            color: white;
            font-size: 12px;
            line-height: 25px;
            position: absolute;
            top:267px;
            z-index: 999;
        }
        .picbg{
            width: 533px;
            height: 25px;
            background: #8e1f76;
            position: absolute;
            top: 267px;
            opacity: 0.5;
            filter: alpha(opacity=50);/*这一条对之前版本的浏览器有用，所以可以一起加上*/
        }
    </style>
</head>
<body>
    <div id="pic">
        <ul>
            <li class="picreal"><img src="images/a.jpg" alt=""></li>
            <li class="pictext">图源：https://image.baidu.com/</li>
            <li class="picbg"></li>
        </ul>
    </div>
</body>
</html>
```

#### 透明度

```
opacity: 0.5;
filter: alpha(opacity=50);/*这一条对之前版本的浏览器有用，所以可以一起加上*/
```

效果对比图：

**没加透明度的图片：**

![img](https://i.loli.net/2020/10/25/QiwJPpEs97T6It4.png)

**加了透明度的图片（opacity: 0.5;）：**

![img](https://i.loli.net/2020/10/25/4h6rgT9HmIXaKYq.png)

### 动画