# HTML

### 初识HTML



![image-20201006214118747](https://i.loli.net/2020/10/06/kcwrsYK61tbPB5d.png)

![img](https://i.loli.net/2020/10/06/9VcPlOvMwusmF7n.png)

![img](https://i.loli.net/2020/10/06/H9L28qrYZ1dvztP.png)

![img](https://i.loli.net/2020/10/06/bh5RzS96ZodPusq.png)

### 网页基本信息

```
<!-- DOCTYPE:告诉浏览器我们要使用什么规范 -->

<!DOCTYPE html>
<html lang="en">
<!-- head标签代表网页头部 -->
<head>
    <!-- meta描述性标签，它用来描述我们网站的一些信息 -->
    <!-- meta一般用来做SEO(搜索引擎优化) -->
    <meta charset="UTF-8">
    <meta name="keywords" content="狂神说Java,西部开源">
    <meta name="description" content="来这个地方可以学习Java">
    <!-- title标签代表网页标题 -->
    <title>我的第一个网页</title>
</head>

<!-- body标签代表王网页主体 -->
<body>
Hello,World!
</body>
</html>
```

### 网页基本标签

![image-20201007195515829](https://i.loli.net/2020/10/07/ixKCV1cSLu5Nd7e.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基本标签学习</title>
</head>
<body>
<!--标题标签-->
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
<h4>四级标签</h4>
<h5>五级标签</h5>
<h6>六级标签</h6>

<!--段落标签-->
<p>两只老虎，两只老虎，</p>
<p>跑得快，跑得快，</p>
<p>一只没有眼睛，</p>
<p>一只没有尾巴，</p>
<p>真奇怪！真奇怪！。</p>
<p>两只老虎，两只老虎，</p>
<p>跑得快，跑得快，</p>
<p>一只没有耳朵，</p>
<p>一只没有尾巴，</p>
<p>真奇怪！真奇怪！</p>

<!--水平线标签-->
<hr/>

<!--换行标签，比段落标签显得紧凑-->
两只老虎，两只老虎，<br/>
跑得快，跑得快，<br/>
一只没有眼睛，<br/>
一只没有尾巴，<br/>
真奇怪！真奇怪！。<br/>
两只老虎，两只老虎，<br/>
跑得快，跑得快，<br/>
一只没有耳朵，<br/>
一只没有尾巴，<br/>
真奇怪！真奇怪！<br/>

<!--粗体，斜体-->
<h1>字体样式标签</h1>

粗体：<strong>i love you</strong>
斜体：<em>i love you</em>

<br/>
<!--特殊符号-->
空格：Hello,&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nju!
大于号：&gt;
小于号：&lt;
版权所有：&copy;
如果不知道的话，可以百度。
<!--
记忆的话就是： &开头，;结尾
-->
</body>
</html>
```

### 图像标签

![img](https://i.loli.net/2020/10/07/ECaUzfdvWOsnIx1.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>图像标签学习</title>
</head>
<body>
<!--图像标签-->
<!--
src：图像地址，分为相对地址（推荐使用）和绝对地址
    ../  上一级目录
alt：图像文字，图像加载不出来的时候会显示
-->
<img src="../resources/images/wyqian.jpg" alt="http://wyqian.top/" title="个人网站头像" width="400" height="400">
</body>
</html>
```

### 超链接标签及应用

![img](https://i.loli.net/2020/10/07/d2WRFwGufA85nlM.png)

![img](https://i.loli.net/2020/10/07/fryhquLwTgCl3DE.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链接标签学习</title>
</head>
<body>
<a name="top">这里是顶部</a>
<!--页面间链接-->
<!--打开新页面-->
<a href="1.我的第一个网页.html" target="_blank">点击跳转页面一</a>
<!--不打开新页面，在原页面跳转-->
<a href="1.我的第一个网页.html" target="_self">点击跳转页面一</a>

<p>
    <img src="../resources/images/wyqian.jpg" alt="http://wyqian.top/" title="个人网站头像" width="400" height="400">
</p>
<p>
    <img src="../resources/images/wyqian.jpg" alt="http://wyqian.top/" title="个人网站头像" width="400" height="400">
</p>
<p>
    <img src="../resources/images/wyqian.jpg" alt="http://wyqian.top/" title="个人网站头像" width="400" height="400">
</p>
<p>
    <img src="../resources/images/wyqian.jpg" alt="http://wyqian.top/" title="个人网站头像" width="400" height="400">
</p>
<!--锚链接-->
<!--
1.需要一个锚标记，用a标签的name属性。
2.跳转到锚标记，href值为#加上锚标记name属性值。
-->
<a href="#top">回到顶部</a>
<a href="1.我的第一个网页.html#down">跳转到页面一底部</a>
<!--功能性链接：
邮件链接：mailto
-->
<a href="mailto:wanyun_qian@163.com">点击联系我</a>
<br/>
<!--QQ推广已经做好了的-->
<a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=2714332531&site=qq&menu=yes">
    <img border="0" src="http://wpa.qq.com/pa?p=2:2714332531:53" alt="点击这里给我发消息" title="点击这里加我QQ"/></a>
</body>
</html>
```

### 行内元素和块元素

![img](https://i.loli.net/2020/10/07/xKLQXDcrtTb6j5u.png)

### 列表标签

![img](https://i.loli.net/2020/10/07/xwMA7veigCRyhK2.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表标签学习</title>
</head>
<body>
<!--有序列表
应用：试卷、问答...
-->
<ol>
    <li>java</li>
    <li>Python</li>
    <li>C#</li>
    <li>Go</li>
</ol>

<!--无序列表
应用：导航、侧边栏
-->
<ul>
    <li>java</li>
    <li>Python</li>
    <li>C#</li>
    <li>Go</li>
</ul>

<!--自定义列表
应用：网站底部
dl：标签
dt：列表名称
dd：列表内容
-->
<dl>
    <dt>学科</dt>
    <dd>java</dd>
    <dd>Python</dd>
    <dd>C#</dd>
    <dd>Go</dd>

    <dt>水果</dt>
    <dd>苹果</dd>
    <dd>香蕉</dd>
    <dd>橘子</dd>
    <dd>火龙果</dd>
</dl>
</body>
</html>
```

### 表格标签

![img](https://i.loli.net/2020/10/09/7zphOiPjbKwI2ET.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表格学习</title>
</head>
<body>

<!--表格
table：标签
tr:行
td:列
-->
<table border="1px">
    <tr>
        <td colspan="3" align="center">学生成绩</td>
    </tr>

    <tr>
        <td rowspan="2">小狂神</td>
        <td>语文</td>
        <td>100</td>
    </tr>

    <tr>
        <td>数学</td>
        <td>100</td>
    </tr>

    <tr>
        <td rowspan="2">老番茄</td>
        <td>语文</td>
        <td>100</td>
    </tr>

    <tr>
        <td>数学</td>
        <td>100</td>
    </tr>
</table>

</body>
</html>
```

实现的效果就是：

![img](https://i.loli.net/2020/10/09/5mMQ3ONzcA2hWae.png)

### 媒体元素

视频元素：video

音频元素：audio

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>媒体元素学习</title>
</head>
<body>

<!--video和audio
src:资源路径
controls:控制条
autoplay:自动播放
-->
<!--<video src="../resources/video/Simon%20&%20Garfunkel%20-%20The%C2%A0Sound%C2%A0of%C2%A0Silence%C2%A0(《守望者》插曲).mp4" controls autoplay></video>-->
<audio src="../resources/audio/Simon%20&%20Garfunkel%20-%20The%20Sound%20of%20Silence.mp3" controls autoplay></audio>
</body>
</html>
```

说明一下，这里使用autoplay仍然不能自动播放的原因是，谷歌官方已经禁止网页自动播放音频或者视频。

### 页面结构分析

![img](https://i.loli.net/2020/10/09/aFXuBZ79zmJ31Pr.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>页面结构分析学习</title>
</head>
<body>

<header>
    <h2>网页头部</h2>
</header>

<section>
    <h2>网页主题</h2>
</section>

<footer>
    <h2>网页脚部</h2>
</footer>
</body>
</html>
```

### iframe内联框架

```
<iframe src="path" name="mainFrame"></iframe>
```

path是引用页面地址，name是框架标识名。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>iframe内联框架学习</title>
</head>
<body>

<!--<iframe src="http://wyqian.top/" frameborder="0" width="1000px" height="800px"></iframe>-->
<iframe src="" frameborder="0" name="hello" width="1000px" height="800px"></iframe>

<a href="1.我的第一个网页.html" target="hello">点击跳转至第一个网页</a>
</body>
</html>
```

### 初识表单post和get提交

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录注册</title>
</head>
<body>

<!--表单form
action: 表单提交的位置，可以是网站，也可以是请求处理地址
method: 表单提交的方式，有get和post两种
   get提交方式：我们可以在url中看到我们提交的信息，不安全，高效
   post提交方式：比较安全，提交大文件
-->

<form action="1.我的第一个网页.html" method="post">
    <h1>登录注册</h1>
<!--    文本输入框：input type="text"-->
    <p>登录名：<input type="text" name="username"></p>

<!--    密码框：input type="password"-->
    <p>密码：<input type="password" name="pwd"></p>


    <input type="submit">
    <input type="reset">
</form>

</body>
</html>
```

### 文本框和单选框

![img](https://i.loli.net/2020/10/11/PefL6GwEo8VvSyR.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录注册</title>
</head>
<body>

<!--表单form
action: 表单提交的位置，可以是网站，也可以是请求处理地址
method: 表单提交的方式，有get和post两种
   get提交方式：我们可以在url中看到我们提交的信息，不安全，高效
   post提交方式：比较安全，提交大文件
-->

<form action="1.我的第一个网页.html" method="get">
    <h1>登录注册</h1>
<!--    文本输入框：input type="text"
                    value: 默认初始值
                    maxlength: 最长能写几个字符
                    size：文本框的长度
-->
    <p>登录名：<input type="text" name="username" value="30号公园" maxlength="8" size="30"></p>

<!--    密码框：input type="password"-->
    <p>密码：<input type="password" name="pwd"></p>

<!--单选框：input type="radio"
                name；表示组
                value：单选框的值
                checked: 表示默认选中
-->
    <p>性别：
        <input type="radio" name="sex" value="boy" checked/>男
        <input type="radio" name="sex" value="girl"/>女
    </p>
    <input type="submit">
    <input type="reset">
</form>

</body>
</html>
```

### 按钮和多选框

```
<!--    多选框：input type="checkbox"
-->
    <p>多选框：
        <input type="checkbox" name="hobby" value="sleep">睡觉
        <input type="checkbox" name="hobby" value="code" checked>写代码
        <input type="checkbox" name="hobby" value="dance">跳舞
        <input type="checkbox" name="hobby" value="sing">唱歌
    </p>

<!--按钮：input type="button"：普通按钮
         input type="image"：图像按钮
         input type="submit"：提交按钮
         input type="reset"：重置
-->
    <input type="button" name="btn1" value="点击变长"/>
    <input type="image" src="../resources/images/wyqian.jpg">
    <input type="submit">
    <input type="reset">
```

### 列表框、文本域和文件域

```
<!--    下拉框（列表框）
        selected: 表示默认选中
-->
    <p>国家:
        <select name="列表名称">
            <option value="China">中国</option>
            <option value="USA" selected>美国</option>
            <option value="UK">英国</option>
            <option value="Russia">俄罗斯</option>
        </select>
    </p>

<!--    文本域-->
    <textarea name="textarea" id="" cols="30" rows="10">
        文本内容
    </textarea>

<!--    文件域-->
    <p>
        <input type="file" name="file" value="选择文件">
        <input type="button"  name="upload" value="点击上传">
    </p>
```

### 搜索框滑块和简单验证

```
<!--    邮件验证-->
    <p>邮箱：
        <input type="email" name="email">
    </p>
<!--    url验证-->
    <p>URL:
        <input type="url" name="url">
    </p>
<!--    数字验证-->
    <p>number:
        <input type="number" name="number" max="100" min="0" step="1">
    </p>
<!--    滑块-->
    <p>音量：
        <input type="range" name="volume" max="100" min="0" step="1"/>
    </p>
<!--    搜索框-->
    <p>搜索框
        <input type="search" name="search">
    </p>
```

### 表单的应用

- 隐藏域 : hidden
- 只读 : readonly
- 禁用 : disabled

**label**定位到所属id的位置，增强鼠标的可用性

```
<p>
     <!--增强鼠标可用性-->
     <label for="test">你点我试试</label>
     <input type="text" id="test" value="30号公园">
</p>
```

### 表单的初级验证

**placeholder**：用在输入框中，提示信息

**required**：非空判断

**pattern**：正则表达式

```
<p>
   <!--pattern:正则表达式,常用正则表达式https://www.cnblogs.com/zxin/archive/2013/01/26/2877765.HTML，placeholder:提示信息，required:非空判断-->
   <input type="text" name="diyEmail" pattern="^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$" placeholder="请输入邮箱..." required>
</p>
```