# mysql基础

### 1、初识MySQL



JavaEE: 企业级开发 Web

前端（页面：展示，数据！）

后台：（连接点：连接数据库JDBC，连接前端（控制，控制视图跳转，和给前端传递数据））

数据库（存数据，txt， excel， word）

> 只会写代码，学好数据库，基本混饭吃
>
> 操作系统，数据结构与算法！当一个不错的程序员！
>
> 离散数学，数字电路，体系结构，编译原理。 + 实战经验，高级程序员~优秀的程序员

#### 1.1、为什么学习数据库

1、岗位需求

2、现在的世界，大数据时代~，得数据者得天下

3、被迫需求：存数据

4、***数据库是所有软件体系中最核心的存在\*** DBA数据库管理员

#### 1.2、什么是数据库

数据库（DB，DataBase）

概念：数据仓库，软件，安装在操作系统（windows,linux,mac…）之上! SQL，可以存储大量的数据。500万！

作用：存储数据，管理数据

#### 1.3、数据库分类

关系型数据库：(SQL)

- MySQL，Oracle，Sql Server，DB2，SQLlite
- 通过表和表之间，列和列之间的关系进行数据的存储，学员信息表，考勤表……

非关系型数据库（NOSQL）Not Only SQL

- Redis，MongoDB
- 非关系型数据库，对象存储，通过对象的自身的属性来决定。

***DBMS(数据库管理系统)\***

- 数据库的管理软件，科学有效的管理我们的数据。维护和获取数据；
- MySQL，数据库管理系统！

![img](https://i.loli.net/2020/11/07/VPgXZdD1uyzH5kO.png)

#### 1.4、MySQL简介

MySQL是一个**关系型数据库管理系统**

前世：瑞典MySQL AB公司

今生：属于Oracle旗下产品

MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (Relational Database Management System，关系数据库管理系统) 应用软件之一。

开源的数据库软件~

体积小、速度快、总体拥有成本低，招人成本比较低，所有人必须会~

中小型网站，或者大型网站，集群

官网：https://www.mysql.com/

官网下载地址：https://dev.mysql.com/downloads/mysql/

5.7 稳

安装建议：

1、尽量不要使用exe，注册表

2、尽可能使用压缩包安装~

#### 1.5、安装MySQL

教程:https://mp.weixin.qq.com/s/E1PM4EHwU6Joot4OG0gDjw

![img](https://i.loli.net/2020/11/07/mz2rOqyXJYtQWhe.png)

> sc delete mysql，清空服务

#### 1.6、安装SQLyog

教程:https://mp.weixin.qq.com/s/E1PM4EHwU6Joot4OG0gDjw

![img](https://i.loli.net/2020/11/07/scbfA1wYCH7Rn6q.png)

1、新建一个数据库school

![img](https://i.loli.net/2020/11/07/o8dvULX2ZxlOYbs.png)

***每一个sqlyog的执行操作，本质上就是对应了一个sql，可以在软件的历史记录中查看。\***😁

2、新建一张表student

![img](https://i.loli.net/2020/11/07/PUYcxhzKOfFuqZw.png)

```
字段：id，name,age
```

3、添加一些数据

![2020-11-07_143800](https://i.loli.net/2020/11/07/B5ujwTyhRW9al27.png)

#### 1.7、连接数据库

命令行连接

```
mysql -uroot -p123456 --连接数据库
update user set password=password('123456')where user='root'; --修改密码
flush privileges;--刷新数据库

-------------------------------------------
-- 所有语句都使用；结尾
show databases;--显示所有数据库
use school;--切换数据库 use 数据库名
show tables;--查看数据库中所有的表
describe student;--查看特定表的详细设计信息
create database westos;--创建一个数据库

exit;--退出连接
-- 单行注释（SQL的本来的注释）
/*
多行注释（sql的多行注释）
*/
```

数据库***语言 CRUD增删改查！

DDL 定义

DML 操作

DQL 查询

DCL 控制

### 2、操作数据库

操作数据库>操作数据库中的表>操作数据库中表的数据

***MySQL关键字不区分大小写\***

#### 2.1、操作数据库(了解)

1、创建数据库

```
CREATE DATABASE [IF NOT EXISTS] NBA;
```

2、删除数据库

```
DROP DATABASE IF EXISTS NBA;
```

3、使用数据库

```
--``tab键的上面，如果你的表明或者字段名是一个特殊字符，就需要带``
USE `school`;
```

4、查看数据库

```
SHOW DATABASES;--查看所有数据库
```

学习思路：

- 对照sqlyog可视化历史记录查看sql。
- 固定的语法或关键字必须要强行记住。

#### 2.2、数据库的列类型

> 数值

- tinyint 十分小的数据 1个字节
- smallint 较小的数据 2个字节
- mediumint 中等大小的数据 3个字节
- **int 标准的整数 4个字节** 常用的
- bigint 较大的数据 8个字节
- float 浮点数 4个字节
- double 浮点数 8个字节（精度问题！）
- decimal 字符串形式的浮点数 金融计算的时候一般使用decimal

> 字符串

- char 字符串固定大小的 0~255BYTES
- **varchar 可变字符串 0~65535**BYTES 常用的 String
- tinytext 微型文本 2^8-1BYTES
- **text 文本串 2^16-1**BYTES 保存大文本

> 时间日期

java.util.Date🕑

- date YYYY-MM-DD 日期格式
- time HH：mm：ss 时间格式
- **datetime YYYY-MM-DD HH：mm：ss 最常用的时间格式**
- **timestamp 时间戳 1970.1.1至今的毫秒数！**也较为常用
- year 年份表示

> null

- 没有值，未知
- **注意，不要使用NULL进行运算，结果为NULL**

#### 2.3、数据库的字段属性（重点）

**Unsigned:**

- 无符号的整数
- 声明了该列不能设置为负数

**zerofill:**

- 0填充的
- 不足的位数，使用0填充，int(3)，5—-005

**自增：**

- 通常可以理解为自动在上一条记录基础上+1(默认)
- 通常用来设计唯一的主键~index，必须是整数类型
- 可以自定义设计主键自增的起始值和步长

**非空：**NULL not null

- 假设设置为NOT NULL，如果不给他赋值，就会报错
- NULL，如果不填写值，默认就是null!

**默认：**

- 设置默认的值！
- sex，默认值为男，如果不指定该列的值，则会有默认的值！

扩展：

```
/*
每一个表，都必须存在以下五个字段！未来做项目用的，表示每一条记录存在意义！（阿里规范）
id 主键
`version` 乐观锁
is_delete  伪删除
gmt_create  创建时间
gmt_update  修改时间
*/
```

#### 2.4、创建数据库表（重点）

```
--目标：创建一个school数据库
--创建学生表（列、字段）  使用SQL创建
--学号、姓名、密码、性别、出生日期、家庭住址、电子邮箱

--注意点，使用英文()，表的名称和字段尽量使用``括起来
--AUTO_INCREMENT  自增
--字符串使用单引号括起来！
--所有语句后面加,(英文的)，最后一个不用加
--PRIMARY KEY 主键，一般一个表只有一个唯一的主键！
CREATE TABLE IF NOT EXISTS `student`(
  `id` INT(10) NOT NULL AUTO_INCREMENT COMMENT '学生id',
  `name` VARCHAR(20) NOT NULL DEFAULT '匿名' COMMENT '学生姓名',
  `pwd` VARCHAR(6) NOT NULL DEFAULT '123456' COMMENT '登陆密码',
  `sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
  `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
  `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
  `email` VARCHAR(20) DEFAULT NULL COMMENT '电子邮箱',
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8
```

格式：

```
CREATE TABLE [IF NOT EXISTS] `表名`(
	`字段名` 列类型 [属性] [索引] [注释]，
    `字段名` 列类型 [属性] [索引] [注释]，
    ......
    `字段名` 列类型 [属性] [索引] [注释]，
    PRIMARY KEY(`字段名`)
)[表类型][表的字符集设置]
```

常用命令：

```
SHOW CREATE DATABASE school;-- 查看创建数据库的语句
SHOW CREATE TABLE student;-- 查看创建表的语句 
DESC student;-- 显示表的结构
```

#### 2.5、数据表的类型

```
-- 关于数据库引擎
/*
INNODB  默认使用~
MYISAM  早些年使用
*/
```

|            | MYISAM | INNODB        |
| ---------- | ------ | ------------- |
| 事务支持   | 不支持 | 支持          |
| 数据行锁定 | 不支持 | 支持          |
| 外键约束   | 不支持 | 支持          |
| 全文索引   | 支持   | 不支持        |
| 表空间大小 | 较小   | 较大，约为2倍 |

常规使用操作：

- MYISAM 节约空间，速度较快
- INNODB 安全性高，事务的处理，多表多用户操作

> 在物理空间存在的位置

所有的数据库文件都存在data目录下，一个文件夹就对应一个数据库！

本质还是文件的存储！

MySQL引擎在物理文件上的区别

- INNODB在数据库表中只有一个*.frm文件，以及上级目录下的ibdata1文件
- MYISAM对应文件
  - *.frm - 表结构的定义文件
  - *.MYD - 数据文件（data）
  - *.MYI - 索引文件

> 设置数据库表的字符集编码

```
charset = utf8
```

不设置的话，会是MySQL默认的字符集编码~（不支持中文！）

https://www.jianshu.com/p/ec0c86ee3e04

MySQL的默认编码是Latin1，不支持中文

在my.ini中配置默认的编码

```
character-set-server=utf8
```

#### 2.6、修改删除表

> 修改

```
-- 修改表名 ALTER TABLE `旧表名` RENAME AS `新表名`
ALTER TABLE `teacher` RENAME AS `teacher1`
-- 增加表的字段 ALTER TABLE `表名` ADD 字段 列属性
ALTER TABLE `teacher1` ADD age INT(10)
-- 修改字段名 ALTER TABLE `表名` CHANGE 旧字段名 新字段名 列属性
ALTER TABLE `teacher1` CHANGE age `age1` INT(10)
-- 修改字段约束 ALTER TABLE `表名` MODIFY 字段名 列属性
ALTER TABLE `teacher1` MODIFY `age1` VARCHAR(10)
```

> 删除

```
-- 删除表中的字段 ALTER TABLE `表名` DROP 字段
ALTER TABLE `teacher1` DROP age
-- 删除表(如果表存在再删除)
DROP TABLE IF EXISTS `teacher1`
```

***所有的创建和删除操作尽量加上判断，以免报错~\***

注意点：

- ``字段名和表名，使用这个包裹~
- 注释 –
- sql关键字大小写不敏感，建议大家写小写~
- 所有符号全部用英文😁

### 3、MySQL数据管理

#### 3.1、外键（了解即可）

> 方式一：在创建表的时候，增加约束（麻烦，比较复杂）

```
CREATE TABLE `grade` (
  `gradeid` int(10) NOT NULL COMMENT '年级id',
  `name` varchar(20) NOT NULL COMMENT '姓名',
  PRIMARY KEY (`gradeid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
-- 学生表的gradeid字段要去引用年级表的gradeid字段
-- 先定义外键key
-- 给这个外键添加约束（执行引用）
CREATE TABLE IF NOT EXISTS `student` (
  `id` INT(10) NOT NULL AUTO_INCREMENT COMMENT '学生id',
  `name` VARCHAR(20) NOT NULL DEFAULT '匿名' COMMENT '学生姓名',
  `pwd` VARCHAR(6) NOT NULL DEFAULT '123456' COMMENT '登陆密码',
  `sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
  `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
  `gradeid` INT(10) NOT NULL COMMENT '年级id',
  `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
  `email` VARCHAR(20) DEFAULT NULL COMMENT '电子邮箱',
  PRIMARY KEY (`id`),
  KEY `FK_gradeid` (`gradeid`),
  CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade`(`gradeid`)
) ENGINE=INNODB DEFAULT CHARSET=utf8
```

删除有外键关系的表的时候，必须先删除引用别人的表（从表），在删除被引用的表（主表）。不然是删不掉的，会报错的😭

> 方式二：创建表成功后添加外键约束

```
CREATE TABLE `grade` (
  `gradeid` INT(10) NOT NULL COMMENT '年级id',
  `name` VARCHAR(20) NOT NULL COMMENT '姓名',
  PRIMARY KEY (`gradeid`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

CREATE TABLE `student` (
  `id` INT(10) NOT NULL AUTO_INCREMENT COMMENT '学生id',
  `name` VARCHAR(20) NOT NULL DEFAULT '匿名' COMMENT '学生姓名',
  `pwd` VARCHAR(6) NOT NULL DEFAULT '123456' COMMENT '登录密码',
  `sex` VARCHAR(2) NOT NULL DEFAULT '女' COMMENT '性别',
  `birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
  `gradeid` INT(10) NOT NULL COMMENT '年级id',
  `address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
  `email` VARCHAR(20) DEFAULT NULL COMMENT '电子邮箱',
  PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8
-- 现在是建表的时候没有外键约束
-- now我们来添加约束
ALTER TABLE `student`
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade` (`gradeid`)
```

#### 3.2、DML语言（全部记住）

数据库意义：数据存储，数据管理

DML语言：数据操作语言

- Insert
- update
- delete

#### 3.3、添加

```
-- 添加数据 INSERT INTO 表名(字段1,字段2...) VALUES(值1,值2)
INSERT INTO `grade` (`gradeid`,`name`) 
VALUES(1,'wyqian')
-- 一次性要插入多条数据
-- INSERT INTO 表名(字段1,字段2...) VALUES(值1,值2),(值1,值2)...
-- 添加多条数据
INSERT INTO `grade` (`gradeid`, `name`)
VALUES(2, 'sxs'),
(3,'lyt')
-- 添加数据时，如果不写前面的字段，那么后面values里面的值就要写全
INSERT INTO `grade` VALUES(4, 'lm')
```

注意事项：

1. 字段和字段之间使用英文逗号隔开
2. 字段是可以省略的，但事后面必须要一一对应，不能少
3. 可以同时插入多条数据，VALUES后面的值，需要使用，隔开即可`values(),(),()...`

#### 3.4、修改

```
UPDATE `student` SET pwd='000' -- 表中所有数据都被修改
-- 修改多个属性，使用逗号隔开
UPDATE `student` SET address='上海',email='sina@sina.com' WHERE NAME='wyqian'
-- 可以加条件，where子句
UPDATE `student` SET pwd='123' WHERE sex='男'
-- 使用多个条件定位数据
UPDATE `student` SET pwd='gsw' WHERE sex='女' AND address='成都'
```

| 操作符       | 含义         | 范围  | 结果  |
| ------------ | ------------ | ----- | ----- |
| =            | 等于         | 5=6   | false |
| <>或者!=     | 不等于       | 5<>6  | true  |
| >            |              |       |       |
| <            |              |       |       |
| >=           |              |       |       |
| <=           |              |       |       |
| BETWEEN…AND… | 在某个闭区间 | [2,5] |       |
| AND          |              |       |       |
| OR           |              |       |       |

#### 3.5、删除

```
-- 删除数据
DELETE FROM `student` WHERE NAME='wyqian'
-- 删除整张表的数据（尽量避免这样使用）
DELETE FROM `student` 
-- 使用TRUNCATE删除表的全部数据
TRUNCATE TABLE `student`
-- 使用delete和TRUNCATE删除表全部数据的区别
INSERT INTO `student` 
VALUES(2,'sxs','12345','男','2020-1-1',1,'北京','sxs@163.com'),
(3,'lyt','12345','女','2020-1-1',1,'兰州','lyt@163.com'),
(4,'lm','12345','女','2020-1-1',1,'成都','lm@163.com'),
(5,'ysh','12345','女','2020-1-1',1,'成都','ysh@163.com')

DELETE FROM `student`-- 不会修改自动增量，从上一次增量继续加1

INSERT INTO `student` 

VALUES(2,'sxs','12345','男','2020-1-1',1,'北京','sxs@163.com'),
(3,'lyt','12345','女','2020-1-1',1,'兰州','lyt@163.com'),
(4,'lm','12345','女','2020-1-1',1,'成都','lm@163.com'),
(5,'ysh','12345','女','2020-1-1',1,'成都','ysh@163.com')
TRUNCATE TABLE `student`-- 自动增量从1开始
```

了解即可：`delete删除的问题`，重启数据库（net start mysql），现象：

- INNODB 自增列会从1开始（存在内存中的，断电即失）
- MyISAM 继续从上一个增量开始（存在文件中的，不会丢失）

### 4、DQL查询数据（最重点）

#### 4.1、DQL

(Data Query Language：数据查询语言)

- 所有的查询笑傲做都要用到它 Select
- 简单的查询，复杂的查询它都能做~
- ***数据库中最核心的语言，最重要的语句\***
- 使用频率最高的语句

#### 4.2、指定查询的字段

```
-- 查询全部的学生 select * from 表名
SELECT * FROM student
-- 查询指定字段
SELECT `studentno`,`studentname` FROM student
-- 别名，给结果起别名，as，可以给字段也可以给表名起别名
SELECT `studentno` AS 学生学号,`studentname` AS 学生姓名 FROM student AS s
-- 函数  concat(a,b)
SELECT CONCAT('新名字：', `studentname`) AS 学生姓名 FROM student
```

语法：`select 字段,... from 表`

> 有时候，列名字不是那么的见名知意，我们起别名 AS 字段名 AS　表名

> 去重 distinct

作用：去除SELECT查询出来的结果中重复的数据，重复的数据只显示一条

```
SELECT DISTINCT `studentno`  FROM result--去除重复数据
```

> 数据库的列（表达式）

```
SELECT VERSION()-- 查询系统版本（函数）
SELECT 300*6/2+1 AS 计算结果 -- 用来计算（表达式）
SELECT @@auto_increment_increment-- 查询自增的步长（变量）

-- 学员考试成绩 加1查看
SELECT `studentno`,`studentresult`+1 AS '加分后' FROM result
```

**数据库中的表达式：文本值，列，Null，函数，计算表达式，系统变量**

*select 表达式 from 表*

> select完整语法

```
SELECT [ALL | DISTINCT]
{* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,...]}
FROM table_name [as table_alias]
	[left|right|inner join table_name2] -- 联合查询
    [WHERE ...]-- 指定结果需要满足的条件
    [GROUP BY...]-- 指定结果按照哪几个字段来分组
    [HAVING...]-- 过滤分组的记录必须满足的次要条件
    [ORDER BY...]-- 指定查询记录按一个或多个条件排序
    [LIMIT {[offset,]row_count | row_countOFFSET offset}];            -- 指定查询的记录从哪条到哪条
```

**注意：[]括号代表可选的，{}括号代表必选的**

#### 4.3、where条件子句

作用：检索数据中**符合条件**的值

搜索的条件由一个或多个表达式组成！结果布尔值

> 逻辑运算符

| 运算符  | 语法            | 描述   |
| ------- | --------------- | ------ |
| and &&  | a and b a&&b    | 逻辑与 |
| or \|\| | a or b a \|\| b | 逻辑或 |
| Not !   | not a !a        | 逻辑非 |

**尽量使用英文字母**

```
-- where子句
select `studentno`,`studentresult` from result
where `studentresult` <=100  and `studentresult` >= 95

select `studentno`,`studentresult` from result
where `studentresult` <= 100 && `studentresult` >= 95

-- 模糊查询（区间）
select `studentno`,`studentresult` from result
where `studentresult`  between 95  and 100

--  !=  not
select `studentno`,`studentresult` from result
where `studentno` != 1000

select `studentno`,`studentresult` from result
where  not `studentno` = 1000
```

> 模糊查询：比较运算符

| 运算符      | 语法              | 描述                                     |
| ----------- | ----------------- | ---------------------------------------- |
| IS NULL     | a is null         | 如果操作符为NULL，结果为真               |
| IS NOT NULL | a is not null     | 如果操作符不为NULL，结果为真             |
| BETWEEN AND | a between b and c | 若a在b和c之间，结果为真                  |
| **Like**    | a like b          | sql匹配，如果a匹配b，则结果为真          |
| **In**      | a in (a1,a2,a3…)  | 假设a在a1，或者a2…其中的一个值，结果为真 |

```
-- 模糊查询
-- like  结合 %(代表0到任意个字符)   _(一个字符)
-- 查询姓张的同学
select `studentno`,`studentname` from `student`
where `studentname` like '张%'

-- 查询姓张的同学，后面只有一个字
select `studentno`,`studentname` from `student`
where `studentname` like '张_'

-- 查询姓张的同学，后面只有一个字
select `studentno`,`studentname` from `student`
where `studentname` like '张_'

-- 查询姓张的同学，后面有两个字
select `studentno`,`studentname` from `student`
where `studentname` like '张__'

-- 查询名字里有伟的同学
select `studentno`,`studentname` from `student`
where `studentname` like '%伟%'

-- IN(具体的一个或多个值)
select `studentno`,`studentname` from `student`
where `studentno` in (1001,1002)

select `studentno`,`studentname`,`address` from `student`
where `address` in ('江苏南京','广东深圳')

-- is NULL  和  IS NOT  NULL
select `studentno`,`studentname` FROM `student`
where `borndate` is NULL

select `studentno`,`studentname` FROM `student`
where `borndate` is not null
```

#### 4.4、联表查询

> JOIN 对比

![img](https://i.loli.net/2020/11/12/H19EUQvZ73wPCMs.png)

![img](https://i.loli.net/2020/11/12/Nt9Xdvzol6nLj4B.jpg)

```
-- INNER JOIN
select s.`studentno`, `studentname`,`studentresult`
from  `student` as s
INNER join `result` as r
on s.`studentno` = r.`studentno`

-- LEFT JOIN
select s.`studentno`, `studentname`,`studentresult`
from  `student` as s
left join `result` as r
on s.`studentno` = r.`studentno`

-- RIGHT JOIN
SELECT s.`studentno`, `studentname`,`studentresult`
FROM  `student` AS s
right JOIN `result` AS r
on s.`studentno` = r.`studentno`
```

**SQL JOIN中ON和WHERE有什么区别？**
https://www.runoob.com/w3cnote/sql-join-the-different-of-on-and-where.html

| 操作       | 描述                                       |
| ---------- | ------------------------------------------ |
| INNER JOIN | 如果表中至少有一个匹配，就返回行           |
| LEFT JOIN  | 会从左表中返回所有的值，即使右表中没有匹配 |
| RIGHT JOIN | 会从右表中返回所有的值，即使左表中没有匹配 |

```
-- JOIN（连接的表） ON  判断的条件   连接查询
-- WHERE  等值查询
SELECT s.`studentno`, `studentname`,`studentresult`
FROM  `student` AS s
LEFT JOIN `result` AS r
ON s.`studentno` = r.`studentno`
where `studentresult` is NULL
```

思路：

1、分析需求，分析查询的字段来自那些表

2、确定使用哪种连接查询？ 7种

确定交叉点：这两张表种哪些数据是相同的

判断的条件：学生表中的 studentNo = 成绩表 studentNo

***三表（多表）查询\***

```
-- 三表查询
SELECT s.`studentno`, `studentname`, `subjectname`, `studentresult`
FROM `student` AS s
LEFT JOIN `result` AS r
ON s.`studentno` = r.`studentno` 
INNER JOIN `subject` AS sub
ON r.`subjectno` = sub.`subjectno`
```

> 自连接

自己的表和自己的表连接，核心：**一张表拆成两张表即可**

父类：

| categoryid | categoryname |
| ---------- | ------------ |
| 2          | 信息技术     |
| 3          | 软件开发     |
| 5          | 美术设计     |

子类：

| pid  | categoryid | categoryname |
| ---- | ---------- | ------------ |
| 3    | 4          | 数据库       |
| 2    | 8          | 办公信息     |
| 3    | 6          | web开发      |
| 5    | 7          | ps技术       |

操作：查询父类对应的子类关系

| 父类     | 子类     |
| -------- | -------- |
| 信息技术 | 办公信息 |
| 软件开发 | 数据库   |
| 软件开发 | web开发  |
| 美术设计 | ps技术   |

```
-- 查询父类对应的子类关系
SELECT a.`categoryname`,b.`categoryname`
FROM `category` AS a, `category` AS b
WHERE a.`categoryid` = b.`pid`
```

#### 4.5、分页排序

> 排序

```
-- order by   升序
SELECT `studentno`, `studentresult`
FROM `result`
ORDER BY `studentresult` ASC
-- order by    降序
SELECT `studentno`, `studentresult`
FROM `result`
ORDER BY `studentresult` DESC
```

> 分页

```
-- 分页
-- 语法：limit 查询起始下标   页面大小
-- 第N页  limit 0,5     (n-1)*pageSize, pageSize
-- 【pageSize:页面大小】
-- 【(n-1)*pageSize：起始值】
-- 【n：当前页】
-- 【数据总数/页面大小 = 总页数】

SELECT `studentno`, `studentresult`
FROM `result`
ORDER BY `studentresult` DESC
LIMIT 0,5

SELECT `studentno`, `studentresult`
FROM `result`
ORDER BY `studentresult` DESC
LIMIT 1,5
```

#### 4.6、子查询

where（这个值是计算出来的）

本质：**在where语句中嵌套i一个子查询语句**

```
-- 查询课程为高等数学-1 且分数不小于80的同学学号和姓名
-- 方式一：联表查询
SELECT DISTINCT s.`studentno`, `studentname`
FROM student AS s
INNER JOIN result AS r
ON s.`studentno` = r.`studentno`
INNER JOIN `subject` AS sub
ON sub.`subjectno` = r.`subjectno`
WHERE `studentresult`>=80 AND `subjectname` = '高等数学-1'

 
-- 方式二：子查询+联表查询
SELECT DISTINCT s.`studentno`, `studentname`
FROM student AS s
INNER JOIN result AS r
ON s.`studentno` = r.`studentno`
WHERE `studentresult`>=80 AND `subjectno` IN(
	SELECT `subjectno` FROM `subject`
	WHERE `subjectname` = '高等数学-1'
)

-- 方式三：子查询
SELECT DISTINCT s.`studentno`, `studentname` FROM student AS s WHERE `studentno` IN (
   SELECT `studentno` FROM result AS r  WHERE `studentresult` > 80 AND `subjectno` IN (
       SELECT `subjectno` FROM `subject` WHERE `subjectname` = '高等数学-1'
   )
)
```

#### 4.7、分组和过滤

```
-- 查询不同课程的平均分，最高分，最低分，平均分大于80

SELECT r.`subjectno`, `subjectname`,AVG(`studentresult`),MAX(`studentresult`),MIN(`studentresult`)
FROM result AS r
INNER JOIN `subject` AS sub
ON sub.`subjectno` = r.`subjectno`
GROUP BY `subjectno`
HAVING AVG(`studentresult`)>80
```

### 5、MySQL常用函数

官网：https://dev.mysql.com/doc/refman/5.7/en/sql-function-reference.html

#### 5.1、常用函数

![img](https://i.loli.net/2020/11/14/3aWLhnxHYEXJIue.png)

![img](https://i.loli.net/2020/11/14/1NULFkhrnT8OQ74.png)

![img](https://i.loli.net/2020/11/14/cJGqDTnKB7LNh4C.png)

```
SELECT VERSION() -- MySQL版本
```

说明一下：**INSERT(s1,x,len,s2)字符串 s2 替换 s1 的 x 位置开始长度为 len 的字符串**

**SUBSTR(s, start, length)从字符串 s 的 start 位置截取长度为 length 的子字符串**

#### 5.2、聚合函数（常用）

![img](https://i.loli.net/2020/11/14/tfahjRmypJOHYGz.png)

#### 5.3、数据库级别的MD5加密（扩展）

```
-- 测试MD5加密---
CREATE TABLE IF NOT EXISTS `testmd5`(
  `id` INT(2) NOT NULL,
  `username` VARCHAR(100) NOT NULL,
  `pwd` VARCHAR(100) NOT NULL,
  PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

INSERT INTO `testmd5`
VALUES(1, '张三', '123456'),
(2, '李四', '123456'),
(3, '王五', '123456')

-- 加密
UPDATE `testmd5` SET pwd = MD5(pwd) 
WHERE id=1

-- 校对
SELECT * FROM `testmd5`
WHERE `username` = '张三'  AND pwd = MD5('123456')-- username和123456:前端传来的数据
```

### 6、事务

#### 6.1、什么是事务

***要么都成功，要么都失败\***

------

1、SQL执行 A给B转账 A1000 —–>200 B200

2、SQL执行 B收到A的钱 A800 –> B400

------

将一组SQL放在一个批次中去执行~

> 事务原则：ACID原则 原子性，一致性，隔离性，持久性 （脏读，幻读…）

参考博客链接：https://blog.csdn.net/dengjili/article/details/82468576

**原子性（Atomicity）**

要么都成功，要么都失败

**一致性（Consistency）**

事务前后的数据完整性要保证一致，1000

**隔离性（Isolation）**

事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，多个并发事务之间要相互隔离。

**持久性（Durability）**

事务一旦提交则不可逆，被持久化到数据库中！

> 隔离所导致的一些问题

**脏读：**

指一个事务读取了另外一个事务未提交的数据。

**不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）

**虚读(幻读)**：

是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致。
（一般是行影响，多了一行）

> 执行事务

```
-- mysql 是默认开启事务自动提交的
SET autocommit = 0 -- 关闭自动提交
SET autocommit = 1 -- 开启自动提交

-- 手动处理事务
SET autocommit = 0; -- 关闭自动提交

-- 事务开启
START TRANSACTION-- 标记一个事务的开始，在这以后的sql都在同一个事务中


INSERT xx
INSERT xx

-- 提交：持久化（成功~）
COMMIT

-- 回滚：回到原来的样子（失败!）
ROLLBACK

-- 事务结束
SET autocommit = 1; -- 开启自动提交

-- 了解
SAVEPOINT 保存点名 -- 设置一个事务的保存点
ROLLBACK TO SAVEPOINT 保存点名 -- 回滚到保存点
RELEASE SAVEPOINT 保存点名 -- 撤销保存点
```

> 模拟转账

```
CREATE DATABASE shop  CHARACTER SET utf8 COLLATE utf8_general_ci -- 创建一个shop数据库


CREATE TABLE  IF NOT EXISTS account(
  `id` INT(3) NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(10) NOT NULL,
  `money` INT(6) NOT NULL,
  PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8


INSERT INTO `account`(`name`,`money`)
VALUES('A', 1000),
('B', 2000)


SET autocommit = 0 -- 关闭自动提交

START TRANSACTION -- 开启事务

UPDATE `account` SET `money` = `money`+200 WHERE `name` = 'A' -- A减少200元
UPDATE `account` SET `money` = `money`-200 WHERE `name` = 'B' -- B加200元


COMMIT -- 提交
ROLLBACK -- 回滚

SET autocommit = 1; -- 事务结束，开启自动提交
```

### 7、索引

推荐一篇博客http://blog.codinglabs.org/articles/theory-of-mysql-index.html

> MySQL官方对索引的定义为：**索引（Index）是帮助MySQL高效获取数据的数据结构。**0.5s 0.0000001s提取句子主干，就可以得到索引的本质：索引是数据结构。

#### 7.1、索引的分类

> 在一个表中，主键索引只能有一个，唯一索引可以有多个

- 主键索引（PRIMARY KEY）
  - 唯一的标识，主键不可重复，只能有一个列作为主键
- 唯一索引（UNIQUE KEY）
  - 避免重复的列出现，唯一索引可以重复，多个列都可以标识为唯一索引
- 常规索引（KEY/INDEX）
  - 默认的，index/key关键字来设置
- 全文索引（FULLTEXT）
  - 在特定的数据库引擎下才有，MyISAM
  - 快速定位数据

基础语法

```
-- 索引的使用
-- 1、在创建表的时候给字段增加索引
-- 2、创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM student

-- 增加一个全文索引 FULLTEXT
ALTER TABLE school.`student` ADD FULLTEXT INDEX `studentname` (`studentname`)

-- EXPLAIN 分析sql执行的情况
EXPLAIN SELECT * FROM student -- 常规索引，非全文索引

EXPLAIN SELECT * FROM student WHERE MATCH(studentname) AGAINST('刘')
```

#### 7.2、测试索引

索引在小数据量的时候，用处不大，但是在大数据量的时候，区别十分明显~

```
-- 建表
CREATE TABLE `app_user` (
`id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
`name` VARCHAR(50) DEFAULT '',
`eamil` VARCHAR(50) NOT NULL,
`phone` VARCHAR(20) DEFAULT '',
`gender` TINYINT(4) UNSIGNED DEFAULT '0',
`password` VARCHAR(100) NOT NULL DEFAULT '',
`age` TINYINT(4) DEFAULT NULL,
`create_time` DATETIME DEFAULT CURRENT_TIMESTAMP,
`update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8

-- 插入100万条数据
DELIMITER $$-- 写函数之前必须要写，标志
CREATE FUNCTION mockdata()
RETURNS INT
BEGIN
  DECLARE num INT DEFAULT 1000000;
  DECLARE i INT DEFAULT 0;
  WHILE i < num DO
    INSERT INTO app_user(`name`,`email`,`phone`,`gender`,`password`,`age`)
       VALUES(CONCAT('用户',i),'2714332531@qq.com',
       CONCAT('18',FLOOR(RAND()*(999999999-100000000) + 100000000)),
       CEILING(RAND()*2),UUID(),FLOOR(RAND()*100)
       );
    SET i = i + 1;
  END WHILE;
  RETURN i;
END;

SELECT mockdata(); -- 执行函数
SELECT * FROM `app_user` WHERE `name` = '用户9999' --  0.651 sec
EXPLAIN SELECT * FROM `app_user` WHERE `name` = '用户9999' -- 未加索引，查了992285行数据
-- 加上索引
-- id_表名_字段名
-- CREATE INDEX 索引名 ON 表(字段)
CREATE INDEX id_app_user_name ON app_user(`name`)
SELECT * FROM `app_user` WHERE `name` = '用户9999' --  0.002 sec
EXPLAIN SELECT * FROM `app_user` WHERE `name` = '用户9999'-- 加上索引，只查找了1行数据
```

![img](https://i.loli.net/2020/11/16/Ec5AGy3j1pX29Kz.png)

#### 7.3、索引原则

- 索引不是越多越好
- 不要对经常变动数据加索引
- 小数据量的表不需要加索引
- 索引一般加在常用来查询的字段上！

> 索引的数据结构

Hash类型的索引

Btree：InnoDB的默认数据结构~

阅读MySQL索引背后的数据结构及算法原理： http://blog.codinglabs.org/articles/theory-of-mysql-index.html

— 业务级别 MySQL学习

— 运维级别 MySQL学习

### 8、权限管理和备份

#### 8.1、用户管理

> SQL yog可视化管理

![img](https://i.loli.net/2020/11/16/1ZvFuRf6qONbMg3.png)

![img](https://i.loli.net/2020/11/16/7FQStl2YMGhzaKI.png)

> SQL命令操作

用户表：mysql.user

本质：对这张表进行增删改查

```
-- 创建用户 create user 用户名 identified by '密码'
create user wyqian identified by '123456'

-- 修改密码（修改当前用户密码）
set password = password('111111')

-- 修改密码（修改指定用户密码）
set password for wyqian = password('123456')

-- 重命名 rename user 原来的名字 to 新的名字
rename user wyqian to wyqian2

-- 用户授权  ALL PRIVILEGES  全部的权限， 库.表
-- ALL PRIVILEGES 除了给别人授权，其他都能干
grant all privileges on *.* to wyqian2


-- 查询权限
show grants for wyqian2 -- 查看指定用户的权限  -- 结果：GRANT ALL PRIVILEGES ON *.* TO 'wyqian2'@'%'
show grants for root@localhost 

-- root用户权限：GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION

-- 撤销权限  REVOKE 哪些权限 ,在哪个库.表撤销，给谁撤销
revoke ALL privileges on *.* from wyqian2

-- 删除用户
drop user wyqian2
```

#### 8.2、MySQL备份

为什么要备份：

- 保证重要的数据不丢失
- 数据转移 A—->B

MySQL数据库备份的方式

- 直接拷贝物理文件（data文件夹）

- 在SQL yog这种可视化工具中手动导出

  - 在想要导出的表或者库中，右键，选择备份或导出

    ![img](https://i.loli.net/2020/11/16/Ep1cZgXDAlVoUTY.png)

- 使用命令行导出 mysqldump 命令行使用

```
-- 导出：mysqldump -h主机 -u用户名 -p密码 库名 表名 >物理磁盘的位置
mysqldump -hlocalhost -uroot -p123456 school student >D:/a.sql -- 导出一张表
mysqldump -hlocalhost -uroot -p123456 school student result >D:/c.sql -- 导出多张表
mysqldump -hlocalhost -uroot -p123456 school student >D:/c.sql -- 导出数据库
-- 导入：首先使用use 数据库名 切换到特定数据库下，然后使用: source 备份文件 导入即可
source d:/a.sql

mysql -u用户名 -p密码 库名< 备份文件 -- 这种方式也可，但是不推荐使用
```

假设你要备份数据库，防止数据丢失。

把数据库给朋友，sql文件给别人即可

### 9、规范数据库设计

#### 9.1、为什么需要设计

***当数据库比较复杂的时候，我们就需要设计了\***

**糟糕的数据库设计：**

- 数据冗余，浪费空间
- 数据插入和删除都会麻烦、异常【屏蔽使用物理外键】
- 程序的性能差

**良好的数据库设计：**

- 节省内存空间
- 保证数据库的完整性
- 方便我们开发系统

**软件开发中，关于数据库的设计**

- 分析需求：分析业务和需要处理的数据库的需求
- 概要设计：设计关系图 E-R图

**设计数据库的步骤：（个人博客）**

- 收集信息，分析需求
  - 用户表（用户登陆注销，用户的个人信息，写博客，创建分类）
  - 分类表（文章分类，谁创建的）
  - 文章表（文章的信息）
  - 评论表
  - 友链表（友链信息）
  - 自定义表（系统信息，某个关键的字，或者一些主字段） key:value
  - 说说表（发表心情…id…content…create_time）
- 标识实体（把需求落地到每个字段）
- 标识实体之间的关系
  - 写博客：user–>blog
  - 创建分类：user–>category
  - 关注：user–>user
  - 友链：links
  - 评论：user-user-blog

#### 9.2、三大范式

**为什么需要数据规范化？**

- 信息重复
- 更新异常
- 插入异常
  - 无法正常显示信息
- 删除异常
  - 丢失有效的信息

> 三大范式（了解）

**第一范式（1NF）**

原子性：保证每一列不可再分

**第二范式（2NF）**

前提：满足第一范式

每张表只描述一件事情

**第三范式（3NF）**

前提：满足第一和第二范式

第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。

（规范数据库的设计）

**规范性和性能的问题**

关联查询的表不得超过三张表

- 考虑商业化的需求和目标，（成本和用户体验！）数据库的性能更加重要
- 在规范性能的问题的时候，需要适当地考虑一下规范性！
- 故意给某些表增加一些冗余的字段。（从多表查询变为单表查询）
- 故意增加一些计算列。（从大数据量降低为小数据量的查询：索引）

### 10、JDBC（重点）

#### 10.1、数据库驱动

驱动：声卡、显卡、数据库

![img](https://i.loli.net/2020/11/16/TZP1x3SsaR2e5Kb.png)

我们的程序会通过数据库驱动，和数据库打交道！

#### 10.2、JDBC

SUN公司为了简化开发人员的（对数据库的统一）操作，提供了一个（Java操作数据库的）规范 俗称 JDBC

这些规范的实现由具体的厂商去做~

对于开发人员来说，我们只需要掌握JDBC接口的操作即可！

![img](https://i.loli.net/2020/11/16/5n6fHv1gSuO8byK.png)

java.sql

javax.sql

还需要导入一个数据库驱动包 mysql-connector-java-5.1.47.jar

#### 10.3、第一个JDBC程序

> 创建测试数据库

```
CREATE DATABASE jdbcStudy CHARACTER SET utf8 COLLATE utf8_general_ci;

USE jdbcStudy;

CREATE TABLE `users`(
	id INT PRIMARY KEY,
	NAME VARCHAR(40),
	PASSWORD VARCHAR(40),
	email VARCHAR(60),
	birthday DATE
);

INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)
VALUES(1,'zhansan','123456','zs@sina.com','1980-12-04'),
(2,'lisi','123456','lisi@sina.com','1981-12-04'),
(3,'wangwu','123456','wangwu@sina.com','1979-12-04')
```

1、创建一个普通项目

2、导入数据库驱动

导入.jar包的步骤：首先在项目目录下建立lib目录，然后直接将jar包复制粘贴到lib目录下，然后右键lib目录，点击add aslibrary即可

3、编写测试代码

```
package com.kuangshen.lesson01;

import java.sql.*;

public class JdbcFirstDemo {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");//该条语句没有返回值的话，就会执行Driver类中的静态代码块

        //2.用户信息和url
        //useUnicode=true&characterEncoding=utf8&useSSL=true
        String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";
        String username = "root";
        String password = "123456";

        //3.连接成功，数据库对象，Connection代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //4.执行SQL的对象 Statement  执行SQL的对象
        Statement statement = connection.createStatement();

        //5.执行SQL对象，去执行SQL，可能存在结果，查看返回结果
        String sql = "SELECT * FROM users";

        ResultSet resultSet = statement.executeQuery(sql);//返回的结果集，结果集中封装了我们所有的查询结果
        while (resultSet.next()){
            System.out.println("id=" + resultSet.getObject("id"));
            System.out.println("name=" + resultSet.getObject("NAME"));
            System.out.println("pwd=" + resultSet.getObject("PASSWORD"));
            System.out.println("email=" + resultSet.getObject("email"));
            System.out.println("birthday=" + resultSet.getObject("birthday"));
            System.out.println("======================================");
        }

        //6.释放连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

步骤总结：

1. 加载数据库驱动
2. 连接数据库 DriverManager
3. 获得SQL对象 Statement
4. 获得返回的结果集
5. 释放连接

> DriverManager

```
//DriverManager.registerDriver(new Driver());
        Class.forName("com.mysql.jdbc.Driver");//该条语句没有返回值的话，就会执行Driver类中的静态代码块

//connection   代表数据库
//事务
//设置自动提交
connection.setAutoCommit();
//提交
connection.commit();
//回滚
connection.rollback();
```

> URL

```
String url = "jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true";

//mysql-- 3306
//jdbc:mysql://主机地址:端口号/数据库名?参数1&参数2&参数3

//oracle-- 1521
//jdbc:mysql:thin:@localhost:1521:sid
```

> Statement执行SQL的对象 PrepareStatement执行SQL的对象

```
String sql = "SELECT * FROM users";

statement.executeQuery();//执行查询语句,返回ResultSet对象
statement.execute();//执行任何SQL
statement.executeUpdate();//更新、删除、插入都是用这一个方法，返回一个受影响的行数
```

> ResultSet查询的结果集：封装了所有的查询结果

获得指定的数据类型

```
resultSet.getObject();//如果不知道字段类型
//知道字段的类型的话，用下面这些
resultSet.getInt();
resultSet.getString();
resultSet.getDate();
resultSet.getBigDecimal();
......
```

遍历，指针

```
resultSet.absolute();//移动到指定行
resultSet.afterLast();//移动到最后面
resultSet.beforeFirst();//移动到最前面
resultSet.next();//移动下一个数据
resultSet.previous();//移动到前一个数据
```

> 释放资源

```
//6.释放连接
resultSet.close();
statement.close();
connection.close();//耗资源，用完关掉！
```

#### 10.4、statement对象

**jdbc中的statement对象用于向数据库发送SQL语句，像完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可。**

Statement对象的excuteUpdate方法，用于向数据库发送增、删、改的sql语句，excuteUpdate执行完后，将会返回一个整数（即增删改语句导致了数据库几行语句发生了变化）。

Statement.executeQuery()方法用汉语向数据库发送查询语句，executeQuery方法返回代表查询结果的ResultSet对象。

> CRUD操作-create

使用excuteUpdate(String sql)方法完成数据添加操作，示例操作：

```
Statement statement = connection.createStatement();
String sql = "insert into juser(...) values(...)";
int num = statement.executeUpdate(sql);
if(num>0){
    System.out.println("插入成功！");
}
```

> CRUD操作-delete

使用excuteUpdate(String sql)方法完成数据删除操作，示例操作：

```
Statement statement = connection.createStatement();
String sql = "delete from user where id=1";
int num = statement.executeUpdate(sql);
if(num>0){
    System.out.println("删除成功！");
}
```

> CRUD操作-update

使用excuteUpdate(String sql)方法完成数据修改操作，示例操作：

```
Statement statement = connection.createStatement();
String sql = "update user set name='' where name=''";
int num = statement.executeUpdate(sql);
if(num>0){
    System.out.println("修改成功！");
}
```

> CRUD操作-read

使用excuteQuery(String sql)方法完成数据修改操作，示例操作：

```
Statement statement = connection.createStatement();
String sql = "select * from user where id=1";
ResultSet rs = statement.executeQuery(sql);
while(rs.next()){
    //根据获取列的数据类型，分别调用rs的相应方法映射到java对象中
}
```

> 代码实现

1、提取工具类

```
package com.kuangshen.lesson02.utils;

import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

public class JdbcUtils {

    private static String driver = null;
    private static String url = null;
    private static String username = null;
    private static String password = null;

    static {
        try{
            InputStream in = JdbcUtils.class.getClassLoader().getResourceAsStream("db.properties");
            Properties properties = new Properties();
            properties.load(in);

            driver = properties.getProperty("driver");
            url = properties.getProperty("url");
            username = properties.getProperty("username");
            password = properties.getProperty("password");

            //1、加载驱动,驱动只用加载一次
            Class.forName(driver);
        }catch (Exception e){
            e.printStackTrace();
        }
    }

    //获取连接
    public static Connection getConnection() throws SQLException {
        Connection conn = DriverManager.getConnection(url, username, password);
        return conn;
    }
    //释放连接
    public static void releaseConnection(Connection conn, Statement st, ResultSet rs){
        if(rs != null){
            try {
                rs.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        if(st != null){
            try {
                st.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        if(conn != null) {
            try {
                conn.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
    }
}

//db.properties
driver = com.mysql.jdbc.Driver
url = jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true
username = root
password = 123456
```

2、Insert **executeUpdate**

```
package com.kuangshen.lesson02;

import com.kuangshen.lesson02.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestInsert {
    public static void main(String[] args) {

        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获得执行SQL的对象
            st = conn.createStatement();

            //定义一个sql语句
            String sql = "INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)" +
                    "VALUES(4,'wwyqian','123456','wyqian@sina.com','1998-12-04')";

            //执行插入语句
            int num = st.executeUpdate(sql);
            if(num > 0){
                System.out.println("插入成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放资源
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

3、delete **executeUpdate**

```
package com.kuangshen.lesson02;

import com.kuangshen.lesson02.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestDelete {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;


        try {
            //获取连接
            conn = JdbcUtils.getConnection();

            //获取执行sql的对象
            st = conn.createStatement();

            //定义一条sql删除语句
            String sql = "delete from users where NAME='wyqian'";

            //执行sql语句
            int num = st.executeUpdate(sql);//返回受影响的行数

            if(num > 0){
                System.out.println("删除成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

4、Update **executeUpdate**

```
package com.kuangshen.lesson02;

import com.kuangshen.lesson02.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestUpdate {
    public static void main(String[] args) {

        Connection conn = null;
        Statement st = null;
        ResultSet rs =  null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获取执行SQL的对象
            st = conn.createStatement();
            //定义一条SQL更新语句
            String sql = "update users set `NAme` = 'wyqian' where id=3";

            //执行SQL语句
            int i = st.executeUpdate(sql);

            if(i > 0){
                System.out.println("更新成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }

    }
}
```

5、查询 **executeQuery**

```
package com.kuangshen.lesson02;

import com.kuangshen.lesson02.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestQuery {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();

            //获取执行SQL的对象
            st = conn.createStatement();

            //定义一条SQL查询语句
            String sql = "select * from users where id=1";

            //执行SQL语句
            rs = st.executeQuery(sql);//查询完毕会返回一个结果集

            while(rs.next()){
                System.out.println("id=" + rs.getInt("id"));
                System.out.println("name=" + rs.getString("NAME"));
                System.out.println("pwd=" + rs.getString("PASSWORD"));
                System.out.println("email=" + rs.getString("email"));
                System.out.println("birthday=" + rs.getDate("birthday"));
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放连接
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

> SQL注入的问题

sql存在漏洞，会被攻击导致数据泄露，**SQL会被拼接 or**

```
package com.kuangshen.lesson02;

import com.kuangshen.lesson02.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestSQL注入 {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获取执行SQL的对象
            st = conn.createStatement();

            //写一条sql语句
            //执行SQL语句
            rs = st.executeQuery(login("' or '1=1", "123456"));
            while(rs.next()){
                System.out.println("name=" + rs.getString("NAME"));
                System.out.println("pwd=" + rs.getString("PASSWORD"));
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放连接
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }

    public static String login(String username, String pwd){
        String sql = "select * from users where NAME = '"+ username + "' and " + "PASSWORD" + "='" + pwd + "'";
        return sql;
    }
}
```

#### 10.5、PreparedStatement对象

PreparedStatement可以防止SQL注入，效率更好！

1、新增

```
package com.kuangshen.lesson03;

import com.kuangshen.lesson03.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestInsert {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs= null;


        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获得执行SQL的对象,预编译一条sql,?代表占位符
            String sql = "Insert into `users` (`id`,`NAME`,`PASSWORD`) values(?,?,?)";
            st = conn.prepareStatement(sql);
            //设置SQl里面的参数
            st.setInt(1, 5);
            st.setString(2, "NJU");
            st.setString(3, "123456");

            //执行SQl
            int i = st.executeUpdate();
            if(i > 0){
                System.out.println("添加成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

2、删除

```
package com.kuangshen.lesson03;

import com.kuangshen.lesson03.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestDelete {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs= null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获得执行SQL的对象，预编译一条SQl语句
            String sql ="delete from users where id = ?";
            st = conn.prepareStatement(sql);

            //设置SQL语句中的？参数
            st.setInt(1,5);

            //执行SQl语句
            int i = st.executeUpdate();
            if(i > 0){
                System.out.println("删除成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

3、更新

```
package com.kuangshen.lesson03;

import com.kuangshen.lesson03.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestUpdate {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获得执行SQl的对象，需要预编译一条SQL
            String sql = "update `users` set `NAME` = ? where id = ?";
            st = conn.prepareStatement(sql);
            //设置sql中？参数
            st.setString(1, "wjyyyyyy");
            st.setInt(2, 3);
            //执行sql语句
            int i = st.executeUpdate();
            if(i > 0){
                System.out.println("更新成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st,rs);
        }
    }
}
```

4、查询

```
package com.kuangshen.lesson03;

import com.kuangshen.lesson03.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestSelect {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //获得执行SQL的对象，需要预编译一条SQl语句
            String sql = "select * from `users` where id = ?";

            st = conn.prepareStatement(sql);

            //设置SQl语句中？参数
            st.setInt(1,1);

            //执行SQl语句
            rs = st.executeQuery();

            //打印出查询到的信息
            while(rs.next()){
                System.out.println("name=" + rs.getString("NAME"));
                System.out.println("pwd=" + rs.getString("PASSWORD"));
            }

        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }

}
```

5、防止SQL注入

```
package com.kuangshen.lesson03;

import com.kuangshen.lesson03.utils.JdbcUtils;

import java.sql.*;

public class TestSQL注入 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();


            //写一条sql语句
            //获取执行SQL的对象
            String sql = "select * from users where `NAME` = ? and PASSWORD = ?";

            st = conn.prepareStatement(sql);
            //设置SQl？参数
            st.setString(1, "'' or 1=1");
            st.setString(2, "123456");

            //执行Sql语句
            rs = st.executeQuery();
            while(rs.next()){
                System.out.println("name=" + rs.getString("NAME"));
                System.out.println("pwd=" + rs.getString("PASSWORD"));
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放连接
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }

    public static String login(String username, String pwd){
        String sql = "select * from users where NAME = ? and PASSWORD = ?";
        return sql;
    }
}
```

#### 10.6、使用IDEA连接数据库

![img](https://i.loli.net/2020/11/17/m8uTZN4prlhz3Va.png)

#### 10.8、事务

**要么都成功，要么都失败**

> ACID原则

原子性：要么都完成，要么都不完成

一致性：总数不变

**隔离性：多个进程互不干扰**

持久性：一旦提交不可逆，持久化到数据库了

隔离性的问题：

脏读：一个事务读取了另一个事务没有提交的事务。

不可重复读：在同一事务内，重复读取表中的数据，表数据发生了改变。

虚读（幻读）：在同一事务内，读取到了别人插入的数据，导致前后读出来的结果不一致。

> 代码实现

***事务提交成功\***

```
package com.kuangshen.lesson04;

import com.kuangshen.lesson04.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestTransaction {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //关闭数据库的自动提交，开启事务
            conn.setAutoCommit(false);

            //获得执行SQL语句的对象并且需要预编译一条SQL
            String sql1 = "update `account` set money=money-100 where id=?";
            st = conn.prepareStatement(sql1);
            st.setInt(1,1);//设置SQl语句中？参数
            st.executeUpdate();

            String sql2 = "update `account` set money=money+100 where id=?";
            st = conn.prepareStatement(sql2);
            st.setInt(1,2);
            st.executeUpdate();

            //提交
            conn.commit();
            System.out.println("提交成功！");
        } catch (SQLException throwables) {
            //如果失败，就回滚(其实不写也可以，提交失败会默认回滚)
            try {
                conn.rollback();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

***事务提交失败\***

```
package com.kuangshen.lesson04;

import com.kuangshen.lesson04.utils.JdbcUtils;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class TestTransaction {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = JdbcUtils.getConnection();
            //关闭数据库的自动提交，开启事务
            conn.setAutoCommit(false);

            //获得执行SQL语句的对象并且需要预编译一条SQL
            String sql1 = "update `account` set money=money-100 where id=?";
            st = conn.prepareStatement(sql1);
            st.setInt(1,1);//设置SQl语句中？参数
            st.executeUpdate();

            //故意设置事务失败
            int x = 1/0;//这是一条一定会报错的语句

            String sql2 = "update `account` set money=money+100 where id=?";
            st = conn.prepareStatement(sql2);
            st.setInt(1,2);
            st.executeUpdate();

            //提交
            conn.commit();
            System.out.println("提交成功！");
        } catch (SQLException throwables) {
            //如果失败，就回滚(其实不写也可以，提交失败会默认回滚)
            try {
                System.out.println("事务提交失败，数据库回滚");
                conn.rollback();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            throwables.printStackTrace();
        }finally {
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

#### 10.9、数据库连接池

数据库连接–执行完毕–释放

连接–释放 十分浪费系统资源

**池化技术：准备一些预先的资源，过来就连接预先准备好的**

最小连接数：10

最大连接数：15

等待超时：100ms

编写连接池 实现一个接口 DataSource

> 开源数据源实现(拿来即用)

DBCP

C3P0

Druid：阿里巴巴

使用这些数据库连接池之后，我们在项目开发中就不需要再编写连接数据库的代码了！

> DBCP

需要用到的jar包：

commons-dbcp-1.4、commons-pool-1.6

**dbcpconfig.properties**

```
#连接设置
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/jdbcstudy?useUnicode=true&characterEncoding=utf8&useSSL=true
username=root
password=123456

#<!-- 初始化连接 -->
initialSize=10

#最大连接数量
maxActive=50

#<!-- 最大空闲连接 -->
maxIdle=20

#<!-- 最小空闲连接 -->
minIdle=5

#<!-- 超时等待时间以毫秒为单位 6000毫秒/1000等于60秒 -->
maxWait=60000
#JDBC驱动建立连接时附带的连接属性属性的格式必须为这样：【属性名=property;】
#注意："user" 与 "password" 两个属性会被明确地传递，因此这里不需要包含他们。
connectionProperties=useUnicode=true;characterEncoding=UTF8

#指定由连接池所创建的连接的自动提交（auto-commit）状态。
defaultAutoCommit=true

#driver default 指定由连接池所创建的连接的只读（read-only）状态。
#如果没有设置该值，则“setReadOnly”方法将不被调用。（某些驱动并不支持只读模式，如：Informix）
defaultReadOnly=

#driver default 指定由连接池所创建的连接的事务级别（TransactionIsolation）。
#可用值为下列之一：（详情可见javadoc。）NONE,READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE
defaultTransactionIsolation=READ_UNCOMMITTED
```

**修改工具类**

```
package com.kuangshen.lesson05;

import com.kuangshen.lesson02.utils.JdbcUtils;
import com.kuangshen.lesson05.utils.DbcpUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestDbcp {
    public static void main(String[] args) {

        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = DbcpUtils.getConnection();
            //获得执行SQL的对象
            st = conn.createStatement();

            //定义一个sql语句
            String sql = "INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)" +
                    "VALUES(4,'wk','123456','wk@sina.com','1998-12-07')";

            //执行插入语句
            int num = st.executeUpdate(sql);
            if(num > 0){
                System.out.println("插入成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放资源
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

**测试添加一条数据到users表**

```
package com.kuangshen.lesson05;

import com.kuangshen.lesson02.utils.JdbcUtils;
import com.kuangshen.lesson05.utils.DbcpUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestDbcp {
    public static void main(String[] args) {

        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = DbcpUtils.getConnection();
            //获得执行SQL的对象
            st = conn.createStatement();

            //定义一个sql语句
            String sql = "INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)" +
                    "VALUES(4,'wk','123456','wk@sina.com','1998-12-07')";

            //执行插入语句
            int num = st.executeUpdate(sql);
            if(num > 0){
                System.out.println("插入成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放资源
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

> C3P0

需要用到的jar包：

c3p0-0.9.5.5、mcahnge-commons-java-0.2.19

无论使用什么数据源

本质还是一样的，DataSource接口不会变，方法就不会变！

**xml文件**

```
<?xml version="1.0" encoding="UTF-8"?>
<c3p0-config>
    <!--
c3p0的缺省（默认）配置
如果在代码中"ComboPooledDataSource ds=new ComboPooledDataSource();"这样写就表示使用的是c3p0的缺省（默认）-->
    <default-config>
        <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbcstudy?userUnicode=true&amp;characterEncoding=utf8&amp;uesSSL=true&amp;serverTimezone=UTC</property>
        <property name="user">root</property>
        <property name="password">123456</property>

        <property name="acquiredIncrement">5</property>
        <property name="initialPoolSize">10</property>
        <property name="minPoolSize">5</property>
        <property name="maxPoolSize">20</property>
    </default-config>
</c3p0-config>
```

**工具类**

```
package com.kuangshen.lesson05.utils;

import com.mchange.v2.c3p0.ComboPooledDataSource;
import org.apache.commons.dbcp.BasicDataSourceFactory;

import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

public class C3p0Utils {

    private static ComboPooledDataSource dataSource = null;
    static {
        try{
            //代码版配置，不推荐使用
//            dataSource = new ComboPooledDataSource();
//            dataSource.setDriverClass();
//            dataSource.setUser();
//            dataSource.setPassword();
//            dataSource.setJdbcUrl();
//
//            dataSource.setMaxPoolSize();
//            dataSource.setMinPoolSize();

            dataSource = new ComboPooledDataSource();//配置文件写法,xml文件在运行时自动导入
            //初始化对象是会自动读取配置文件中的配置信息，自动连接数据库
        }catch (Exception e){
            e.printStackTrace();
        }
    }

    //获取连接
    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection();//从数据源中获取连接
    }
    //释放连接
    public static void releaseConnection(Connection conn, Statement st, ResultSet rs){
        if(rs != null){
            try {
                rs.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        if(st != null){
            try {
                st.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
        if(conn != null) {
            try {
                conn.close();
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            }
        }
    }
}
```

测试一条插入的SQl语句

```
package com.kuangshen.lesson05;

import com.kuangshen.lesson02.utils.JdbcUtils;
import com.kuangshen.lesson05.utils.C3p0Utils;
import com.kuangshen.lesson05.utils.DbcpUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class TestC3p0 {
    public static void main(String[] args) {

        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;

        try {
            //获取连接
            conn = C3p0Utils.getConnection();
            //获得执行SQL的对象
            st = conn.createStatement();

            //定义一个sql语句
            String sql = "INSERT INTO `users`(id,NAME,PASSWORD,email,birthday)" +
                    "VALUES(5,'xiaoxie','123456','xiaoxie@sina.com','1998-12-07')";

            //执行插入语句
            int num = st.executeUpdate(sql);
            if(num > 0){
                System.out.println("插入成功！");
            }
        } catch (SQLException throwables) {
            throwables.printStackTrace();
        }finally {
            //释放资源
            JdbcUtils.releaseConnection(conn, st, rs);
        }
    }
}
```

Druid，后面会学阿里巴巴的

Apache

![img](https://i.loli.net/2020/11/17/MsAmB2GXP4f1vRl.png)