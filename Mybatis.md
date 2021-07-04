# MyBatis

## Mybatis-9.28



环境：

- JDK1.8
- Mysql 5.7
- Maven 3.6.1
- IDEA

回顾：

- JDBC
- Mysql
- Java基础
- Maven
- Junit

SSM框架：配置文件的。最好方式：看官网文档：https://mybatis.org/mybatis-3/zh/index.html

## 1、简介

### 1.1、什么是Mybatis

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/mybatis-logo.png)

- MyBatis 是一款优秀的**持久层框架**
- 它支持自定义 SQL、存储过程以及高级映射。
- MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
- MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
- MyBatis 本是apache的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。
- 2013年11月迁移到Github。

如何获得Mybatis?

- maven仓库：

  ```
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
  <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.6</version>
  </dependency>
  ```

- Github：https://github.com/mybatis/mybatis-3/releases

- 中文文档：https://mybatis.org/mybatis-3/zh/index.html

### 1.2、持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库（Jdbc）,io文件持久化。
- 生活：冷藏，罐头。

**为什么需要持久化？**

- 有一些对象，不能让他丢掉。
- 内存太贵了

### 1.3、持久层

Dao层、Service层、Cotroller层…

- 完成持久化工作的代码块
- 层界限十分明显。

### 1.4、为什么需要Mybatis?

- 帮助程序员将数据存入到数据库中。
- 方便
- 传统的JDBC代码太复杂了。简化。框架。自动化。
- 不用Mybatis也可以。更容易上手。**技术没有高低之分**
- 优点
  - 简单易学
  - 灵活
  - sql和代码的分离，提高了可维护性。
  - 提供映射标签，支持对象与数据库的orm字段关系映射
  - 提供对象关系映射标签，支持对象关系组建维护
  - 提供xml标签，支持编写动态sql。

**最重要的一点：使用的人多！**

Spring SpringMVC SpringBoot

## 2、第一个Mybatis程序

思路：搭建环境–>导入Mybatis–>编写代码–>测试！

### 2.1、搭建环境

搭建数据库

```
CREATE DATABASE `mybatis`;

USE `mybatis`;

CREATE TABLE `user`(
   `id` INT(20) NOT NULL PRIMARY KEY,
   `name` VARCHAR(20) DEFAULT NULL,
   `pwd` VARCHAR(20) DEFAULT NULL
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `user`(`id`,`name`,`pwd`) VALUES
(1, '小钱', '123'),
(2, '小王', '456'),
(3, '小陈', '789')
```

新建项目

1. 新建一个普通的maven项目

2. 删除src目录

3. 导入maven依赖

   ```
   <!--导入依赖-->
   <dependencies>
       <!--mysql驱动-->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.47</version>
       </dependency>
       <!--Mybatis-->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.6</version>
       </dependency>
       <!--junit-->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
   </dependencies>
   ```

### 2.2、创建一个模块

- 编写mybatis的核心配置文件

  ```
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <!--configuration核心配置文件-->
  <configuration>
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="123456"/>
              </dataSource>
          </environment>
      </environments>
  </configuration>
  ```

- 编写mybatis工具类

```
package com.wyqian.utils;


import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

//SqlSessionFactory --->  sqlSession
public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static{

        try {
            //使用Mybatis第一步：获取SqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream =  Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    //SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}
```

### 2.3、编写代码

- 实体类

  ```
  package com.wyqian.pojo;
  
  //实体类
  public class User {
      private int id;
      private String name;
      private String pwd;
  
      public User() {
      }
  
      public User(int id, String name, String pwd) {
          this.id = id;
          this.name = name;
          this.pwd = pwd;
      }
  
      public int getId() {
          return id;
      }
  
      public void setId(int id) {
          this.id = id;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public String getPwd() {
          return pwd;
      }
  
      public void setPwd(String pwd) {
          this.pwd = pwd;
      }
  
      @Override
      public String toString() {
          return "User{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  ", pwd='" + pwd + '\'' +
                  '}';
      }
  }
  ```

- Dao接口

  ```
  public interface UserDao {
      List<User> getUserList();
  }
  ```

- 接口实现类(由原来的UserDaoImpl转变为一个Mapper.xml配置文件)

  ```
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!--namespace绑定一个对应的Dao/Mapper接口-->
  <mapper namespace="com.wyqian.dao.UserDao">
  
      <!--sql查询语句-->
      <select id="getUserList" resultType="com.wyqian.pojo.User">
          select * from mybatis.user
      </select>
  </mapper>
  ```

### 2.4、测试

- junit测试

```
package com.wyqain.dao;

import com.wyqian.dao.UserDao;
import com.wyqian.pojo.User;
import com.wyqian.utils.MybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

public class UserDaoTest {

    @Test
    public void test(){
        //获取sqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        //方式一：getMapper---推荐使用
        UserDao mapper = sqlSession.getMapper(UserDao.class);
        List<User> userList = mapper.getUserList();

        //方式二：---不推荐使用
//        List<User> userList = sqlSession.selectList("com.wyqian.dao.UserDao.getUserList");

        //打印出来
        for (User user : userList) {
            System.out.println(user);
        }

        //关闭资源
        sqlSession.close();

    }
}
```

注册mapper:

```
<!--每一个Mapper.xml都要在mybatis-config.xml文件中注册-->
<mappers>
    <mapper resource="com/wyqian/dao/UserMapper.xml"></mapper>
</mappers>
```

为了保证maven项目不出现资源导出的问题，通常我们会在父子工程的pom.xml文件中加上下面这段代码：

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
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

你们可能遇到的问题：

1. 配置文件没有注册
2. 绑定接口错误
3. 方法名不对
4. 返回类型不对
5. Maven导出资源问题

## 3、CRUD

### 1、namespace

namespace的包名要和Dao/Mapper接口的包名一致！

### 2、select

选择，查询语句；

- id：就是对应的namespace中的方法名；
- resultType：Sql语句的返回值！
- parameterType：参数类型

> 查询全部用户

1. 编写接口

   ```
   //查询全部用户
   List<User> getUserList();
   ```

2. 编写对应的mapper中的sql语句

   ```
   <!--sql查询语句-->
   <select id="getUserList" resultType="com.wyqian.pojo.User">
       select * from mybatis.user
   </select>
   ```

3. 编写测试代码

   ```
   //查询所有用户
   @Test
   public void test(){
       //获取sqlSession对象
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       //方式一：getMapper---推荐使用
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       List<User> userList = mapper.getUserList();
   
       //方式二：
       //        List<User> userList = sqlSession.selectList("com.wyqian.dao.UserDao.getUserList");
   
       //打印出来
       for (User user : userList) {
           System.out.println(user);
       }
   
       //关闭资源
       sqlSession.close();
   
   }
   ```

> 根据用户id查询用户

1. 编写接口

   ```
   //根据id查询用户
   User getUserById(int id);
   ```

2. 编写mapper中对应的sql语句

   ```
   <select id="getUserById" resultType="com.wyqian.pojo.User" parameterType="int">
       select * from mybatis.user where id = #{id}
   </select>
   ```

3. 编写测试代码

   ```
   //根据用户Id查询用户
   @Test
   public void getUserById(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       User user = mapper.getUserById(1);
   
       System.out.println(user);
   
       sqlSession.close();
   }
   ```

### 3、Insert

1. 编写接口

   ```
   //插入一个用户
   int addUser(User user);
   ```

2. 编写对应的mapper中的sql语句

   ```
   <!--插入用户-->
   <insert id="addUser" parameterType="com.wyqian.pojo.User" >
       insert into mybatis.user (id, name, pwd) values(#{id}, #{name}, #{pwd})
   </insert>
   ```

3. 编写测试代码

   ```
   //添加一个用户
   @Test
   public void addUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       mapper.addUser(new User(4, "斯蒂芬库里", "345"));
   
       //不要忘了提交事务
       sqlSession.commit();
       sqlSession.close();
   }
   ```

### 4、update

1. 编写接口

   ```
   //更新用户信息
   int updateUser(User user);
   ```

2. 编写对应的mapper中的sql语句

   ```
   <!--更新用户信息-->
   <update id="updateUser" parameterType="com.wyqian.pojo.User">
       update mybatis.user set name = #{name}, pwd = #{pwd} where id = #{id}
   </update>
   ```

3. 编写测试代码

   ```
   //更新用户信息
   @Test
   public void updateUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       mapper.updateUser(new User(4, "哈登", "123456"));
   
       //不要忘了提交事务
       sqlSession.commit();
       sqlSession.close();
   }
   ```

### 5、delete

1. 编写接口

   ```
   //删除用户
   int deleteUser(int id);
   ```

2. 编写对应的mapper中的sql语句

   ```
   <!--删除一个用户-->
   <delete id="deleteUser" parameterType="int">
       delete from mybatis.user where id = #{id}
   </delete>
   ```

3. 编写测试代码

   ```
   //删除一个用户
   @Test
   public void deleteUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       mapper.deleteUser(4);
   
       //不要忘了提交事务
       sqlSession.commit();
       sqlSession.close();
   }
   ```

注意点：

- ***增删改需要提交事务！！！\***

### 6、分析错误

- 标签不要匹配错
- resource绑定mapper，需要使用路径！
- 程序配置文件必须符合规范！
- NullPointerException 没有注册到资源！
- 输出的xml文件中存在中文乱码问题！
- maven没有资源导出问题！

### 7、万能Map

假设，我们的实体类，或者数据库中的表、字段胡总和参数过多，我们应当考虑使用Map!

```
//使用万能的Map插入一个用户
int addUser2(Map<String, Object> map);
<!--使用万能的Map插入一个用户-->
<!--对象中的属性可以直接取出来   传递Map的key-->
<insert id="addUser2" parameterType="Map">
    insert into mybatis.user (id, name, pwd) values(#{userId}, #{userName}, #{passWord})
</insert>
//使用万能的Map添加一个用户
@Test
public void addUser2(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    UserMapper mapper = sqlSession.getMapper(UserMapper.class);

    Map<String, Object> map = new HashMap<String, Object>();
    map.put("userId", 4);
    map.put("userName", "詹姆斯哈登");
    map.put("passWord", "123456");
    mapper.addUser2(map);

    //不要忘了提交事务
    sqlSession.commit();
    sqlSession.close();
}
```

Map传递参数，直接在sql中取出key即可！【parameterType=”Map”】

对象传递参数需要，直接在sql中取对象的属性即可！例如：【parameterType=”com.wyqian.pojo.User”】

只有一个基本类型参数的情况下，可以直接在sql中取到！例如：【parameterType=”int”】或者不谢，但是这仅限一个参数的情况下，多个参数是不行的！

多个参数用Map，**或者注解！**

### 8、思考题

模糊查询怎么写？

1. Java代码执行的时候，传递通配符% %

   ```
   //模糊查询
   List<User> getUserLike(String name);
   ```

   ```
   <!--模糊查询-->
   <select id="getUserLike" resultType="com.wyqian.pojo.User">
       select * from mybatis.user where name like #{name}
   </select>
   ```

   ```
   //模糊查询
   @Test
   public void getUserLike(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       List<User> userList = mapper.getUserLike("%王%");
       for (User user : userList) {
           System.out.println(user);
       }
       sqlSession.close();
   }
   ```

2. 在sql拼接中使用通配符！

   ```
   //模糊查询
   List<User> getUserLike(String name);
   ```

   ```
   <!--模糊查询-->
   <select id="getUserLike" resultType="com.wyqian.pojo.User">
       select * from mybatis.user where name like "%"#{name}"%"
   </select>
   ```

   ```
   //模糊查询
   @Test
   public void getUserLike(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       List<User> userList = mapper.getUserLike("王");
       for (User user : userList) {
           System.out.println(user);
       }
       sqlSession.close();
   }
   ```

## 4、配置解析

### 1、核心配置文件

- mybatis-config.xml

- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。

  ```
  configuration（配置）
      properties（属性）
      settings（设置）
      typeAliases（类型别名）
      typeHandlers（类型处理器）
      objectFactory（对象工厂）
      plugins（插件）
      environments（环境配置）
      environment（环境变量）
      transactionManager（事务管理器）
      dataSource（数据源）
      databaseIdProvider（数据库厂商标识）
      mappers（映射器）
  ```

### 2、环境配置（environments）

MyBatis 可以配置成适应多种环境

**不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

学会使用配置多套运行环境!

Mybatis默认的事务管理器就是JDBC，连接池：POOLED

### 3、属性（properties）

我们可以通过properties属性来实现引用配置文件

这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置。【db.properties】

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-29_150431.png)

编写一个配置文件

db.properties

```
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=UTF-8
username=root
password=123456
```

在核心配置文件中引入

```
<!--引入外部配置文件-->
<properties resource="db.properties">
    <property name="username" value="root"/>
    <property name="pwd" value="123456"/>
</properties>
```

- 可以直接引入外部文件
- 可以在其中增加一些属性配置
- 如果有两个文件有同一个字段，优先使用外部配置文件的！

### 4、类型别名（typeAliases）

- 类型别名可为 Java 类型设置一个缩写名字。
- 意在降低冗余的全限定类名书写。

```
<!--可以给实体类起别名-->
<typeAliases>
    <typeAlias type="com.wyqian.pojo.User" alias="User"/>
</typeAliases>
```

也可以指定一个包名，MyBatis 会在包名下面搜索需要的 Java Bean。

扫描实体类的包，他的默认别名就为这个类的类名，首字母小写！

```
<typeAliases>
    <package name="com.wyqian.pojo"/>
</typeAliases>
```

在实体类比较少的时候，使用第一种方式

如果实体类十分多，建议使用第二种。

第一种可以DIY别名，第二种则不行。如果非要改，需要在实体类上增加注解

```
//实体类
@Alias("user")
public class User {...}
```

### 5、设置

这是 MyBatis 中极为重要的调整设置，它们会改变 MyBatis 的运行时行为。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-29_163152.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-29_163128.png)

### 6、其他配置

- typeHandlers（类型处理器）
- objectFactory（对象工厂）
- plugins（插件）
  - mybatis-generator-core
  - mybatis-core
  - 通用mapper

### 7、映射器（mappers）

MapperRegistry：注册绑定我们的Mapper文件

方式一：【推荐使用】

```
<!--每一个Mapper.xml都要在mybatis-config.xml文件中注册-->
<mappers>
    <mapper resource="com/wyqian/dao/UserMapper.xml"></mapper>
</mappers>
```

方式二：使用class文件绑定注册

```
<mappers>
    <mapper class="com.wyqian.dao.UserMapper"></mapper>
</mappers>
```

注意点：

- 接口和它的Mapper配置文件必须同名！
- 接口和它的Mapper配置文件必须在同一个包下

方式三：使用扫描包进行注入绑定

```
<mappers>
    <package name="com.wyqian.dao"/>
</mappers>
```

练习时间：

- 将数据库配置文件外部引入
- 实体类别名
- 保证UserMapper接口和UserMapper.xml改为一致！并且放在同一个包下！

### 8、生命周期和作用域

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-29_192955.png)

生命周期和作用域是至关重要的，因为错误的使用会导致非常严重的**并发问题**。

**SqlSessionFactoryBuilder**：

- 一旦创建了SqlSessionFactory，就不再需要它了
- 局部变量

**SqlSessionFactory**：

- 说白了就是可以想象为：数据库连接池
- SqlSessionFactory 一旦被创建就应该在应用的运行期间一直存在，**没有任何理由丢弃它或重新创建另一个实例。**
- 因此 SqlSessionFactory 的最佳作用域是应用作用域。说白了程序开始它就开始，程序结束它就结束。
- 最简单的就是使用**单例模式**或者静态单例模式。

**SqlSession**：

- 连接到数据库连接池的一个请求！
- SqlSession 的实例不是线程安全的，因此是不能被共享的。所以它的最佳的作用域是请求或方法作用域。
- 用完之后需要赶紧关闭，否则资源被占用！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-29_200648.png)

这里面的每一个Mapper，就代表一个具体的业务！

## 5、解决属性名和字段名不一致的问题

### 1、问题

数据库中的字段

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_141852.png)

新建一个项目，拷贝之前的，测试实体类字段不一致的情况

```
public class User {
    private int id;
    private String name;
    private String password;
}
```

测试出现问题：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_143509.png)

```
select * from mybatis.user where id = #{id}
类型处理器
select id,name,pwd from mybatis.user where id = #{id}
```

解决方案：

- 起别名

  ```
  <select id="getUserById" resultType="com.wyqian.pojo.User" parameterType="int">
      select id, name, pwd as password from mybatis.user where id = #{id}
  </select>
  ```

### 2、resultMap

结果集映射

```
id   name   password---实体类
id   name   pwd---数据库字段
<!--结果集映射-->
    <resultMap id="UserMap" type="User">
    <!--column数据库中的字段，property实体类的属性-->
    <result column="id" property="id"></result>
    <result column="name" property="name"></result>
    <result column="pwd" property="password"></result>
    </resultMap>

    <select id="getUserById"  parameterType="int" resultMap="UserMap">
    select * from mybatis.user where id = #{id}
</select>
```

- `resultMap` 元素是 MyBatis 中最重要最强大的元素。
- `ResultMap`的设计思想是，对简单的语句做到零配置，对于复杂一点的语句，只需要描述语句之间的关系就行了。
- `ResultMap`最优秀的地方在于，虽然你已经对它相当了解了，但是根本就不需要显式地用到他们。
- 如果这个世界总是这么简单就好了。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_152102.png)

## 6、日志

### 6.1、日志工厂

如果一个数据库操作，出现了异常，我们需要排错。日志就是最好的助手！

曾经：sout、debug

现在：日志工厂！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_153410.png)

- SLF4J
- LOG4J 【掌握】
- LOG4J2
- JDK_LOGGING
- COMMONS_LOGGING
- STDOUT_LOGGING【掌握】
- NO_LOGGING

在Mybatis种具体使用哪一个日志实现，在设置种设定！

**STDOUT_LOGGING标准日志输出**

在mybatis核心配置文件中，配置我们的日志！

```
<settings>
    <!--标准的日志工厂实现-->
    <setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_154442.png)

### 6.2、Log4j

什么是Log4j?

- Log4j是Apache的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件。
- 我们也可以控制每一条日志的输出格式。
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。
- 通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

1、先导入Log4j的包

```
<!--导入log4j的依赖-->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2、log4j.properties

```
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=【%c】-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/kuang.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=【%p】【%d{yy-MM-dd}】【%c】%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

3、配置log4j为日志的实现

```
<settings>
    <setting name="logImpl" value="LOG4J"/>
</settings>
```

4、Log4j的使用！直接测试运行刚才的查询

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_161248.png)

**简单使用**

1、在要使用Log4j的类中，导入包import org.apache.log4j.Logger;

2、日志对象，参数为当前类的class

```
static Logger logger = Logger.getLogger(UserDaoTest.class);
```

3、日志级别

```
logger.info("info:进入了testLog4j");
logger.debug("debug:进入了testLog4j");
logger.error("error:进入了testLog4j");
```

## 7、分页

**思考：为什么要分页？**

- 减少数据的处理量

### 7.1、使用Limit分页

语法：

```
select * from user limit 0,2;
select * from user limit 4;#[0,n)
```

使用Mybatis实现分页，核心SQL

1. 接口

   ```
   //limit分页
   List<User> getUserByLimit(Map<String, Object> map);
   ```

2. Mapper.xml

   ```
   <!--分页-->
   <select id="getUserByLimit" parameterType="map" resultMap="UserMap">
       select * from mybatis.user limit #{startIndex}, #{pageSize}
   </select>
   ```

3. 测试

   ```
   //limit分页测试
   @Test
   public void getUserByLimit(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       UserDao mapper = sqlSession.getMapper(UserDao.class);
       Map<String, Object> map = new HashMap<String, Object>();
       map.put("startIndex", 0);
       map.put("pageSize", 2);
       List<User> userList = mapper.getUserByLimit(map);
       for (User user : userList) {
           System.out.println(user);
       }
   
       sqlSession.close();
   }
   ```

### 7.2、RowBounds分页

不再使用SQL实现分页

1. 接口

   ```
   //分页2
   List<User> getUserByRowBounds();
   ```

2. mapper.xml

   ```
   <!--分页2-->
   <select id="getUserByRowBounds" resultMap="UserMap">
       select * from mybatis.user
   </select>
   ```

3. 测试

   ```
   /*
       分页2
       在java代码层面上实现
        */
   @Test
   public void getUserByRowBounds(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
       RowBounds rowBounds = new RowBounds(0,2);
   
       List<User> userList = sqlSession.selectList("com.wyqian.dao.UserDao.getUserByRowBounds", null, rowBounds);
       for (User user : userList) {
           System.out.println(user);
       }
       sqlSession.close();
   }
   ```

### 7.3、分页插件

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_204658.png)

了解即可，万一以后公司架构师说要使用，你需要它是什么东西！

## 8、使用注解开发

### 8.1、面向接口编程

- 大家之前都学过面向对象编程，也学习过接口，但在真正的开发中，很多时候我们会选择面向接口编程
- **根本原因 : 解耦 , 可拓展 , 提高复用 , 分层开发中 , 上层不用管具体的实现 , 大家都遵守共同的标准 , 使得开发变得容易 , 规范性更好**
- 在一个面向对象的系统中，系统的各种功能是由许许多多的不同对象协作完成的。在这种情况下，各个对象内部是如何实现自己的,对系统设计人员来讲就不那么重要了；
- 而各个对象之间的协作关系则成为系统设计的关键。小到不同类之间的通信，大到各模块之间的交互，在系统设计之初都是要着重考虑的，这也是系统设计的主要工作内容。面向接口编程就是指按照这种思想来编程。

**关于接口的理解**

- 接口从更深层次的理解，应是定义（规范，约束）与实现（名实分离的原则）的分离。
- 接口的本身反映了系统设计人员对系统的抽象理解。
- 接口应有两类：
- - 第一类是对一个个体的抽象，它可对应为一个抽象体(abstract class)；
  - 第二类是对一个个体某一方面的抽象，即形成一个抽象面（interface）；
- 一个体有可能有多个抽象面。抽象体与抽象面是有区别的。

**三个面向区别**

- 面向对象是指，我们考虑问题时，以对象为单位，考虑它的属性及方法 .
- 面向过程是指，我们考虑问题时，以一个具体的流程（事务过程）为单位，考虑它的实现 .
- 接口设计与非接口设计是针对复用技术而言的，与面向对象（过程）不是一个问题.更多的体现就是对系统整体的架构

### 8.2、使用注解开发

1. 注解在接口上实现

   ```
   @Select("select * from mybatis.user")
   List<User> getUser();
   ```

2. 需要在核心配置文件中绑定接口

   ```
   <mappers>
       <mapper class="com.wyqian.dao.UserMapper"></mapper>
   </mappers>
   ```

3. 测试使用

   ```
   @Test
   public void getUser(){
       SqlSession sqlSession = MybatisUtils.getSqlSession();
   
       //底层主要应用反射
       UserMapper mapper = sqlSession.getMapper(UserMapper.class);
       List<User> userList = mapper.getUser();
       for (User user : userList) {
           System.out.println(user);
       }
   
       sqlSession.close();
   }
   ```

本质：反射机制实现

底层：动态代理！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-30_213452.png)

**Mybatis详细的执行流程！**

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/20201017070716720.png)

### 8.3、CRUD

我们可以在工具类创建的时候开启自动提交事务！

```
public static SqlSession getSqlSession(){
    return sqlSessionFactory.openSession(true);//开启自动提交事务
}
```

编写接口，增加注解

```
public interface UserMapper {

    @Select("select * from mybatis.user")
    List<User> getUser();

    //方法存在多个参数，所以参数前面一定要加上@Param("id")注解
    //引用对象不需要写@Param
    @Select("select * from mybatis.user where id = ${id}")
    User getUserById(@Param("id") int id);

    //添加一个用户
    @Insert("insert into mybatis.user (id, name, pwd) values(#{id}, #{name}, #{password})")
    int insertUser(User user);

    //修改用户
    @Update("update mybatis.user set name = #{name}, pwd = #{password} where id = #{id}")
    int updateUser(User user);

    //删除一个用户
    @Delete("delete from mybatis.user where id = #{id2}")
    int deleteUser(@Param("id2") int id);
}
```

测试类

【注意：我们必须要将接口注册绑定到我们的核心配置文件中！】

**关于@Param()注解**

- 基本类型的参数或者String类型，需要加上
- 引用类型不需要加
- 如果只有一个基本类型的话，可以忽略，但是建议大家都加上！
- 我们在SQL中引用的就是我们这里的@Param(“uid”)中设定的属性名！

**#{} ${}区别**

就相当于statement和prepareStatement的区别，#{}可以防止SQL注入，而${}无法防止SQL注入！

## 9、Lombok

```
Project Lombok is a java library that automatically plugs into your editor and build tools, spicing up your java.
Never write another getter or equals method again, with one annotation your class has a fully featured builder, Automate your logging variables, and much more.
```

- java library
- plugs
- build tools
- with one annotation your class

使用步骤:

1. 在IDEA中安装Lombok插件！

2. 在项目中导入lombok的jar包

   ```
   <dependency>
       <groupId>org.projectlombok</groupId>
       <artifactId>lombok</artifactId>
       <version>1.18.12</version>
   </dependency>
   ```

3. 在实体类上加注解即可！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-31_110055.png)

说明：

```
@Data：无参构造、get、set、toString、hashcode、equals
@AllArgsConstructor  有参构造
@NoArgsConstructor   无参构造
@Getter  and   @Setter
@ToString
@EqualsAndHashCode
```

4、测试：

```
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String password;
}
```

三个注解就实现了之前的用IDEA ALT+Insert实现的所有方法！

但是lombok有好处也有坏处，好处是简洁，坏处就是减少源码的可读性！

## 10、多对一处理

### 10.1、测试环境搭建

多对一：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-31_113327.png)

- 多个学生，对应一个老师
- 对于学生这边而言，**关联**…多个学生，关联一个老师【多对一】
- 对于老师而言，**集合**，一个老师有很多学生【一对多】

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2020-12-31_193425.png)

SQL：

```
CREATE TABLE `teacher` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO teacher(`id`, `name`) VALUES (1, '秦老师'); 

CREATE TABLE `student` (
  `id` INT(10) NOT NULL,
  `name` VARCHAR(30) DEFAULT NULL,
  `tid` INT(10) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `fktid` (`tid`),
  CONSTRAINT `fktid` FOREIGN KEY (`tid`) REFERENCES `teacher` (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('1', '小明', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('2', '小红', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('3', '小张', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('4', '小李', '1'); 
INSERT INTO `student` (`id`, `name`, `tid`) VALUES ('5', '小王', '1');
```

测试环境搭建：

1. 导入lombok的包

2. 新建实体类Teacher、Student

   ```
   package com.wyqian.pojo;
   
   import lombok.Data;
   
   @Data
   public class Teacher {
       private int id;
       private String name;
   }
   ```

   ```
   package com.wyqian.pojo;
   
   import lombok.Data;
   
   @Data
   public class Student {
       private int id;
       private String name;
   
       //学生需要关联一个老师！
       private Teacher teacher;
   }
   ```

3. 写接口。TeacherMapper和StudentMapper接口

4. 建立Mapper.xml文件

5. 在核心配置文件中绑定注册我们的mapper接口

6. 测试查询是否能够成功！

### 10.2、按照查询嵌套处理

```
<!--
    思路:
        1、查询所有的学生信息
        2、根据查询出来的tid，寻找对应的老师！   子查询
    -->
<select id="getStudent" resultMap="StudentTeacher">
    select * from mybatis.student
</select>

<resultMap id="StudentTeacher" type="Student">
    <result property="id" column="id"></result>
    <result property="name" column="name"></result>
    <!--
        复杂的属性我们需要单独处理，对象：association  集合：collection
        -->
    <association property="teacher" column="tid" javaType="Teacher" select="getTeacher"></association>
</resultMap>

<select id="getTeacher" resultType="Teacher">
    select * from mybatis.teacher where id = #{id}
</select>
```

### 10.3、按照结果嵌套处理

```
<!--这种方式类似联表查询-->
<select id="getStudent2" resultMap="StudentTeacher2">
    select s.id sid, s.name sname, t.name tname
    from mybatis.student s, mybatis.teacher t
    where s.tid = t.id
</select>
<resultMap id="StudentTeacher2" type="Student">
    <result property="id" column="sid"></result>
    <result property="name" column="sname"></result>
    <association property="teacher" javaType="Teacher">
        <result property="name" column="tname"></result>
    </association>
</resultMap>
```

回顾Mysql多对一查询方式：

- 子查询
- 联表查询

## 11、一对多处理

比如：一个老师拥有多个学生！

对于老师而言，就是一对多的关系！

### 11.1、环境搭建

和刚才一样，实体类有点变化

**实体类**

```
package pojo;

import lombok.Data;

import java.util.List;

@Data
public class Teacher {
    private int id;
    private String name;

    //一个老师拥有关联多个学生
    private List<Student> students;
}
package pojo;

import lombok.Data;

@Data
public class Student {
    private int id;
    private String name;
    private int tid;
}
```

### 按照查询嵌套处理

```
<!--按照查询做嵌套处理-->
<select id="getStudentsTeacher2" resultMap="getST2">
    select * from mybatis.teacher where id = #{tid}
</select>
<resultMap id="getST2" type="Teacher">
    <result property="id" column="id"></result>
    <collection property="students" javaType="ArrayList" ofType="Student" select="getS" column="id">
    </collection>
</resultMap>

<select id="getS" resultType="Student">
    select * from mybatis.student where tid = #{tid}
</select>
```

### 按照结果嵌套处理

```
<!--按照结果嵌套处理-->
<select id="getStudentsTeacher" resultMap="getST">
    select s.id sid,s.name sname,s.tid stid, t.id tid,t.name tname
    from mybatis.teacher t, mybatis.student s
    where t.id = s.tid and t.id = #{tid}
</select>
<resultMap id="getST" type="Teacher">
    <result property="id" column="tid"/>
    <result property="name" column="tname"/>
    <collection property="students" ofType="Student">
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
        <result property="tid" column="stid"/>
    </collection>
</resultMap>
```

### 小结

1. 关联-association 【多对一】
2. 集合-collection【一对多】
3. javaType & ofType
   1. javaType 用来指定实体类中属性的类型
   2. ofType 用来指定映射到List或者集合中的pojo类型，泛型中的约束类型

注意点：

1. 保证SQL的可读性，尽量保证通俗易懂
2. 注意一对多和多对一中，属性名和字段的问题！
3. 如果问题不好排查错误，可以使用日志，建议使用Log4j

慢SQL 1s 1000s

面试高频：

- Mysql引擎
- InnoDB底层原理
- 索引
- 索引优化！

## 12、动态SQL

**什么是动态SQL：动态SQL就是指根据不同的条件生成不同的SQL语句**

利用动态 SQL，可以彻底摆脱这种痛苦——根据不同条件拼接 SQL 语句。

```
如果你之前用过 JSTL 或任何基于类 XML 语言的文本处理器，你对动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

- if
- choose (when, otherwise)
- trim (where, set)
- foreach
```

### 12.1、搭建环境

```
CREATE TABLE `blog`(
  `id` VARCHAR(50) NOT NULL COMMENT '博客id',
  `title` VARCHAR(100) NOT NULL COMMENT '博客标题',
  `author` VARCHAR(30) NOT NULL COMMENT '博客作者',
  `create_time` DATETIME NOT NULL COMMENT '创建时间',
  `views` INT(30) NOT NULL COMMENT '浏览量' 
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

创建一个基础工程

1. 导包

2. 编写配置文件

3. 编写实体类

   ```
   package com.wyqian.pojo;
   
   import lombok.Data;
   
   import java.util.Date;
   
   @Data
   public class Blog {
       private String id;
       private String title;
       private String author;
       private Date createTime;
       private int views;
   }
   ```

4. 编写实体类对应的Mapper接口和Mapper.xml文件

### 12.2、if

接口

```
//测试IF
List<Blog> getBlogsByIf(Map map);
```

xml文件

```
<select id="getBlogsByIf" parameterType="map" resultType="blog">
    select * from mybatis.blog where 1=1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>
```

测试类

```
@Test
public void getBlogsByIf(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();

    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
    HashMap map = new HashMap();
    //        map.put("title", "Java如此简单");
    map.put("author", "钱万云");
    List<Blog> blogsByIf = mapper.getBlogsByIf(map);
    for (Blog blog : blogsByIf) {
        System.out.println(blog);
    }

    sqlSession.close();
}
```

### 12.3、choose (when, otherwise)

```
<select id="getBlogByWhereChooseWhen" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <choose>
            <when test="title != null">
                and title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```

### 12.4、trim (where, set)

```
<select id="getBlogByWhereIf" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <if test="title != null">
            title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
<update id="updateBlog" parameterType="map">
    update mybatis.blog
    <set>
        <if test="title != null">
            title = #{title},
        </if>
        <if test="author != null">
            author = #{author},
        </if>
    </set>
    where id = #{id}
</update>
```

所谓的动态SQL，本质还是SQL语句，只是我们可以在SQL层面，去执行一个逻辑代码

### 12.5、SQL片段

有的时候，我们可能会将一些公共的部分抽取出来，方便复用！

1. 使用SQL标签抽取公共的部分

   ```
   <sql id="update-set">
       <set>
           <if test="title != null">
               title = #{title},
           </if>
           <if test="author != null">
               author = #{author},
           </if>
       </set>
   </sql>
   ```

2. 在需要的地方使用Include标签引用即可

   ```
   <update id="updateBlog" parameterType="map">
       update mybatis.blog
       <include refid="update-set"></include>
       where id = #{id}
   </update>
   ```

注意事项：

1. 最好基于单表来定义SQL片段
2. 不要存在where标签

### 12.6、Foreach

```
select * from user where 1=1 and (id=1 or id=2 or id=3)
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_104715.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_111321.png)

```
<!--select * from mybatis.blog where 1=1 and (id=1 or id=2 or id=3)-->
<!--我们现在传递一个万能的map，这个map中可以存在一个集合-->
<select id="selectForEach" parameterType="map" resultType="blog">
    select * from mybatis.blog
    <where>
        <foreach collection="ids"  item="id" open="and (" close=")" separator="or">
            id = #{id}
        </foreach>
    </where>
</select>
```

测试类：

```
@Test
public void selectForEach(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();


    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
    HashMap map = new HashMap();
    List<Integer> ids = new ArrayList<Integer>();
    ids.add(1);
    map.put("ids", ids);
    List<Blog> blogs = mapper.selectForEach(map);
    for (Blog blog : blogs) {
        System.out.println(blog);
    }
    sqlSession.close();
}
```

**动态SQL就是在拼接SQL语句，我们只要保证SQL的正确性，按照SQL的格式，去排列组合就可以了！**

建议：

- 先在Mysql中写出完整的SQL，再对应地去修改成为我们的动态SQL实现通用即可！

## 13、缓存

### 13.1、简介

```
查询：连接数据库，耗资源！
一次查询的结果，给他暂存在一个可以直接取到的地方！--->内存：缓存！
我们再次查询相同数据的时候，直接走缓存，就不用走数据库了！
```

1、什么是缓存 [ Cache ]？

- 存在内存中的临时数据。
- 将用户经常查询的数据放在缓存（内存）中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。

2、为什么使用缓存？

- 减少和数据库的交互次数，减少系统开销，提高系统效率。

3、什么样的数据能使用缓存？

- 经常查询并且不经常改变的数据。【可以使用缓存】

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_151640.png)

### 13.2、Mybatis缓存

- MyBatis包含一个非常强大的查询缓存特性，它可以非常方便地定制和配置缓存。缓存可以极大的提升查询效率。
- MyBatis系统中默认定义了两级缓存：**一级缓存**和**二级缓存**
  - 默认情况下，只有一级缓存开启。（SqlSession级别的缓存，也称为本地缓存）
  - 二级缓存需要手动开启和配置，他是基于namespace级别的缓存。
  - 为了提高扩展性，MyBatis定义了缓存接口Cache。我们可以通过实现Cache接口来自定义二级缓存

### 13.3、一级缓存

一级缓存也叫本地缓存：

- 与数据库同一次会话期间查询到的数据会放在本地缓存中。
- 以后如果需要获取相同的数据，直接从缓存中拿，没必须再去查询数据库；

测试步骤：

1. 开启日志！
2. 测试在一个Session中查询两次相同记录。
3. 查看日志输出。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_153232.png)

缓存失效的情况：

1. 查询不同的东西

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_154711.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_154757.png)

2. 增删改操作，可能会改变原来的数据，所以必定会刷新缓存！

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_155244.png)

3. 查询不同的Mapper.xml

4. 手动清理缓存

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_155528.png)

小结：一级缓存默认是开启的，只在一次SqlSession中有效，也就是拿到连接到关闭连接的这个区间段！

一级缓存就是一个Map。

### 13.4、二级缓存

- 二级缓存也叫全局缓存，一级缓存作用域太低了，所以诞生了二级缓存
- 基于namespace级别的缓存，一个名称空间，对应一个二级缓存；
- 工作机制
  - 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中；
  - 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存到二级缓存中；
  - 新的会话查询信息，就可以从二级缓存中获取内容；
  - 不同的mapper查出的数据会放在自己对应的缓存（map）中；

步骤：

1. 开启全局缓存

   ```
   <!--显式地开启缓存-->
   <setting name="cacheEnabled" value="true"/>
   ```

2. 在要使用二级缓存地Mapper中开启

   ```
   <!--在当前Mapper.xml文件中使用二级缓存-->
   <cache/>
   ```

   也可以自定义参数

   ```
   <cache
          eviction="FIFO"
          flushInterval="60000"
          size="512"
          readOnly="true"/>
   ```

3. 测试

   1. 问题：我们需要将实体类序列化！否则就会报错！

   ```
   package com.wyqian.dao;
   
   import com.wyqian.pojo.User;
   import com.wyqian.utils.MybatisUtils;
   import org.apache.ibatis.session.SqlSession;
   import org.junit.Test;
   
   public class MyTest {
       @Test
       public void getUserById(){
           SqlSession sqlSession1 = MybatisUtils.getSqlSession();
           SqlSession sqlSession2 = MybatisUtils.getSqlSession();
   
           UserMapper mapper1 = sqlSession1.getMapper(UserMapper.class);
           User user1 = mapper1.getUserById(1);
           System.out.println(user1);
           sqlSession1.close();
           //sqlSession到这儿就结束了，二级缓存派上用场！
   
           //mapper.updateUser(new User(2, "dgasu", "12343"));
           //sqlSession.clearCache();//手动清理缓存！
   
           System.out.println("============================");
           UserMapper mapper2 = sqlSession2.getMapper(UserMapper.class);
           User user2 = mapper2.getUserById(1);
           System.out.println(user2);
   
           System.out.println(user1==user2);
   
   
           sqlSession2.close();
       }
   }
   ```

小结：

- 只要开启了二级缓存，在同一个Mapper中有效
- 所有的数据都会先放在一级缓存中；
- 只有当会话提交，或者关闭的时候，才会提交到二级缓存中！

### 13.5、缓存原理

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_163407.png)

### 13.6、自定义缓存-ehcache

```
Ehcache是一种广泛使用的开源Java分布式缓存。主要面向通用缓存。
```

要在程序中使用ehcache，先要导包！

```
<!-- https://mvnrepository.com/artifact/org.mybatis.caches/mybatis-ehcache -->
<dependency>
    <groupId>org.mybatis.caches</groupId>
    <artifactId>mybatis-ehcache</artifactId>
    <version>1.2.1</version>
</dependency>
```

在mapper中指定使用我们的ehcache缓存实现！

```
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

ehcache.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
         updateCheck="false">

    <diskStore path="./tmpdir/Tmp_EhCache"/>

    <defaultCache
                  eternal="false"
                  maxElementsInMemory="10000"
                  overflowToDisk="false"
                  diskPersistent="false"
                  timeToIdleSeconds="1800"
                  timeToLiveSeconds="259200"
                  memoryStoreEvictionPolicy="LRU"/>

    <cache
           name="cloud_user"
           eternal="false"
           maxElementsInMemory="5000"
           overflowToDisk="false"
           diskPersistent="false"
           timeToIdleSeconds="1800"
           timeToLiveSeconds="1800"
           memoryStoreEvictionPolicy="LRU"/>
</ehcache>
<!--
            <cache     name 缓存名唯一标识
                       maxElementsInMemory="1000" 内存中最大缓存对象数
                       eternal="false" 是否永久缓存
                       timeToIdleSeconds="3600" 缓存清除时间 默认是0 即永不过期
                       timeToLiveSeconds="0" 缓存存活时间 默认是0 即永不过期
                       overflowToDisk="true" 缓存对象达到最大数后，将其写入硬盘
                       maxElementsOnDisk="10000"  磁盘最大缓存数
                       diskPersistent="false" 磁盘持久化
                       diskExpiryThreadIntervalSeconds="120" 磁盘缓存的清理线程运行间隔
                       memoryStoreEvictionPolicy="FIFO" 缓存清空策略
                       FIFO 先进先出
                       LFU  less frequently used  最少使用
                       LRU  least recently used 最近最少使用
        />
        -->
```

Redis数据库来做缓存！K-V键值对