

# JavaWeb



Java Web

# 1、基本概念

### 1.1、前言

web开发：

- web，网页的意思，[www.baidu.com](http://www.baidu.com/)
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝，几乎所有的网站；
  - 提供给所有人看的数据始终会发生变化，每个人在不同时间，不同地带你看到的信息各不相同！
  - 技术栈：Servlet/JSP，ASP，PHP

在Java中，动态web资源开发的技术统称为JavaWeb。

### 1.2、web应用程序

Web应用程序：可以提供浏览器访问的程序；

- a.html、b.html…多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上。
- URL：统一资源定位符
- 这些统一的web资源会被放在同一个文件夹下，web应用程序–>Tomcat：服务器
- 一个web应用由多部分组成（静态web，动态web）
  - html,css,js
  - jsp,servlet
  - java程序
  - Jar包
  - 配置文件（Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

### 1.3、静态web

- *.htm,*.html，这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。

  ![img](https://i.loli.net/2020/11/17/aX9ovixC6wzteLB.png)

- 静态web存在的缺点

  - Web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript[实际开发中，它用的最多]
    - VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）

### 1.4、动态web

页面会动态展示：”web页面展示的效果因人而异“；

![img](https://i.loli.net/2020/11/17/LUlPMwskSvBWioO.png)

缺点：

- 假如服务器的动态web资源出现了错误，我们需要重新我们的

  后台程序

  ，重新发布；

  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到的都不是同一个页面
- 它可以和数据库交互（数据持久化：注册，商品信息，用户信息…）

![img](https://i.loli.net/2020/11/17/3ENr1j2uFwMUZSv.png)

新手村：魔鬼训练（分析原理，看源码）–> PK场

## 2、web服务器

### 2.1、技术讲解

**ASP：**

- 微软：国内最早流行的就是ASP；
- 在HTML中嵌入VB的脚本，ASP+COM；
- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其混乱
- 维护成本高！
- C#
- IIS服务器

**PHP：**

- php开发速度很快，功能很强大，跨平台，代码很简单（70%，WP）
- 无法承载大访问量的情况下（局限性）

**JSP/Servlet：**

B/S：浏览器和服务器

C/S：客户端和服务器

- sun公司主推的B/S架构
- 基于Java语言的（所有的大公司，或者一些开源的组件，都是用java写的）
- 可以承载三高问题带来的影响；
- 语法像ASP，ASP–>JSP，加强市场竞争度；

……

### 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息；

**IIS**

微软的；ASP…Windows中自带的

**Tomcat**：

![img](https://i.loli.net/2020/11/17/RfwJZY5j2isnF8W.png)

面向百度编程：

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳选择

Tomcat 实际上运行JSP 页面和Servlet。目前Tomcat最新版本为**9.0.37**。

……

**工作3-5年之后，可以手写Tomcat服务器；**

下载Tomcat：

1. 安装或者解压
2. 了解配置文件及目录问结构
3. 这个东西的作用

## 3、Tomcat

### 3.1、安装Tomcat

官网：https://tomcat.apache.org/

### 3.2、Tomcat启动和配置

文件夹作用：

![img](https://i.loli.net/2020/11/17/ICMceQ4AgxURtK9.png)

**启动、关闭Tomcat**

![img](https://i.loli.net/2020/11/18/Jsw45abCljXqE1o.png)

访问测试：**http://localhost:8080/**

可能遇到的问题：

1. java环境变量没有配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

### 3.3、配置

![img](https://i.loli.net/2020/11/18/xNuP58b1TqKQnXW.png)

可以配置启动的端口号

- tomcat默认端口号是8080
- mysql:3306
- https:443
- http:80

```
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

可以配置主机名称

- 默认的主机名为：localhost->127.0.0.1
- 默认网站应用存放的位置为：webapps

```
<Host name="www.wyqian.com"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_103702.png)

![img](https://i.loli.net/2020/11/18/hjtVD1BiGRSIEf8.png)

**高难度面试题：**

请你谈谈网站是如何进行访问的！

1. 输入一个域名，回车！

2. 检查本机的C:\Windows\System32\drivers\etc\hosts配置文件中是否有这个域名映射

   1. 有：直接返回对应的ip地址，这个地址中有我们需要访问的web程序，可以直接访问

      ```
      127.0.0.1    www.wyqian.com
      ```

   2. 没有，去DNS服务器上找，找得到就返回，找不到就返回找不到

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_105019.png)

可以配置一下环境变量

### 3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放到服务器（Tomcat）中指定的web应用的文件夹（webapps）下，就可以访问了

网站应该有的结构

```
-- webapps:Tomcat服务器的web目录
    -ROOT
    -wyqian:网站的目录名
        - WEB-INF
        	- classes : java程序
            - lib : web应用所依赖的jar包
            - web.xml : 网站配置文件
        - index.html
        - static
             - css
                - style.css
             - js
             - img
         -......
```

## 4、Http

### 4.1、什么是Http

Http(超文本传输协议)是一个简单的请求-响应协议，它通常运行在TCP之上。

- 文本：html,字符串，~…
- 超文本：图片、音频、视频、定位、地图…
- 80

Https:安全的

- 443

### 4.2、两个时代

- http1.0
  - HTTP/1.0：客户端与web服务器连接后，只能获得一个web资源，断开连接
- http2.0
  - HTTP/1.1：客户端与web服务器连接后，可以获得多个web资源

### 4.3、Http请求

- 客户端–发请求–服务器

百度：

```
Request URL: https://www.baidu.com/  请求地址
Request Method: GET   get方法/post方法
Status Code: 200 OK   状态码：200
Remote Address: 182.61.200.7:443 远程ip地址：端口号
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9   语言
Cache-Control: max-age=0    缓存控制
Connection: keep-alive
```

**1、请求行**

- 请求行中的请求方式：GET

- 请求方式：

  GET、POST

  、HEAD、DELETE、PUT、TRACT…

  - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL栏显示数据内容，不安全，但高效
  - post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL栏显示数据内容，安全，但不高效

**2、消息头**

```
Accept: 告诉浏览器（应该是服务器吧...），它所支持的数据类型
Accept-Encoding: 支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language: 告诉浏览器，它的语言环境
Cache-Control: 缓存控制
Connection: 告诉浏览器，请求完成时断开还是保持连接
HOST:主机
```

### 4.4、Http响应

- 服务器–响应–客户端

百度：

```
Cache-Control: private    缓存控制
Connection: keep-alive    连接
Content-Encoding: gzip    编码
Content-Type: text/html;charset=utf-8   类型
```

**1、响应体**

```
Accept: 告诉浏览器（应该是服务器吧...），它所支持的数据类型
Accept-Encoding: 支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language: 告诉浏览器，它的语言环境
Cache-Control: 缓存控制
Connection: 告诉浏览器，请求完成时断开还是保持连接
HOST:主机
Refresh:告诉客户端刷新，多久刷新一次
Location:让网页重新定位；
```

**2、响应状态码（重点）**

200：请求响应成功

3** ：请求重定向

- 重定向：你重新到我给你的新位置去；

4**：找不到资源 404

- 资源不存在

5**：服务器代码错误 500 502：网关错误

**常见面试题**：

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

## 5、Maven

我为什么要学习这个技术？

1. 在JavaWeb开发中，需要使用大量的jar包，我们需要手动去导入；

2. 如何能够让一个东西自动帮我导入和配置这个jar包

   由此，Maven诞生了！

### 5.1、Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven核心思想：**约定大于配置**

- 有约束，不要去违反

Maven会规定好你该如何去编写我们的Java代码，必须按照这个规范来；

### 5.2、下载安装Maven

官网：https://maven.apache.org/

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_160409.png)

下载完成后，解压即可；

### 5.3、配置环境变量

在我们的系统环境变量中

配置如下配置：

- M2_HOME maven目录下的bin目录
- MAVEN_HOME maven的目录
- 在系统的path中配置 %MAVEN_HOME%\bin

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_162239.png)

测试MAVEN是否安装配置成功！

### 5.4、阿里云镜像

- 镜像：mirrors
  - 作用：加速我们的下载
- 国内建议使用阿里云的镜像

```
<mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

### 5.5、本地仓库

在本地的仓库，远程仓库；

**建立一个本地仓库:**

```
<localRepository>C:\Program Files\apache-maven-3.6.3-bin\apache-maven-3.6.3\maven-repo</localRepository>
```

### 5.6、在IDEA中使用Maven

![img](https://wyqian.top/2020/11/17/JavaWeb/JavaWeb/H:%5Chexoblog%5Cblog%5Csource_posts%5CJavaWeb%5C2020-11-18_164710.png)

![img](https://wyqian.top/2020/11/17/JavaWeb/JavaWeb/H:%5Chexoblog%5Cblog%5Csource_posts%5CJavaWeb%5C2020-11-18_164838.png)

![img](https://wyqian.top/2020/11/17/JavaWeb/JavaWeb/H:%5Chexoblog%5Cblog%5Csource_posts%5CJavaWeb%5C2020-11-18_165353.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_165637.png)

等待项目初始化完毕~~~~~

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_165737.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_170533.png)

观察maven仓库中多了什么东西？–>导入了一堆包

IDEA中的Maven配置

注意事项：IDEA项目创建成功后，看一眼Maven的配置

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_171141.png)

到这里，Maven在IDEA中的配置和使用就ok了!

### 5.7、创建一个普通的Maven项目

不用选模板，干净、简单

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_172609.png)

下面这张图展示的是在Web应用下才有的！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_181642.png)

### 5.8、标记文件夹功能

方式一：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_190444.png)

方式二：进入 project structure标记

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_190726.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_191027.png)

### 5.9、在Maven中配置Tomcat

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_191615.png)

解决警告问题：

**必须要的配置：**为什么会有这个问题：**我们访问一个网站，需要指定一个文件夹的名字**

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_191828.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_192216.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_192345.png)

访问成功页面如下：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_193736.png)

### 5.10、pom文件

pom.xml是Maven的核心配置文件

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_194107.png)

```
<?xml version="1.0" encoding="UTF-8"?>

<!--  Maven头文件和版本-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

<!--这里就是我们创建项目时候配置的GAV-->
  <groupId>com.kuang</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--  Package:项目的打包方式
jar:java应用
war:JavaWeb应用
-->
  <packaging>war</packaging>

<!--配置-->
  <properties>
<!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<!--编码版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

<!--项目依赖-->
  <dependencies>
    <dependency>
<!--项目依赖的具体jar包-->
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
<!--项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_201731.png)

Maven由于约定大于配置，可能会出现资源无法导出的情况，解决方案：

```
<!--在build中配置resources，防止出现maven资源导出失败的问题-->
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```

### 5.11、IDEA操作

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_202456.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_202445.png)

5.12、遇到的一些问题

1、Maven默认项目中的web.xml版本问题

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-18_204643.png)

2、可以替换成新版本，与Tomcat保持一致

```
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
</web-app>
```

3、Maven仓库的使用

地址：https://mvnrepository.com/

## 6、Servlet

### 6.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的Java类部署到web服务器中。

**把实现了Servlet接口的Java程序叫做：Servlet**。

### 6.2、HelloServlet

Servlet接口Sun公司有两个默认的实现类：HttpServlet，GenericServlet

1、构建一个普通的Maven项目，删掉里面的src目录，以后我们的学习就在这个项目里面建立Module;这个空的工程就是Maven主工程；

2、关于Maven父子工程的理解：

父项目中会有

```
<modules>
    <module>Servlet-01</module>
</modules>
```

子项目中会有

```
<parent>
    <groupId>org.example</groupId>
    <artifactId>javaweb-maven06</artifactId>
    <version>1.0-SNAPSHOT</version>
</parent>
```

父项目中的java子项目可以直接使用

```
son extends father
```

3、Maven环境优化

1. 修改web.xml为最新的
2. 将maven的结构搭建完整

4、编写一个Servlet程序

1. 编写一个普通类
2. 实现Servlet接口，这里我们直接继承HttpServlet

```
package com.wyqian.Servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class helloServlet extends HttpServlet {
    //由于get和post只是提交方式不同，业务逻辑是一样的，可以相互调用
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        PrintWriter writer = resp.getWriter();//响应流

        writer.println("ComeonStephen");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

5、编写Servlet映射

为什么需要映射：我们写的是JAVA程序，但是需要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给他一个浏览器能够访问的路径。

```
<servlet>
    <servlet-name>helloServlet</servlet-name>
    <servlet-class>com.wyqian.Servlet.helloServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet</url-pattern>
</servlet-mapping>
```

6、配置Tomcat

注意：配置项目发布的路径就可以了。

7、启动测试

### 6.3、Servlet原理

Servlet是由Web服务器调用，web服务器在收到浏览器请求之后，会：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-22_174738.png)

①：Tomcat将http请求文本接收并解析，然后封装成HttpServletRequest类型的request对象，所有的HTTP头数据读可以通过request对象调用对应的方法查询到。

②：Tomcat同时会要响应的信息封装为HttpServletResponse类型的response对象，通过设置response属性就可以控制要输出到浏览器的内容，然后将response交给tomcat，tomcat就会将其变成响应文本的格式发送给浏览器

### 6.4、Mapping

1、一个Servlet可以指定一个映射路径

```
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet</url-pattern>
</servlet-mapping>
```

2、一个Servlet可以指定多个映射路径

```
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet2</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet3</url-pattern>
</servlet-mapping>
```

3、一个Servlet可以指定通用映射路径

```
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet/*</url-pattern>
</servlet-mapping>
```

4、默认请求路径

```
<!--默认请求路径-->
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

5、指定一些后缀或者前缀等等…

```
<!--
指定后缀是do，前面可以随便怎么写，最后以do结尾就行
比如：http://localhost:8080/wyqian/dfasjfh/fhausi.do
-->
<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>*.do</url-pattern>
</servlet-mapping>
```

6、优先级问题

指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求

```
<servlet>
    <servlet-name>helloServlet</servlet-name>
    <servlet-class>com.wyqian.Servlet.helloServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/helloServlet</url-pattern>
</servlet-mapping>

<servlet>
    <servlet-name>error</servlet-name>
    <servlet-class>com.wyqian.Servlet.error</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>error</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

### 6.5、ServletContext

Web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用。

#### 1、共享数据

我在这个Servlet中保存数据，可以在另外一个Servlet中拿到

***保存数据\***

```
package com.wyqian.Servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class helloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

//        this.getInitParameter();//初始化参数
//        this.getServletConfig();//配置
        ServletContext context = this.getServletContext();//获取上下文

        context.setAttribute("username", "钱万云");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

***获取数据\***

```
package com.wyqian.Servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class getC extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();//获取上下文
        String username = (String) context.getAttribute("username");

        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html");

        resp.getWriter().println(username);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

***配置xml\***

```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
  <servlet>
    <servlet-name>helloServlet</servlet-name>
    <servlet-class>com.wyqian.Servlet.helloServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>helloServlet</servlet-name>
    <url-pattern>/hello</url-pattern>
  </servlet-mapping>
  
  <servlet>
    <servlet-name>getC</servlet-name>
    <servlet-class>com.wyqian.Servlet.getC</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>getC</servlet-name>
    <url-pattern>/getC</url-pattern>
  </servlet-mapping>
</web-app>
```

#### 2、获取初始化参数

```
<!--配置一些web应用初始化参数-->
<context-param>
    <param-name>url</param-name>
    <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
</context-param>
package com.wyqian.Servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext sC = this.getServletContext();
        String url = sC.getInitParameter("url");
        resp.getWriter().println(url);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

#### 3、请求转发

```
<servlet>
    <servlet-name>sd</servlet-name>
    <servlet-class>com.wyqian.Servlet.ServletDemo04</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>sd</servlet-name>
    <url-pattern>/sd</url-pattern>
</servlet-mapping>
package com.wyqian.Servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletDemo04 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();

        System.out.println("进入了ServletDemo04");
        servletContext.getRequestDispatcher("/*.do").forward(req,resp);//请求转发，路径不变，与重定向是不同的
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-23_214009.png)

#### 4、读取资源文件

Properties

- 在java目录下新建properties
- 在resources目录下新建properties

发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath

properties:

```
username=wyqian
password=123456
```

Servlet映射:

```
<servlet>
    <servlet-name>sd5</servlet-name>
    <servlet-class>com.wyqian.Servlet.ServletDemo05</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>sd5</servlet-name>
    <url-pattern>/sd5</url-pattern>
</servlet-mapping>
```

java文件：

```
package com.wyqian.Servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();

        InputStream is = servletContext.getResourceAsStream("/WEB-INF/classes/db.properties");//“/”不能少

        Properties prop = new Properties();

        prop.load(is);

        String username = prop.getProperty("username");
        String pwd = prop.getProperty("password");

        resp.getWriter().print(username + ":" + pwd);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### 6.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse。

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 1、简单分类

**负责向浏览器发送数据的方法**

```
ServletOutputStream getOutputStream() throws IOException;

PrintWriter getWriter() throws IOException;
```

**负责向浏览器发送响应头的方法**

```
void setCharacterEncoding(String var1);

void setContentLength(int var1);

void setContentType(String var1);

void setBufferSize(int var1);

void setDateHeader(String var1, long var2);

void addDateHeader(String var1, long var2);

void setHeader(String var1, String var2);

void addHeader(String var1, String var2);

void setIntHeader(String var1, int var2);

void addIntHeader(String var1, int var2);
```

**响应的状态码**

```
int SC_CONTINUE = 100;
int SC_SWITCHING_PROTOCOLS = 101;
int SC_OK = 200;
int SC_CREATED = 201;
int SC_ACCEPTED = 202;
int SC_NON_AUTHORITATIVE_INFORMATION = 203;
int SC_NO_CONTENT = 204;
int SC_RESET_CONTENT = 205;
int SC_PARTIAL_CONTENT = 206;
int SC_MULTIPLE_CHOICES = 300;
int SC_MOVED_PERMANENTLY = 301;
int SC_MOVED_TEMPORARILY = 302;
int SC_FOUND = 302;
int SC_SEE_OTHER = 303;
int SC_NOT_MODIFIED = 304;
int SC_USE_PROXY = 305;
int SC_TEMPORARY_REDIRECT = 307;
int SC_BAD_REQUEST = 400;
int SC_UNAUTHORIZED = 401;
int SC_PAYMENT_REQUIRED = 402;
int SC_FORBIDDEN = 403;
int SC_NOT_FOUND = 404;
int SC_METHOD_NOT_ALLOWED = 405;
int SC_NOT_ACCEPTABLE = 406;
int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
int SC_REQUEST_TIMEOUT = 408;
int SC_CONFLICT = 409;
int SC_GONE = 410;
int SC_LENGTH_REQUIRED = 411;
int SC_PRECONDITION_FAILED = 412;
int SC_REQUEST_ENTITY_TOO_LARGE = 413;
int SC_REQUEST_URI_TOO_LONG = 414;
int SC_UNSUPPORTED_MEDIA_TYPE = 415;
int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
int SC_EXPECTATION_FAILED = 417;
int SC_INTERNAL_SERVER_ERROR = 500;
int SC_NOT_IMPLEMENTED = 501;
int SC_BAD_GATEWAY = 502;
int SC_SERVICE_UNAVAILABLE = 503;
int SC_GATEWAY_TIMEOUT = 504;
int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 2、常见应用

1、向浏览器输出消息（一直在讲，就不说了）

2、下载文件

1. 要获取下载文件的路径
2. 下载的文件名是啥
3. 设置想办法让浏览器能够支持下载我们需要的东西
4. 获取下载文件的输入流
5. 创建缓冲区
6. 获取OutputStream对象
7. 将FileOutputStream流写入buffer缓冲区
8. 使用OutputStream将缓冲区的数据输出到客户端！

文件下载：

```
package com.wyqian.Servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.FileInputStream;
import java.io.IOException;
import java.net.URLEncoder;

public class response extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //1. 要获取下载文件的路径
        String downpath = "D:\\java后端\\code\\JavaWeb\\javaweb-maven06\\response01\\src\\main\\resources\\万云.png";
    //2. 下载的文件名是啥--非常巧妙
        String filename = downpath.substring(downpath.lastIndexOf("\\") + 1);
    //3. 设置想办法让浏览器能够支持下载我们需要的东西
        resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(filename,"utf-8"));
    //4. 获取下载文件的输入流
        FileInputStream fIS = new FileInputStream(downpath);
    //5. 创建缓冲区
        byte[] buffer = new byte[1024];
    //6. 获取OutputStream对象
        ServletOutputStream oS = resp.getOutputStream();
    //7. 将FileOutputStream流写入buffer缓冲区
    //8. 使用OutputStream将缓冲区的数据输出到客户端！
        int len = 0;
        while((len = fIS.read(buffer)) != -1){
            oS.write(buffer,0,len);
        }
    //关闭流对象
        oS.close();
        fIS.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

#### 3、验证码功能

- 前端实现
- 后端实现，需要用到java的图片类，生成一个图片

```
package com.wyqian.Servlet;

import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

import static java.awt.image.BufferedImage.TYPE_INT_RGB;

public class ImageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //在内存中写入一张图片,宽度是80，高度是20
        BufferedImage bufferedImage = new BufferedImage(80, 20, TYPE_INT_RGB);

        //生成一只画笔
        Graphics2D g = (Graphics2D) bufferedImage.getGraphics();
        g.setColor(Color.white);

        g.fillRect(0,0,80,20);

        //给图片写数据
        g.setColor(Color.BLUE);
        g.setFont(new Font("Times New Roman",Font.BOLD,20));

        g.drawString(makeNum(),0,20);

        //网站存在缓存，不让浏览器缓存
        resp.setHeader("Cache-Control","no-store");
        resp.setHeader("Pragma","no-cache");
        resp.setDateHeader("Expires",-1);

        //设置浏览器每3秒刷新一次
        resp.setHeader("refresh", "3");

        //设置浏览器以图片的方式打开
        resp.setContentType("image/jpeg");

        //把图片写给浏览器
        ImageIO.write(bufferedImage,"jpeg",resp.getOutputStream());
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }

    //生成随机数的函数
    private String makeNum(){
        Random random = new Random();
        String num = random.nextInt(9999999) + "";
        StringBuffer sB = new StringBuffer();
        for(int j = 0; j < 7-num.length(); j++){
            sB.append("0");
        }
        String s = sB.toString();
        String res = s + num;
        return res;
    }
}
```

#### 4、重定向

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-24_193044.png)

一个web资源(B)收到客户端(A)请求之后，他会通知客户端(A)去访问另外一个web资源(C)，这个过程叫做重定向。

常见场景：

- 用户登录

```
void sendRedirect(String var1) throws IOException;
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    /*
        resp.setHeader("Location","/r/img");
        resp.setStatus(302);
         */
    resp.sendRedirect("/r/img");//实现重定向
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-24_194702.png)

面试题：请你聊聊重定向和转发的区别？

相同点：

- 页面都会实现跳转

不同点：

- 请求转发的时候，url不会变化
- 重定向的时候，url地址栏会变

![img](https://wyqian.top/2020/11/17/JavaWeb/JavaWeb/H:%5Chexoblog%5Cblog%5Csource_posts%5CJavaWeb%5C2020-11-23_214009.png)

**demo(重要)**

首先是index.jsp

```
<html>
<body>
<%--这里需要找到请求的路径，也就是项目路径--%>
<%--{pageContext.request.getContextPath()}代表当前项目--%>
<form action="${pageContext.request.getContextPath()}/login" method="get">
    用户名：<input type="text" name="username"> </br>
    密码：<input type="password" name="password"></br>
    <input type="submit">
</form>
</body>
</html>
```

然后RequestTest会对请求到的数据进行处理，这里简单地使用req对象的getParameter方法将提交的用户名和密码读取了出来，然后在tomcat控制台打印了出来，然后用了一个重定向，将当前页面跳转到一个叫做Success.jsp页面。

```
package com.wyqian.Servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class RequestTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("进入这个请求了");
        String username = req.getParameter("username");
        String pwd = req.getParameter("password");
        System.out.println(username + ":" + pwd);

        //这里跳转路径的问题要注意
        resp.sendRedirect("/r/Success.jsp");

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

Success.jsp

```
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2020/11/24
  Time: 20:27
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Success</title>
</head>
<body>
<h1>Success!</h1>
</body>
</html>
```

### 6.7、HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，Http请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有信息。

![image-20201124205605983](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/image-20201124205605983.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20201124205850.png)

#### 1、获取前端传递的参数

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20201124210345.png)

index.jsp

```
<html>
<body>
<%--这里需要找到请求的路径，也就是项目路径--%>
<%--{pageContext.request.getContextPath()}代表当前项目--%>
<form action="${pageContext.request.getContextPath()}/login" method="get">
    用户名：<input type="text" name="username"> </br>
    密码：<input type="password" name="password"></br>
    爱好：
        <input type="checkbox" name="hobbys" value="看电影">看电影
        <input type="checkbox" name="hobbys" value="代码">代码
        <input type="checkbox" name="hobbys" value="NBA">NBA
    <input type="submit">
</form>
</body>
</html>
```

LoginRequest.java

```
package com.wyqian.servlet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

public class LoginRequest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        String username = req.getParameter("username");
        String password = req.getParameter("password");

        String[] hobbys = req.getParameterValues("hobbys");

        System.out.println(Arrays.toString(hobbys));

        //请求转发---实现方式有两种，一种是Context，还有一种就是request
        //这里的/代表当前web应用，所以不需要再加/r(Tomcat中配置的)，这里与重定向不同，需要注意
		//RequestDispatcher rD = req.getRequestDispatcher("/success.jsp");
		//rD.forward(req,resp);
        req.getRequestDispatcher("/success.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

success.jsp

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>转发成功</h1>
</body>
</html>
```

面试题：请你聊聊重定向和转发的区别？

相同点：

- 页面都会实现跳转

不同点：

- 请求转发的时候，url不会变化 307
- 重定向的时候，url地址栏会变化 302

## 7、Cookie、Session

### 7.1、会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话。

**有状态会话**：一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

**你能怎么证明你是南大的学生？**

你 南大

1. 发票 南大给你发票
2. 学校登记 南大标记你来过了

**一个网站，你怎么证明你来过？**

客户端 服务端

1. 服务端给客户端一个信件，客户端下次访问服务端带上信件就可以了；cookie
2. 服务器登记你来过了，下次你来的时候我来匹配你；Session

### 7.2、保存会话的两种技术

**cookie**

- 客户端技术（响应、请求）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息。我们可以把信息或者数据放在Session中。

常见场景： 网站登录之后，你下次不用登录了，第二次访问直接就上去了！

### 7.3、Cookie

1、从请求中拿到cookie信息

2、服务器响应给客户端cookie

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-26_223244.png)

```
Cookie[] cookies = req.getCookies();//获得cookie
cookie.getName();//获得cookie中的key
cookie.getValue();//获得cookie中的value
new Cookie("lastLoginTime", System.currentTimeMillis()+"");//新建一个cookie
cookie.setMaxAge(24*60*60);//设置cookie的有效期
resp.addCookie(cookie);//响应给客户端一个cookie
package com.wyqian.cookie;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

public class cookieDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置请求和响应的编码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        PrintWriter out = resp.getWriter();
        //服务器获取cookie
        Cookie[] cookies = req.getCookies();
        if(cookies != null){
            for (int i = 0; i < cookies.length; i++) {
                Cookie cookie = cookies[i];
                if(cookie.getName().equals("lastLoginTime")){
                    long lastLoginTime = Long.parseLong(cookie.getValue());
                    out.write("您上次访问本站时间是：" + new Date(lastLoginTime).toLocaleString());
                }
            }
        }else{
            out.write("这是您第一次访问本站！");
        }
        //服务器响应cookie
        Cookie cookie = new Cookie("lastLoginTime",System.currentTimeMillis()+"");
        cookie.setMaxAge(24*60*60);//设置cookie有效时间
        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req,resp);
    }
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-25_210514.png)

![img](https://wyqian.top/2020/11/17/JavaWeb/JavaWeb/H:%5Chexoblog%5Cblog%5Csource_posts%5CJavaWeb%5C2020-11-25_210443.png)

**cookie：一般会保存在本地的用户目录下appdata;**

一个网站cookie是否存在上限，**聊聊细节问题**

- 一个cookie只能保存一个信息
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- Cookie大小有限制4kb；
- 300个cookie浏览器上限

**删除Cookie：**

- 不设置有限期，关闭浏览器，自动失效；
- 设置有效期时间为0；

```
Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis() + "");
cookie.setMaxAge(0);//设置cookie有效期是0
resp.addCookie(cookie);
```

网络编程中编码解码：

```
URLEncoder.encode("钱万云", "utf-8");
URLDecoder.decode(cookie.getValue(),"UTF-8");
```

### 7.4、Session（重点）

什么是Session:

- 服务器会给每一个用户（浏览器）创建一个Session对象；
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登陆之后，整个网站它都可以访问！–>保存用户信息；保存购物车信息……

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-26_223339.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-26_212328.png)

```
package com.wyqian.session;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class sessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();

        //在Session中存东西
        session.setAttribute("name","钱万云");

        //获得Session的id
        String sessionId = session.getId();

        //判断session是不是新创建
        if(session.isNew()){
            resp.getWriter().write("Session创建成功，id为：" + sessionId);
        }else{
            resp.getWriter().write("Session已经在服务器中存在，id为：" + sessionId);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
package com.wyqian.session;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class sessionDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();

        //获取key为name的值
        String value = (String) session.getAttribute("name");

        resp.getWriter().write(value);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

**session中存的东西可以是一个对象**

```
package com.wyqian.session;

import com.wyqian.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class sessionDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();

        //获取key为name的值
        Person person =  (Person)session.getAttribute("name");

        resp.getWriter().write("人名：" + person.getName());
        resp.getWriter().write("年龄：" + person.getAge());

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
package com.wyqian.session;

import com.wyqian.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class sessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();

        //在Session中存东西
        session.setAttribute("name",new Person("钱万云", 22));

        //获得Session的id
        String sessionId = session.getId();

        //判断session是不是新创建
        if(session.isNew()){
            resp.getWriter().write("Session创建成功，id为：" + sessionId);
        }else{
            resp.getWriter().write("Session已经在服务器中存在，id为：" + sessionId);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
package com.wyqian.pojo;

import java.util.PriorityQueue;

public class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

注销session

```
package com.wyqian.session;

import com.wyqian.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class sessionDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //得到Session
        HttpSession session = req.getSession();

        session.removeAttribute("name");//删除属性
        session.invalidate();//注销

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

也可以在xml中设置注销session:

```
<session-config>
    <!--设置session有效时间是15分钟，15分钟自动失效-->
    <session-timeout>15</session-timeout>
</session-config>
```

Session和cookie区别：

- Cookie是把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）；
- Session把用户的数据写到用户独占Session中，服务端保存（保存重要的信息，减少服务器资源的浪费）；
- Session对象由服务端创建；

使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们将它保存在Session中；

## 8、JSP

### 8.1、什么是JSP

Java Server Pages：java服务器端页面，也和Servlet一样，用于动态web技术；

最大的特点：

- 写JSP就像在写HTML
- 区别：
  - HTML只给用户提供静态的数据
  - JSP页面中可以嵌入JAVA代码，为用户提供动态数据；

### 8.2、JSP原理

思路：JSP怎么执行的

- 代码层面没有问题，启动Tomcat后，项目目录下的jsp文件对应到target目录下还是jsp文件
- 服务器内部工作
  - Tomcat中有一个work目录；
  - IDEA中使用Tomcat的话会在IDEA的tomcat中生成一个work目录

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-27_133251.png)

我电脑的地址：

```
C:\Users\Administrator\AppData\Local\JetBrains\IntelliJIdea2020.2\tomcat\Unnamed_javaweb-session\work\Catalina\localhost\ROOT\org\apache\jsp
```

发现页面转变成了java程序！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-27_133511.png)

**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

JSP最终也会被转换成为一个Java类！

**JSP本质上就是一个Servlet**

```
//初始化
public final void init(ServletConfig config) throws ServletException {
    
}

//销毁
public final void destroy() {
   
}

//JSP Service
public final void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
   
}
```

1、判断请求

2、内置一些对象

```
final javax.servlet.jsp.PageContext pageContext;//页面上下文
javax.servlet.http.HttpSession session = null;//session
final javax.servlet.ServletContext application;//applicationContext
final javax.servlet.ServletConfig config;//config
javax.servlet.jsp.JspWriter out = null;//out
final java.lang.Object page = this;//page：当前
HttpServletRequest request;//请求
HttpServletResponse response;//响应
```

3、输出页面前增加的代码

```
response.setContentType("text/html");//设置响应的页面类型
pageContext = _jspxFactory.getPageContext(this, request, response,
                                          null, true, 8192, true);
_jspx_page_context = pageContext;
application = pageContext.getServletContext();
config = pageContext.getServletConfig();
session = pageContext.getSession();
out = pageContext.getOut();
_jspx_out = out;
```

4、以上的这些个对象我们可以在JSP页面中直接使用！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-27_145358.png)

在JSP页面中：

只要是JAVA代码就会原封不动地输出；

如果是HTML代码，就会被转换为：

```
out.write("<html>\r\n");
```

这样的格式输出到前端。

比如说：这样的一个jsp文件：（helloNJU.jsp文件）

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-27_151928.png)

就会被转换成：（helloNJU_jsp.java文件）

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-27_151945.png)

### 8.3、JSP基础语法

任何语言都有自己的语法，JAVA中有，JSP作为java技术的一种应用，它拥有一些自己扩充的语法（了解，知道即可！），JAVA所有语法都支持！

**JSP表达式**

```
<%--jsp表达式：
用来将程序的输出，输出到客户端
<%= 变量或者表达式%>
--%>
<%= new java.util.Date()%>
```

**JSP脚本片段**

```
<%--jsp脚本片段--%>
<%
    int sum = 0;
    for (int i = 0; i <= 100; i++) {
        sum += i;
    }
    out.println("<h1>sum=" + sum + "</h1>");
%>
```

**脚本片段再实现**

```
<%--脚本片段再实现--%>
<%
    int x = 10;
    out.println(x);
%>
<p>这是一个JSP文档</p>
<%
    int y = 10;
    out.println(y);
%>

<hr>
<%--在代码中嵌入HTML元素--%>
<%
    for (int i = 0; i < 5; i++) {

%>
    <p>Hello,NJU! <%=i%></p>
<%
    }
%>
```

**JSP声明**

```
<%--JSP声明--%>
<%!
    static{
        System.out.println("Loading Servlet");
    }
    private int globalVar = 0;
    public void wyqian(){
        System.out.println("进入了wyqian方法中！");
    }
%>
```

JSP声明：会被编译到JSP生成Java的类中！其他的（JSP表达式和JSP片段）就会被生成到_jspService方法中！

在JSP，嵌入Java代码即可！

```
<%%>jsp脚本片段
<%=%>jsp表达式
<%!%>jsp声明
<%----%>注释
```

JSP的注释，不会在客户端显示，HTML就会！

### 8.4、JSP指令

```
<%@ page args.... %>
<%--@include会将两个页面合二为一--%>
<%@include file="common/header.jsp"%>
<h1>网站主体</h1>
<%@include file="common/footer.jsp"%>

<hr>
<%--jsp标签
    jsp:include：拼接页面，本质上还是3个
--%>
<jsp:include page="/common/header.jsp"></jsp:include>
<h1>网站主体</h1>
<jsp:include page="/common/header.jsp"></jsp:include>
```

demo：定制错误页面

首先是人为制造一个错误：

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%--定制错误页面--%>
<%--<%@ page errorPage="/error/500.jsp" %>--%>
<html>
<head>
    <title>jsp2</title>
</head>
<body>
<%
    //    这里一定会报错
    int x = 1 / 0;
%>
</body>
</html>
```

这里会报500错误，于是乎，我们有两种方式，第一种在该页面中使用errorPage:

```
<%@ page errorPage="/error/500.jsp" %>
```

第二种方式就是在web.xml中配置：

```
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <error-page>
        <error-code>500</error-code>
        <location>/error/500.jsp</location>
    </error-page>
    <error-page>
        <error-code>404</error-code>
        <location>/error/404.jsp</location>
    </error-page>
</web-app>
```

500.jsp代码：

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>500错误页面</title>
</head>
<body>
    <img src="/img/500.jpg" alt="500" width="1000px" height="700px">
</body>
</html>
```

404.jsp代码：

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>404错误页面</title>
</head>
<body>
    <img src="/img/404.jpg" alt="404错误页面" >
</body>
</html>
```

值得一提的是，我在坐上面的demo时，404页面显示的一开始是404错误页面几个字，图片并没有显示出来，经过解决：直接在target文件夹中，手动将404.jpg给粘贴进去。

### 8.5、九大内置对象

- PageContext 存东西
- Request 存东西
- Response
- Session 存东西
- Application 【ServletContext】 存东西
- config 【ServletConfig】
- out
- page 几乎不用
- exception

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>pageContextDemo01</title>
</head>
<body>
<%--内置对象--%>
<%
    pageContext.setAttribute("name1","wyqian1");//保存的数据只在一个页面中有效
    request.setAttribute("name2","wyqian2");//保存的数据只在一次请求中有效，请求转发会携带这个数据
    session.setAttribute("name3","wyqian3");//保存的数据只在一次会话有效，从打开浏览器到关闭浏览器
    application.setAttribute("name4","wyqian4");//保存的数据只在服务器有效，从打开服务器到关闭服务器
%>

<%--脚本片段中的代码，会被原封不动被转换成*_jsp.java
要求：这里面的代码：必须保证java语法的正确性
--%>
<%
    //从pageContext中取出，我们通过寻找的方式来
    //从底层到高层（作用域）:page-->request-->session-->application
    String name1 = (String) pageContext.findAttribute("name1");
    String name2 = (String) pageContext.findAttribute("name2");
    String name3 = (String) pageContext.findAttribute("name3");
    String name4 = (String) pageContext.findAttribute("name4");
    String name5 = (String) pageContext.findAttribute("name5");//不存在
%>
<h1>寻找的结果为：</h1>
<%--使用EL表达式输出--%>
<h3>${name1}</h3>
<h3>${name2}</h3>
<h3>${name3}</h3>
<h3>${name4}</h3>
<%--使用${name5}就是什么都没输出--%>
<h3>${name5}</h3>
<%--使用<%=name5%>就是输出null--%>
<%=name5%>
</body>
</html>
```

request：客户端向服务器发送请求，产生的数据，用户看完了就没用了，比如：新闻，用户看完没用的！

session：客户端向服务器发送请求，产生的数据，用户用完一会还有用，比如：购物车；

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据；

### 8.6、JSP标签、JSTL标签、EL表达式

maven依赖

```
<!--JSTL表达式的依赖-->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>
<!--standard标签库的依赖-->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

EL表达式：${ }

- **获取数据**
- **执行运算**
- **获取web开发的常用对象**
- 调用Java方法

> jsp标签

```
<%--<jsp:include page="jspTag2.jsp"></jsp:include>--%>

<%--跳转，可以携带参数--%>
<%--https://localhost:8080/jspTag?name=wyqian&age=22--%>
<%
    request.setCharacterEncoding("utf-8");
    response.setCharacterEncoding("utf-8");
%>
<jsp:forward page="jspTag2.jsp">
    <jsp:param name="name" value="钱万云"/>
    <jsp:param name="age" value="22"/>
</jsp:forward>
```

> JSTL表达式

JSTL标签库的使用就是为了弥补HTML标签的不足，它自定义了许多标签，可以供我们使用，标签的功能和Java代码一样！

**格式化标签**

**SQL标签**

**XML标签**

**核心标签**（掌握部分）

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-29_103028.png)

**JSTL标签库使用步骤**

- 引入对应的taglib
- 使用其中的方法
- 在Tomcat中也需要引入jstl的包，否则会报错，jstl解析错误

***c:if\***

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<html>
<head>
    <title>jstl核心标签库的学习</title>
</head>
<body>

<h2>jstl核心标签库的学习</h2>
<hr/>
<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单的数据
    ${param.参数名}
    --%>
    用户名：<input type="text" name="username" value="${param.username}">
    <input type="submit" value="提交">
</form>

<%--判断如果登录的用户名是管理员，就显示登陆成功--%>
<c:if test="${param.username == 'admin'}" var="isAdmin">
    <c:out value="欢迎您管理员！"/>
</c:if>

<c:out value="${isAdmin}"/>

</body>
</html>
```

***c:choose c:when\***

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2020/11/29
  Time: 11:07
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>coreWhen</title>
</head>
<body>

<%--保存数据，类似javascript中设置变量--%>
<c:set var="score" value="85"></c:set>

<c:choose>
    <c:when test="${score>=90}">
        <c:out value="优秀"/>
    </c:when>
    <c:when test="${score>=80}">
        <c:out value="良好"/>
    </c:when>
    <c:when test="${score>=70}">
        <c:out value="一般"/>
    </c:when>
    <c:when test="${score>=60}">
        <c:out value="不及格"/>
    </c:when>
</c:choose>
</body>
</html>
```

***c:foreach\***

```
<%@ page import="java.util.ArrayList" %>
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2020/11/29
  Time: 12:20
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>coreForeach</title>
</head>
<body>

<%
    ArrayList<String> people = new ArrayList<String>();
    people.add(0, "张三");
    people.add(1, "李四");
    people.add(2, "王五");
    people.add(3, "赵六");
    people.add(4, "田七");
    people.add(5, "黑八");
    request.setAttribute("list",people);
%>

<%--
使用jstl标签库的foreach进行遍历
var:每一次遍历的变量
items:要遍历的对象
begin: 从哪里开始
end: 到哪里
step:步长
--%>

<c:forEach var="person" items="${list}">
    <c:out value="${person}"/></br>
</c:forEach>

<hr/>
<c:forEach var="person" items="${list}" begin="1" end="3" step="2">
    <c:out value="${person}"/></br>
</c:forEach>

</body>
</html>
```

## 9、JavaBean

实体类

JavaBean有特点的写法：

- 必须要有无参构造
- 属性必须私有化
- 必须有对应的get/set方法；

一般用来和数据库的字段做映射 ORM；

ORM：对象关系映射

- 表—>类
- 字段—>属性
- 行记录—>对象

people表

| id   | name   | age  | address |
| ---- | ------ | ---- | ------- |
| 1    | wyqian | 22   | 南京    |
| 2    | yq     | 21   | 南昌    |
| 3    | ysh    | 21   | 成都    |

```
class People{
    private int id;
    private String name;
    private int age;
    private int address;
}

class A{
    new People(1, "wyqian", 22, "南京");
    new People(2, "yq", 21, "南昌");
    new People(3, "ysh", 21, "成都");
}
<%@ page import="com.wyqian.pojo.People" %>
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2020/11/29
  Time: 13:15
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>javaBean</title>
</head>
<body>

<%--使用熟悉的java代码来写--%>
<%
//    People people = new People();
//    people.setId(1);
//    people.setName("wyqian");
//    people.setAge(22);
//    people.setAddress("南京");
%>

<%--使用javaBean来写--%>
<jsp:useBean id="people" class="com.wyqian.pojo.People" scope="page"></jsp:useBean>

<jsp:setProperty name="people" property="id" value="1"></jsp:setProperty>
<jsp:setProperty name="people" property="name" value="wyqian"></jsp:setProperty>
<jsp:setProperty name="people" property="age" value="22"></jsp:setProperty>
<jsp:setProperty name="people" property="address" value="南京"></jsp:setProperty>

ID：<jsp:getProperty name="people" property="id"/>
姓名：<jsp:getProperty name="people" property="name"/>
年龄：<jsp:getProperty name="people" property="age"/>
地址：<jsp:getProperty name="people" property="address"/>

</body>
</html>
```

## 10、MVC三层架构

什么是MVC：Model view Controller 模型、视图、控制器

### 10.1、早些年

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-29_194443.png)

用户直接访问控制层，控制层可以直接操作数据库；

```
servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码
    
架构：没有什么是加一层解决不了的！
程序员    
|    
JDBC
|    
Mysql   Oracle     SqlServer......
```

### 10.2、MVC三层架构

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-29_195650.png)

Model

- 业务处理：业务逻辑（Service）
- 数据持久层：CRUD（Dao）

View

- 展示数据
- 提供链接发起Servlet请求（a、form、img……）

Controller（Servlet）

- 接收用户的请求：（req：请求参数、Session信息）
- 交给业务层处理对应的代码
- 控制视图的跳转

```
登录--->接收用户的登录请求--->处理用户的请求（获取用户登录的参数，username,password）--->交给业务层处理登陆业务（判断用户名和密码是否正确：事务）--->Dao层查询用户名和密码是否正确--->数据库
```

## 11、Filter

Filter：过滤器，用来过滤网站的数据；

- 处理中文乱码
- 登录验证…

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-11-29_201555.png)

Filter开发步骤：

1. 导包

2. 编写过滤器

   1. 导包不要错

   2. ```
      package com.wyqian.filter;
      
      import javax.servlet.*;
      import java.io.IOException;
      
      public class CharacterEncodingFilter implements Filter {
          //初始化：web服务器启动的时候就执行了，随时等待过滤对象出现
          public void init(FilterConfig filterConfig) throws ServletException {
              System.out.println("CharacterEncodingFilter初始化");
          }
      
          //chain：链
          /*
          1.过滤中的所有代码，都会在过滤特定请求时被执行
          2.必须要让过滤器继续同行：filterChain.doFilter(servletRequest, servletResponse);
           */
          public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
              servletRequest.setCharacterEncoding("utf-8");
              servletResponse.setCharacterEncoding("utf-8");
              servletResponse.setContentType("text/html;charset=utf-8");
      
              System.out.println("doFilter执行前...");
              filterChain.doFilter(servletRequest, servletResponse);//为了放行，不然程序到这儿就停住了
              System.out.println("doFilter执行后...");
          }
      
          //销毁：web服务器关闭的时候，过滤会销毁
          public void destroy() {
              System.out.println("CharacterEncodingFilter销毁");
          }
      }
      
      <!--￼86-->
      ```

## 12、监听器

实现一个监听器的接口，有很多种

步骤：

1. 实现监听器接口

   ```
   package com.wyqian.listener;
   
   import javax.servlet.ServletContext;
   import javax.servlet.http.HttpSessionEvent;
   import javax.servlet.http.HttpSessionListener;
   
   //统计网站在线人数：统计session
   public class onlineCountListener implements HttpSessionListener {
       //创建session监听
       //一旦创建session，就会触发一次这个事件
       @Override
       public void sessionCreated(HttpSessionEvent httpSessionEvent) {
           ServletContext sC = httpSessionEvent.getSession().getServletContext();
           Integer onlineCount = (Integer) sC.getAttribute("onlineCount");
   
           System.out.println(httpSessionEvent.getSession().getId());
           if(onlineCount == null){
               onlineCount = new Integer(1);
           }else{
               int count = onlineCount.intValue();
               onlineCount = new Integer(count + 1);
           }
   
           sC.setAttribute("onlineCount", onlineCount);
       }
   
       //销毁session监听
       //一旦销毁session，就会触发一次这个事件
       @Override
       public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
           ServletContext sC = httpSessionEvent.getSession().getServletContext();
           Integer onlineCount = (Integer) sC.getAttribute("onlineCount");
   
           if(onlineCount == null){
               onlineCount = new Integer(0);
           }else{
               int count = onlineCount.intValue();
               onlineCount = new Integer(count - 1);
           }
   
           sC.setAttribute("onlineCount", onlineCount);
       }
   }
   ```

2. 配置监听器

```
<!--配置监听器-->
<listener>
    <listener-class>com.wyqian.listener.onlineCountListener</listener-class>
</listener>
```

第一次启动的时候，由于Tomcat的原因，会显示3人在线，打印出***sessionId\***可以看到有三个Id，但是前两个会被销毁，重新发布项目（redeploy）之后就会变成在线人数1人。

 3. 看情况是否使用

## 13、过滤器、监听器常见应用

监听器：GUI编程中经常使用

```
package com.wyqian.listener;

import java.awt.*;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;

public class panel {
    public static void main(String[] args) {
        Frame frame = new Frame("金州勇士新赛季加油丫");//创建窗口
        Panel panel = new Panel();//创建面板
        frame.setLayout(null);//设置窗体布局

        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255));

        panel.setBounds(30,80,300,300);
        panel.setBackground(new Color(0,255,0));

        frame.add(panel);//把面板加到窗口
        frame.setVisible(true);//使窗口保持可见
        //当然也可以实现WindowListener的子类，这样的话可以选择实现哪个方法，不用去重写所有方法
        frame.addWindowListener(new WindowListener() {
            @Override
            public void windowOpened(WindowEvent e) {
                System.out.println("正在打开...");
            }

            @Override
            public void windowClosing(WindowEvent e) {
                System.out.println("正在关闭...");
                System.exit(1);
            }

            @Override
            public void windowClosed(WindowEvent e) {
                System.out.println("已经关闭");
            }

            @Override
            public void windowIconified(WindowEvent e) {

            }

            @Override
            public void windowDeiconified(WindowEvent e) {

            }

            @Override
            public void windowActivated(WindowEvent e) {
                System.out.println("激活");
            }

            @Override
            public void windowDeactivated(WindowEvent e) {
                System.out.println("未激活");
            }
        });
    }
}
```

用户登录之后才能进入主页！用户注销后就不能进入主页！

1、用户登陆之后，向Session中放入用户的数据

2、进入主页的时候要判断用户是否已经登录；要求：在过滤器中实现

```
@Override
public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

    HttpServletRequest req = (HttpServletRequest) servletRequest;
    HttpServletResponse resp = (HttpServletResponse) servletResponse;

    if(req.getSession().getAttribute(Content.USER_SESSION) == null){
        resp.sendRedirect("/error/error.jsp");
    }

    filterChain.doFilter(servletRequest, servletResponse);
}
```

## 14、JDBC

什么是JDBC：Java连接数据库！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-12_214818.png)

需要jar包的支持：

- java.sql
- javax.sql
- mysql-connector-java…连接驱动（必须要导入）

实验环境搭建：

```
CREATE TABLE `users`(
  `id` INT PRIMARY KEY,
  `name` VARCHAR(40),
  `password` VARCHAR(40),
  `email` VARCHAR(40),
  `birthday` DATE
);

INSERT INTO `users`(`id`, `name`, `password`, `email`, `birthday`)
VALUES(1, '张三', '123', 'zs@qq.com', '2020-01-01'),
(2, '李四', '234', 'ls@qq.com', '2020-01-02'),
(3, '王五', '345', 'ww@qq.com', '2020-01-03')
```

导入数据库依赖

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```

IDEA连接数据库

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-14_200829.png)

JDBC固定步骤：

1. 加载驱动
2. 连接数据库，代表数据库
3. 向数据库发送SQL的对象Statement：CRUD
4. 编写SQL（根据业务不同，SQL语句会不同）
5. 执行SQL
6. 关闭连接

```
package com.wyqian.test;

import java.sql.*;

public class TestJdbc {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //加载驱动
        Class.forName("com.mysql.jdbc.Driver");

        //配置信息
        //useUnicode=true&characterEncoding=utf-8解决中文乱码问题
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        //连接数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //执行SQl的对象
        Statement statement = connection.createStatement();

        ResultSet rs = statement.executeQuery("select * from users;");

        while(rs.next()){
            System.out.println("id=" + rs.getString("id"));
            System.out.println("姓名=" + rs.getString("name"));
            
            
            System.out.println("密码=" + rs.getString("password"));
            System.out.println("电子邮箱=" + rs.getString("email"));
            System.out.println("生日=" + rs.getString("birthday"));
        }

        //关闭资源
        rs.close();
        statement.close();
        connection.close();

    }
}
```

预编译SQL

```
package com.wyqian.test;

import java.sql.*;

public class TestJdbc02 {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //1. 加载驱动
        Class.forName("com.mysql.jdbc.Driver");

        //配置信息
        String url = "jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String pwd = "123456";

        //连接数据库
        Connection connection = DriverManager.getConnection(url, username, pwd);

        //编写SQL
        String sql = "insert into users (id, name, password, email, birthday) values(?,?,?,?,?)";

        //预编译
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        //给占位符赋值
        preparedStatement.setInt(1,4);
        preparedStatement.setString(2,"斯蒂芬库里");
        preparedStatement.setString(3,"30");
        preparedStatement.setString(4,"curry@qq.com");
        preparedStatement.setDate(5,new Date(System.currentTimeMillis()));

        //执行SqL
        int i = preparedStatement.executeUpdate();

        if(i > 0){
            System.out.println("插入成功！");
        }

        //关闭资源
        preparedStatement.close();
        connection.close();

    }
}
```

**事务**

要么都成功，要么都失败！

ACID原则：保证数据的安全。

```
开启事务
事务提交  commit()
事务回滚  rollback()
关闭事务

转账：
A:1000
B:1000
    
A(900)   --100-->   B(1100)
```

**Junit单元测试**

依赖

```
<!--单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

简单使用

@Test注解只有在方法上有效，只要加了这个注解的方法，就可以直接运行！

```
@Test
public void test(){
    System.out.println("Hello");
}
```

![1568442261610](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/1568442289597.png)

失败的时候是红色：

![1568442289597](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/1568442289597.png)

**搭建一个环境**

```
CREATE TABLE account(
   id INT PRIMARY KEY AUTO_INCREMENT,
   `name` VARCHAR(40),
   money FLOAT
);

INSERT INTO account(`name`,money) VALUES('A',1000);
INSERT INTO account(`name`,money) VALUES('B',1000);
INSERT INTO account(`name`,money) VALUES('C',1000);
@Test
public void test() {
    //配置信息
    //useUnicode=true&characterEncoding=utf-8 解决中文乱码
    String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
    String username = "root";
    String password = "123456";

    Connection connection = null;

    //1.加载驱动
    try {
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
         connection = DriverManager.getConnection(url, username, password);

        //3.通知数据库开启事务,false 开启
        connection.setAutoCommit(false);

        String sql = "update account set money = money-100 where name = 'A'";
        connection.prepareStatement(sql).executeUpdate();

        //制造错误
        //int i = 1/0;

        String sql2 = "update account set money = money+100 where name = 'B'";
        connection.prepareStatement(sql2).executeUpdate();

        connection.commit();//以上两条SQL都执行成功了，就提交事务！
        System.out.println("success");
    } catch (Exception e) {
        try {
            //如果出现异常，就通知数据库回滚事务
            connection.rollback();
        } catch (SQLException e1) {
            e1.printStackTrace();
        }
        e.printStackTrace();
    }finally {
        try {
            connection.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```