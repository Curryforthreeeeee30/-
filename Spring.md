# Spring

## 1、Spring

### 1.1、简介

- Spring：春天—>给软件行业带来了春天！
- 2002，首次推出了Spring框架的雏形：*interface21*
- *2004年3月24*日,*Spring*框架以interface21框架为基础,经过重新设计,发布了1.0正式版本。
- **Rod Johnson**，Spring Framework创始人，著名作者。很难想象Rod Johnson的学历，真的让好多人大吃一惊，他是悉尼大学的博士，然而他的专业不是计算机，而是音乐学。
- Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架！
- SSH：Struct2 + Spring + Hibernate
- SSM：SpringMVC + Spring + Mybatis！

官网：https://spring.io/projects/spring-framework#overview

官方下载地址：[http://repo.spring.io/release/org/springframework/spring](https://repo.spring.io/release/org/springframework/spring)

GitHub地址：https://github.com/spring-projects/spring-framework

```
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.2</version>
</dependency>
```

### 1.2、优点

- Spring是一个开源的免费的框架（容器）！
- Spring是一个轻量级的、非入侵式的框架！
- **控制反转（IOC），面向切面编程（AOP）！**
- 支持事务的处理，对框架整合的支持！

***总结：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架！\***

### 1.3、组成

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_204319.png)

### 1.4、扩展

在Spring的官网有这个介绍：现代化的Java开发！说白了就是基于Spring的开发！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-05_204520.png)

- Spring Boot
  - 一个快速开发的脚手架。
  - 基于SpringBoot可以快速的开发单个微服务。
  - 约定大于配置！
- Spring Cloud
  - SpringCloud是基于SpringBoot实现的。

因为现在大多数公司都在使用SpringBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及SpringMVC！承上启下的作用！

**弊端：发展了太久之后，违背了原来的理念，配置十分繁琐，人称：”配置地狱！“**

## 2、IOC理论推导

1.UserDao 接口

2.UserDaoImpl 实现类

3.UserService 业务接口

4.UserServiceImpl 业务实现类

在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改源代码！如果程序代码量十分大，修改一次的成本代价十分昂贵！

我们使用一个set接口实现。已经发生了革命性的变化！

```
private UserDao userDao;

//利用set进行动态实现值的注入！
public void setUserDao(UserDao userDao) {
    this.userDao = userDao;
}
```

- 之前，程序时主动创建对象！控制权在程序员手上！
- 使用了set注入之后，程序不再具有主动性，而是变成了被动地接收对象！

这种思想，从本质上解决了问题，我们程序员不用再去管理对象的创建了。系统的耦合性大大降低！可以更加专注地在业务实现上！这是IOC的原型！

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-06_102022.png)

**控制反转IoC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IoC的一种方法**，也有人认为DI只是IoC的另一种说法。没有IoC的程序中 , 我们使用面向对象编程 , 对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后将对象的创建转移给第三方，个人认为所谓控制反转就是：获得依赖对象的方式反转了。

采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式可以把两者合为一体，Bean的定义信息直接以注解的形式定义在实现类中，从而达到了零配置的目的。

**控制反转是一种通过描述（XML或注解）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是IoC容器，其实现方法是依赖注入（Dependency Injection,DI）。**

## 3、HelloSpring

- Hello对象是谁创建的？

  ***hello对象是由Spring创建的\***

- Hello对象的属性是怎么设置的？

  ***hello对象的属性是由容器创建的\***

这个过程就叫做控制反转：

- 控制：谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，使用Spring后，对象是由Spring来创建
- 反转：程序本身不创建对象，而变成被动的接收对象

依赖注入：就是利用set方法来进行注入的

***IOC是一种编程思想，由主动的编程变成被动的接收\***

可以通过newClassPathXmlApplicationContext去浏览一下底层源码 .

案例：

首先新增一个Spring配置文件：beans.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="mysqlImpl" class="com.wyqian.dao.UserDaoMysqlImpl"/>
    <bean id="oracleImpl" class="com.wyqian.dao.UserDaoOracleImpl"/>

    <bean id="userServiceImpl" class="com.wyqian.service.UserServiceImpl">
        <!--注意: 这里的name并不是属性 , 而是set方法后面的那部分 , 首字母小写-->
        <!--引用另外一个bean , 不是用value 而是用 ref-->
        <!--基本类型用value,引用类型用ref-->
        <property name="userDao" ref="oracleImpl"/>
    </bean>
</beans>
```

测试：

```
@Test
public void getUser2(){
    //获取Spring容器
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

    UserServiceImpl userServiceImpl = (UserServiceImpl) context.getBean("userServiceImpl");
    userServiceImpl.getUser();
}
```

OK , 到了现在 , 我们彻底不用再程序中去改动了 , 要实现不同的操作 , 只需要在xml配置文件中进行修改 , 所谓的IoC,一句话搞定 : 对象由Spring 来创建 , 管理 , 装配 !

## 4、IOC创建对象的方式

1. 使用无参构造创建对象，默认！

   *pojo*

   ```
   package com.wyqian.pojo;
   
   public class User {
       private String name;
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public void show(){
           System.out.println("name:" + name);
       }
   }
   ```

   *beans.xml*

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
       <bean id="user" class="com.wyqian.pojo.User">
           <property name="name" value="钱万云"/>
       </bean>
   </beans>
   ```

2. 假设我们要使用有参构造创建对象

   1. 下标赋值

      *pojo*

      ```
      package com.wyqian.pojo;
      
      public class User {
          private String name;
      
          public User(String name){
              this.name = name;
          }
      
          public String getName() {
              return name;
          }
      
          public void setName(String name) {
              this.name = name;
          }
      
          public void show(){
              System.out.println("name:" + name);
          }
      }
      ```

      *beans.xml*

      ```
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
      <!--    <bean id="user" class="com.wyqian.pojo.User">-->
      <!--        <property name="name" value="钱万云"/>-->
      <!--    </bean>-->
          <bean id="user" class="com.wyqian.pojo.User">
              <!--第一种，下标赋值-->
              <constructor-arg index="0" value="钱万云"/>
          </bean>
      </beans>
      ```

   2. 通过类型创建

      *beans.xml*

      ```
      <!--第二种方式：通过类型创建，不建议使用-->
      <bean id="user" class="com.wyqian.pojo.User">
          <constructor-arg type="java.lang.String" value="钱万云"/>
      </bean>
      ```

   3. 通过参数名来创建

      ```
      <!--第三种方式：直接通过参数名来自置-->
      <bean id="user" class="com.wyqian.pojo.User">
          <constructor-arg name="name" value="钱万云"/>
      </bean>
      ```

总结：在配置文件加载的时候，容器中管理的对象就已经初始化了！

证明上面这句话的一个例子：

*pojo—User类*

```
package com.wyqian.pojo;

public class User {
    private String name;

    public User(String name){
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void show(){
        System.out.println("name:" + name);
    }
}
```

*pojo—UserT类*

```
package com.wyqian.pojo;

public class UserT {
    private String name;

    public UserT(){
        System.out.println("UserT被加载~~~");
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void show(){
        System.out.println("name:" + name);
    }
}
```

*beans.xml*

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--第三种方式：直接通过参数名来自置-->
    <bean id="user" class="com.wyqian.pojo.User">
        <constructor-arg name="name" value="钱万云"/>
    </bean>
    <bean id="userT" class="com.wyqian.pojo.UserT">
        <property name="name" value="钱万云"/>
    </bean>
</beans>
```

*测试*

```
@Test
public void getUser(){
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
    User user = (User) context.getBean("user");
    user.show();
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-07_160517.png)

## 5、Spring配置

### 5.1、别名

```
<!--别名，如果添加了别名，我们也可以通过别名来获取到这个对象-->
<alias name="user" alias="userAlias"/>
```

### 5.2、Bean的配置

```
<!--
    id : bean的唯一标识符，也就是相当于我们学的对象名
    class:bean对象所对应的全限定名：包名+类型
    name:也是别名，而且name可以同时取多个别名
    -->

<bean id="userT2" class="com.wyqian.pojo.UserT" name="u2,usert usert2;userT22">
    <property name="name" value="钱万云呀"/>
</bean>
```

### 5.3、import

这个import，一般用于团队开发使用，它可以将多个配置文件，导入合并为一个

假设，现在项目中有多个人开发，这三个人负责不同的类开发，不同的类需要注册在不同的beans.xml中，我们可以利用import将所有人的beans.xml合并为一个总的！

- 张三

- 李四

- 王五

- applicationContext.xml

  ```
  <import resource="beans.xml"/>
  <import resource="beans2.xml"/>
  <import resource="beans3.xml"/>
  ```

使用的时候，直接使用总的配置就可以了!

## 6、依赖注入

### 6.1、构造器注入

前面已经说过了

### 6.2、Set方式注入【重点】

- 依赖注入：Set注入！
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入！

【环境搭建】

1. 复杂类型

   ```
   public class Address {
       private String address;
   
       public String getAddress() {
           return address;
       }
   
       public void setAddress(String address) {
           this.address = address;
       }
   }
   ```

2. 真实测试对象

   ```
   public class Student {
       private String name;
       private Address address;
       private String[] books;
       private List<String> hobbies;
       private Map<String, String> card;
       private Set<String> games;
       private String wife;
       private Properties info;
   ```

3. beans.xml

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="student" class="com.wyqian.pojo.Student">
           <property name="name" value="钱万云"/>
       </bean>
   </beans>
   ```

4. 测试类

   ```
   import com.wyqian.pojo.Student;
   import org.junit.Test;
   import org.springframework.context.ApplicationContext;
   import org.springframework.context.support.ClassPathXmlApplicationContext;
   
   public class MyTest {
       @Test
       public void getStudent(){
           ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
   
           Student student = (Student) context.getBean("student");
           System.out.println(student.getName());
       }
   }
   ```

   ***完善:\***

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
       <bean id="address" class="com.wyqian.pojo.Address">
           <property name="address" value="南京"/>
       </bean>
   
       <bean id="student" class="com.wyqian.pojo.Student">
           <!--第一种，普通值注入，value-->
           <property name="name" value="钱万云"/>
   <!--
               这种方式也可以
               <property name="name">-->
   <!--            <value>千瓦云</value>-->
   <!--        </property>-->
   
           <!--第二种，Bean注入，ref-->
           <property name="address" ref="address"/>
   
           <!--数组注入，ref-->
           <property name="books">
               <array>
                   <value>红楼梦</value>
                   <value>水浒传</value>
                   <value>西游记</value>
                   <value>三国演义</value>
               </array>
           </property>
   
           <!--List注入-->
           <property name="hobbies">
               <list>
                   <value>唱歌</value>
                   <value>篮球</value>
                   <value>rap</value>
               </list>
           </property>
   
           <!--Map-->
           <property name="card">
               <map>
                   <entry key="身份证" value="123124313"/>
                   <entry key="银行卡" value="fbauisdyfg"/>
               </map>
           </property>
   
           <!--Set-->
           <property name="games">
               <set>
                   <value>LOL</value>
                   <value>BOB</value>
                   <value>COC</value>
               </set>
           </property>
   
           <!--null-->
           <property name="wife">
               <null/>
           </property>
   
           <!--properties-->
           <property name="info">
               <props>
                   <prop key="url">mysql:3306</prop>
                   <prop key="driver">mysql</prop>
                   <prop key="username">root</prop>
                   <prop key="password">1234124</prop>
               </props>
           </property>
        </bean>
   
   <!--    Student{name='钱万云',
           address=Address{address='南京'},
           books=[红楼梦, 水浒传, 西游记, 三国演义],
           hobbies=[唱歌, 篮球, rap],
           card={身份证=123124313, 银行卡=fbauisdyfg},
           games=[LOL, BOB, COC],
           wife='null',
           info={password=1234124, url=mysql:3306, driver=mysql, username=root}}
   -->
   
   </beans>
   ```

### 6.3、扩展方式注入

官网解释：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-07_202459.png)

我们可以使用p命名空间和c命名空间进行注入

***使用！\***

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:c="http://www.springframework.org/schema/c"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--p命名空间注入，可以直接注入属性的值：property-->
    <bean id="user" class="com.wyqian.pojo.User" p:name="钱万云" p:age="23"/>

    <!--c命名空间注入，可以直接注入构造器参数的值：constructor-args-->
    <bean id="user2" class="com.wyqian.pojo.User" c:name="钱万云" c:age="23"/>
</beans>
```

***pojo类\***

```
package com.wyqian.pojo;

public class User {
    private String name;
    private int age;

    public User() {
    }

    public User(String name, int age) {
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
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

***测试\***

```
@Test
public void getUser(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userBeans.xml");

    User user = context.getBean("user2", User.class);
    System.out.println(user);
}
```

注意点：p命名空间和c命名空间不能直接使用，需要导入xml约束！

```
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```

### 6.4、bean的作用域

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-07_202945.png)

1. 单例模式（Spring默认机制）

   ```
   <bean id="user2" class="com.wyqian.pojo.User" c:name="钱万云" c:age="23" scope="singleton"/>
   ```

2. 原型模式：每次从容器中get的时候，都会产生一个新对象！

   ```
   <bean id="user2" class="com.wyqian.pojo.User" c:name="钱万云" c:age="23" scope="prototype"/>
   ```

3. 其余的request、session、application，这些个只能在web开发中才能使用到！

单例模式下的测试代码：

```
@Test
public void getUser(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userBeans.xml");

    User user = context.getBean("user2", User.class);
    User user2 = context.getBean("user2", User.class);
    System.out.println(user==user2);
}
```

## 7、Bean的自动装配

- 自动装配是Spring满足bean依赖的一种方式！
- Spring会在上下文中自动寻找，并自动给bean装配属性！

在Spring中有三种配置的方式

1. 在xml中显示地配置
2. 在java中显示配置
3. 隐式地自动装配bean【重要】

为什么有了1，还要有3呢？—>看下面这个例子，如果按照1的写法去写，那么dog和cat的配置就显得不那么智能，因为people类中为dog的属性本来就要去找id为dog的bean去实现配置，因此自动装配就派上用场了！

### 7.1、测试

环境搭建：一个人有两个宠物！

***pojo—Cat\***

```
package com.wyqian.pojo;

public class Cat {
    public void shout(){
        System.out.println("miao~");
    }
}
```

***pojo—Dog\***

```
package com.wyqian.pojo;

public class Dog {
    public void shout(){
        System.out.println("wang~");
    }
}
```

***pojo—People\***

```
package com.wyqian.pojo;

public class People {
    private String name;
    private Cat cat;
    private Dog dog;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Cat getCat() {
        return cat;
    }

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    public Dog getDog() {
        return dog;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    @Override
    public String toString() {
        return "People{" +
                "name='" + name + '\'' +
                ", cat=" + cat +
                ", dog=" + dog +
                '}';
    }
}
```

### 7.2、ByName自动装配

```
<bean id="cat" class="com.wyqian.pojo.Cat"/>
<bean id="dog" class="com.wyqian.pojo.Dog"/>

<!--byName：会自动在容器上下文查找，和自己对象set方法后面的值对应的beanid~-->
<bean id="people" class="com.wyqian.pojo.People" autowire="byName">
    <property name="name" value="wyqian呀"/>
</bean>
```

### 7.3、ByType自动装配

```
<bean id="cat" class="com.wyqian.pojo.Cat"/>
<bean id="dog" class="com.wyqian.pojo.Dog"/>

<bean id="people" class="com.wyqian.pojo.People" autowire="byType">
    <property name="name" value="wyqian呀"/>
</bean>
<!--byType:会自动在容器上下文中查找，和自己对象属性类型相同的bean!
    所以使用byType的话，上面Dog和Cat的bean的id都可以省略，但是必须保证唯一！也就是不能出现多个Dog或者Cat的bean-->
```

小结：

1. byName的时候，需要保证所有的bean的**id唯一**，并且bean**id**需要和自动注入的属性的**set方法的值**一致！
2. byType的时候，需要保证所有的bean的**class唯一**，并且bean**class**需要和自动注入的**属性的类型**一致！

### 7.4、使用注解实现自动装配

jdk1.5支持的注解，Spring2.5就支持注解了！

```
The introduction of annotation-based configuration raised the question of whether this approach is “better” than XML.
```

要使用注解须知：

1. 导入约束：context 约束
2. ***配置注解的支持：[context:annotation-config/](context:annotation-config/)\***【重要】

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

**@Autowired**

直接在属性上使用即可！也可以在set方法上使用

使用Autowired我们也可以不用编写Set方法了，前提是你这个自动装配的属性在IOC（Spring）容器中存在，默认按byType匹配！

科普：

```
@Nullable   字段标记了这个注解，说明这个字段可以为null
public @interface Autowired {
    boolean required() default true;
}
```

测试代码

```
public class People {
    private String name;
    //如果显式定义了Autowired的required属性为false，说明这个对象可以为null，否则不允许为空
    @Autowired(required = false)
    private Cat cat;
    @Autowired
    private Dog dog;
}
```

如果使用@Autowired自动装配的环境比较复杂，自动装配无法通过【@Autowired】完成的时候，我们可以使用@Qualifier(value = “***”)去配置@Autowired的使用，指定一个唯一的bean对象注入！

```
public class People {
    private String name;

    @Autowired
    private Cat cat;
    @Autowired
    @Qualifier(value = "dog222")
    private Dog dog;
}
<context:annotation-config/>

<bean id="cat" class="com.wyqian.pojo.Cat"/>
<bean id="dog" class="com.wyqian.pojo.Dog"/>
<bean id="dog222" class="com.wyqian.pojo.Dog"/>
<bean id="people" class="com.wyqian.pojo.People"/>
```

**@Resource注解**

```
public class People {
    private String name;

    @Resource
    private Cat cat;

    @Resource(name = "dog111")
    private Dog dog;
}
<context:annotation-config/>

<bean id="cat" class="com.wyqian.pojo.Cat"/>
<bean id="dog111" class="com.wyqian.pojo.Dog"/>
<bean id="dog222" class="com.wyqian.pojo.Dog"/>
<bean id="people" class="com.wyqian.pojo.People"/>
```

小结：

@Resource和@Autowired的区别：

- 都是用来自动装配的，都可以放在属性字段上
- @Autowired默认通过byType的方式实现,，而且必须要求这个对象存在【常用】
- @Resource默认通过byName的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就报错！【常用】
- 执行顺序不同：@Autowired默认通过byType的方式实现，@Resource默认通过byName的方式实现

## 8、使用注解开发

在Spring4之后，要使用注解开发，必须要保证aop的包导入了

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-09_185936.png)

使用注解需要导入context约束，增加注解的支持！

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           ">
    <!--增加注解支持-->
    <context:annotation-config/>
</beans>
```

1、bean

2、属性如何注入

```
//等价于  <bean id="user" class="com.wyqian.pojo.User"/>
// @Component  组件
@Component
public class User {
    @Value("钱万云")//或者在setName方法上加也可以
    public String name;

    @Value("wk")
    public void setName(String name) {
        this.name = name;
    }
}
```

3、衍生的注解

@Component 有几个衍生注解，我们在web开发中，会按照mvc三层架构分层！

- dao【@Repository】
- service【@Service】
- controller【@Controller】

这四个注解功能都是一样的，都是代表将某个类注册到Spring中，装配Bean

4、自动装配

```
@Autowired: 自动装配通过类型。名字
    如果@Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value="***")
@Nullable   字段标记了这个注解，说明这个字段可以为null;
@Resource:  自动装配通过名字。类型
```

5、作用域

```
@Component
@Scope("singleton")
public class User {
    @Value("钱万云")//或者在setName方法上加也可以
    public String name;

    @Value("wk")
    public void setName(String name) {
        this.name = name;
    }
}
```

6、小结

xml与注解：

- xml更加万能，适用于任何场合！维护简单方便
- 注解 不是自己的类使用不了， 维护相对复杂！

xml与注解最佳实践：

- xml用来管理Bean;

- 注解只负责完成属性的注入；

- 我们在使用的过程中，只需要注意一个问题：必须让注解生效，就需要开启注解的支持！

  ```
  <!--指定要扫描包，这个包下的注解就会生效！-->
  <context:component-scan base-package="com.wyqian"/>
  <!--增加注解支持-->
  <context:annotation-config/>
  ```

## 9、使用Java的方式配置Spring

我们现在要完全不使用Spring的xml配置了，全权交给Java来做！

JavaConfig 是Spring的一个子项目，在Spring之后，它成为了一个核心功能！

![image-20210109200714336](https://wyqian.top/2021/01/05/Spring/Spring/H:%5Chexoblog%5Cblog%5Csource_posts%5CSpring%5Cimage-20210109200714336.png)

实体类

```
package com.wyqian.pojo;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
//这里这个注解的意思，就是说这个类被Spring托管了，注册到了容器中
public class User {
    private String name;

    public String getName() {
        return name;
    }

    @Value("钱万云")//属性注入值
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

配置类

```
package com.wyqian.config;

import com.wyqian.pojo.User;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

//这个也会被Spring托管，注册到容器中，因为他本来就是个@Conponent
//@Configuration代表这是一个配置类，就和我们之前看的beans.xml
@Configuration
@ComponentScan("com.wyqian.pojo")
@Import(WyqianConfig2.class)//就像之前一个beans.xml文件导入其他beans.xml文件一样
public class WyqianConfig {

    //注册一个Bean，就相当于我们之前写的一个bean标签
    @Bean
    //这个方法的名字，就相当于bean标签中的id属性
    //这个方法的返回值，就相当于bean标签中的class属性
    public User getUser(){
        return new User();//就是返回要注入到bean的对象！
    }
}
```

测试类

```
import com.wyqian.config.WyqianConfig;
import com.wyqian.pojo.User;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MyTest {
    @Test
    public void getUser(){
        //如果完全使用了配置类方式去做，我们就只能通过AnnotationConfig  上下文来获取容器，通过配置类的class对象加载
        ApplicationContext context = new AnnotationConfigApplicationContext(WyqianConfig.class);
        User getUser = context.getBean("getUser", User.class);

        System.out.println(getUser.getName());
    }
}
```

这种纯Java的配置方式，在SpringBoot中随处可见！

## 10、代理模式

为什么要学习代理模式？因为这就是Spring AOP的底层！【SpringAOP和SpringMVC】

代理模式的分类：

- 静态代理
- 动态代理

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-09_210659.png)

### 10.1、静态代理

角色分析：

- 抽象角色：一般会使用接口或者抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，饿哦们一般会做一些附属操作
- 客户：访问代理对象的人！

代码步骤：

1. 接口

   ```
   public interface Rent {
       public void rent();
   }
   ```

2. 真实角色

   ```
   package com.wyqian.demo01;
   
   public class Host implements Rent{
   
       public void rent() {
           System.out.println("房东要出租房子！");
       }
   }
   ```

3. 代理角色

   ```
   package com.wyqian.demo01;
   
   public class Proxy implements Rent{
       private Host host;
   
       public Proxy() {
       }
   
       public Proxy(Host host) {
           this.host = host;
       }
   
       public void rent() {
           seeHouse();
           host.rent();
           hetong();
           fee();
       }
   
       public void seeHouse(){
           System.out.println("中介带你看房");
       }
   
       public void hetong(){
           System.out.println("签租赁合同！");
       }
   
       public void fee(){
           System.out.println("收中介费！");
       }
   }
   ```

4. 客户端访问代理角色

   ```
   package com.wyqian.demo01;
   
   public class client {
       public static void main(String[] args) {
           //房东要出租房子！
           Host host = new Host();
   
           //代理，中介帮房东租房子，但是呢？一般会加一些附加操作
           Proxy proxy = new Proxy(host);
           //你不用面对房东，直接找中介租房即可
           proxy.rent();
       }
   }
   ```

代理模式的好处：

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共业务就交给代理角色！实现了业务的分工！
- 公共业务发生扩展的时候，方便集中管理！

缺点：

- 一个真实角色就会产生一个代理角色；代码量会翻倍~开发效率会变低

### 10.2、加深理解

1、接口

```
package com.wyqian.demo02;

public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void query();
}
```

2、真实角色

```
package com.wyqian.demo02;

public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("实现了add方法");
    }

    public void delete() {
        System.out.println("实现了delete方法");
    }

    public void update() {
        System.out.println("实现了update方法");
    }

    public void query() {
        System.out.println("实现了query方法");
    }
}
```

3、代理角色

```
package com.wyqian.demo02;

public class Proxy implements UserService {

    private UserServiceImpl userServiceImpl;

    public void setUserServiceImpl(UserServiceImpl userServiceImpl) {
        this.userServiceImpl = userServiceImpl;
    }

    public void add() {
        log("add");
        userServiceImpl.add();
    }

    public void delete() {
        log("delete");
        userServiceImpl.delete();
    }

    public void update() {
        log("update");
        userServiceImpl.update();
    }

    public void query() {
        log("query");
        userServiceImpl.query();
    }

    public void log(String msg){
        System.out.println("[Debug]" + "使用了" + msg + "方法");
    }
}
```

4、客户端访问代理角色

```
package com.wyqian.demo02;

public class Client {
    public static void main(String[] args) {
        UserServiceImpl userService = new UserServiceImpl();

        Proxy proxy = new Proxy();
        proxy.setUserServiceImpl(userService);
        proxy.delete();
    }
}
```

聊聊AOP

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-09_220300.png)

### 10.3、动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的，不是我们直接写好的！
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口的—>JDK 动态代理【我们在这里使用】
  - 基于类：cglib
  - java字节码实现：javassist

需要了解两个类：Proxy：代理，InvocationHandler：调用处理程序

可以在jdk文档中找到

***例一：\***

接口

```
package com.wyqian.demo03;

//接口
public interface Rent {
    public void rent();
}
```

真实角色

```
package com.wyqian.demo03;

//房东
public class Host implements Rent {

    public void rent() {
        System.out.println("房东要出租房子！");
    }
}
```

动态生成代理角色的处理程序

```
package com.wyqian.demo03;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

//等会儿我们会用这个类，自动生成代理类
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Rent rent;

    public void setRent(Rent rent) {
        this.rent = rent;
    }

    //生成得到代理类
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),rent.getClass().getInterfaces(),this);
    }

    //处理代理实例，并返回结果
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        seeHouse();
        //动态代理的本质，就是使用反射机制实现！
        Object result = method.invoke(rent, args);
        fee();
        return result;
    }

    public void seeHouse(){
        System.out.println("中介带看房子！");
    }

    public void fee(){
        System.out.println("收中介费！");
    }
}
```

动态生成代理角色，客户端访问代理角色

```
package com.wyqian.demo03;

public class Client {
    public static void main(String[] args) {
        //真实角色
        Host host = new Host();
        //代理角色：现在没有
        ProxyInvocationHandler pih = new ProxyInvocationHandler();
        //通过调用程序处理角色来处理我们要调用的接口对象！
        pih.setRent(host);

        Rent proxy = (Rent) pih.getProxy();//这里的proxy就是动态生成的，我们并没有写~

        proxy.rent();
    }
}
```

***例二：\***

接口：

```
package com.wyqian.demo04;

public interface UserService {
    public void add();
    public void delete();
    public void update();
    public void query();
}
```

真实角色：

```
package com.wyqian.demo04;

public class UserServiceImpl implements UserService {
    public void add() {
        System.out.println("实现了add方法");
    }

    public void delete() {
        System.out.println("实现了delete方法");
    }

    public void update() {
        System.out.println("实现了update方法");
    }

    public void query() {
        System.out.println("实现了query方法");
    }
}
```

动态生成代理角色的处理程序：

```
package com.wyqian.demo04;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class ProxyInvocationHandler implements InvocationHandler {

    //要代理的接口
    private Object target;

    //生成set方法
    public void setTarget(Object target) {
        this.target = target;
    }

    //生成代理对象
    public Object getProxy(){
        return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(), this);
    }

    //自动执行的invoke()方法
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        log(method.getName());
        Object result = method.invoke(target, args);
        return result;
    }

    public void log(String msg){
        System.out.println("[Debug]" + "执行了" + msg + "方法");
    }
}
```

动态生成代理角色，客户端访问代理角色：

```
package com.wyqian.demo04;

public class Client {
    public static void main(String[] args) {
        //真实角色
        UserServiceImpl userService = new UserServiceImpl();
        //代理角色，不存在
        ProxyInvocationHandler pih = new ProxyInvocationHandler();

        pih.setTarget(userService);//设置要代理的对象

        //动态生成代理类
        UserService proxy = (UserService) pih.getProxy();

        proxy.delete();
    }
}
```

动态代理的好处：

- 可以使真实角色的操作更加纯粹！不用去关注一些公共的业务
- 公共业务就交给代理角色！实现了业务的分工！
- 公共业务发生扩展的时候，方便集中管理！
- 一个动态代理类代理的是一个接口，一般就是对应的一类业务
- 一个动态代理类可以代理多个类，只要是实现了同一个接口即可，比如例二，你再去写一个UserServiceImpl2（实现UserService接口）的话，生成它的动态代理角色程序基本和上面一样，只需修改一下真实角色就好了~

## 11、AOP

### 11.1、什么是AOP

AOP（Aspect Oriented Programming）意为：面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/640.png)

### 11.2、Aop在Spring中的作用

***提供声明式事务；允许用户自定义切面\***

以下名词需要了解下：

- 横切关注点：跨越应用程序多个模块的方法或功能。即是，与我们业务逻辑无关的，但是我们需要关注的部分，就是横切关注点。如日志 , 安全 , 缓存 , 事务等等 ….
- 切面（ASPECT）：横切关注点 被模块化 的特殊对象。即，它是一个类。
- 通知（Advice）：切面必须要完成的工作。即，它是类中的一个方法。
- 目标（Target）：被通知对象。
- 代理（Proxy）：向目标对象应用通知之后创建的对象。
- 切入点（PointCut）：切面通知 执行的 “地点”的定义。
- 连接点（JointPoint）：与切入点匹配的执行点。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/640%20(1).png)

SpringAOP中，通过Advice定义横切逻辑，Spring中支持5种类型的Advice:

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/640%20(2).png)

即 Aop 在 不改变原有代码的情况下 , 去增加新的功能 .

### 11.3、使用Spring实现AOP

【重点】使用AOP织入，需要导入一个依赖包

```
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.6</version>
    <scope>runtime</scope>
</dependency>
```

方式一：使用Spring的API接口【主要是SpringAPI接口实现】

导入aop约束

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-01-11_105527.png)

Log.java

```
package com.wyqian.log;

import org.springframework.aop.MethodBeforeAdvice;
import org.springframework.lang.Nullable;

import java.lang.reflect.Method;

public class Log implements MethodBeforeAdvice {
    //method:要执行的目标对象的方法
    //args: 参数
    //target: 目标对象
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName() + "的" + method.getName() + "方法被执行了！");
    }
}
```

AfterLog.java

```
package com.wyqian.log;

import org.springframework.aop.AfterReturningAdvice;

import java.lang.reflect.Method;

public class AfterLog implements AfterReturningAdvice {

    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了" + method.getName() + "方法，返回结果为：" + returnValue);
    }
}
<!--注册bean-->
<bean id="userService" class="com.wyqian.service.UserServiceImpl"/>
<bean id="log" class="com.wyqian.log.Log"/>
<bean id="afterLog" class="com.wyqian.log.AfterLog"/>

<!--方式一：使用原生Spring API接口-->
<!--配置AOP：需要导入aop的约束-->
<aop:config>
    <!--切入点：expression:表达式，execution(要执行的位置! * * * * *)-->
    <aop:pointcut id="pointcut" expression="execution(* com.wyqian.service.UserServiceImpl.*(..))"/>

    <!--执行环绕增加-->
    <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
    <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
</aop:config>
<bean id="diy" class="com.wyqian.diy.diyPointCut"/>
```

测试：

```
import com.wyqian.service.UserService;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MyTest {
    @Test
    public void testAop(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        //动态代理代理的是接口：注意点
        UserService userService = (UserService) context.getBean("userService");

        userService.add();
    }
}
```

方式二：自定义来实现AOP【主要是切面定义】

自定义类：

```
package com.wyqian.diy;

public class diyPointCut {
    public void before(){
        System.out.println("==============方法执行前================");
    }
    public void after(){
        System.out.println("==============方法执行后================");
    }
}
<aop:config>
    <!--自定义切面，ref:要引入的类-->
    <aop:aspect ref="diy">
        <!--切入点-->
        <aop:pointcut id="pointcut" expression="execution(* com.wyqian.service.UserServiceImpl.*(..))"/>

        <!--通知-->
        <aop:before method="before" pointcut-ref="pointcut"/>
        <aop:after method="after" pointcut-ref="pointcut"/>
    </aop:aspect>
</aop:config>
```

方式三：使用注解实现！

```
package com.wyqian.diy;

//方式三：使用注解方式实现AOP

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.Signature;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

//标注这个类是一个切面
@Aspect
public class AnnotationPointCut {

    @Before("execution(* com.wyqian.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("================方法执行前===============");
    }

    @After("execution(* com.wyqian.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("================方法执行后===============");
    }

    //在环绕增强中，我们可以给定一个参数，代表我们要获取处理切入的点
    @Around("execution(* com.wyqian.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable {

        System.out.println("环绕前");
        Signature signature = jp.getSignature();//获得签名
        System.out.println("signature: " + signature);
        Object proceed = jp.proceed();//执行方法
        System.out.println("环绕后");
    }
}
```

## 12、整合Mybatis

步骤：

1. 导入相关jar包
   - junit
   - mybatis
   - mysql数据库
   - spring相关的
   - aop织入
   - mybatis-spring【new知识点】
2. 编写配置文件
3. 测试

### 12.1、回忆Mybatis

1. 编写实体类
2. 编写核心配置文件
3. 编写接口
4. 编写mapper.xml
5. 测试

### 12.2、Mybatis-Spring

***方式一：常规方法\***

1、编写数据源配置

```
<!--DataSource:使用Spring的数据源替换Mybatis的配置  c3p0  dbcp   druid
    我们这里使用Spring提供的JDBC ：org.springframework.jdbc.datasource.DriverManagerDataSource
    -->
<bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;characterEncoding=UTF-8"/>
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
</bean>
```

2、sqlSessionFactory

```
<!--SqlSessionFactory-->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="datasource" />
    <!--绑定Mybatis的配置文件-->
    <property name="configLocation" value="classpath:mybatis-config.xml"/>
    <property name="mapperLocations" value="classpath:com/wyqian/mapper/*.xml"/>
</bean>
```

3、sqlSessionTemplate

```
<!--sqlSessionTemplate:就是我们使用的sqlSession-->
<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
    <!--只能使用构造器注入，因为它没有set方法-->
    <constructor-arg index="0" ref="sqlSessionFactory" />
</bean>
```

4、需要给接口加实现类【这是和以前写Mybatis的时候不一样的地方！以前写Mybatis不需要写接口实现类~】

接口：

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;

import java.util.List;

public interface UserMapper {
    public List<User> selectUser();
}
```

接口的实现类：

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;
import org.mybatis.spring.SqlSessionTemplate;

import java.util.List;

public class UserMapperImpl implements UserMapper {
    //我们所有的操作都是用SqlSession来执行，原来是SqlSession，现在使用SqlSessionTemplate
    private SqlSessionTemplate sqlSession;

    //为了让Spring来管理这个类，我们要使用set方法注入
    public void setSqlSession(SqlSessionTemplate sqlSession){
        this.sqlSession = sqlSession;
    }

    public List<User> selectUser() {
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        List<User> userList = mapper.selectUser();
        return userList;
    }
}
```

5、将自己写的实现类，注入到Spring中

```
<!--注册UserMapperImpl类-->
<bean id="userMapperImpl" class="com.wyqian.mapper.UserMapperImpl">
    <property name="sqlSession" ref="sqlSession"/>
</bean>
```

6、测试使用即可！

```
import com.wyqian.mapper.UserMapper;
import com.wyqian.mapper.UserMapperImpl;
import com.wyqian.pojo.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class MyTest {
    @Test
    public void selectUser() throws IOException {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapperImpl = context.getBean("userMapperImpl", UserMapperImpl.class);
        List<User> userList = userMapperImpl.selectUser();
        for (User user : userList) {
            System.out.println(user);
        }

    }
}
```

***方式二：继承SqlSessionDaoSupport类\***

1、编写数据源配置

```
<!--DataSource:使用Spring的数据源替换Mybatis的配置  c3p0  dbcp   druid
    我们这里使用Spring提供的JDBC ：org.springframework.jdbc.datasource.DriverManagerDataSource
    -->
<bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;characterEncoding=UTF-8"/>
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
</bean>
```

2、sqlSessionFactory

```
<!--SqlSessionFactory-->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="datasource" />
    <!--绑定Mybatis的配置文件-->
    <property name="configLocation" value="classpath:mybatis-config.xml"/>
    <property name="mapperLocations" value="classpath:com/wyqian/mapper/*.xml"/>
</bean>
```

3、不需要自己写sqlSessionTemplate了，直接写接口实现类：

接口：

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;

import java.util.List;

public interface UserMapper {
    public List<User> selectUser();
}
```

接口实现类：（继承SqlSessionDaoSupport类）

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;
import org.mybatis.spring.support.SqlSessionDaoSupport;

import java.util.List;

public class UserMapperImpl2 extends SqlSessionDaoSupport implements UserMapper {
    public List<User> selectUser() {
        return getSqlSession().getMapper(UserMapper.class).selectUser();
    }
}
```

4、在Spring中注入实现类，这里与常规方法也有区别，相当于少了一步获取SqlSession对象的步骤，这里配置sqlSessionFactory，而不是SqlSession。

```
<bean id="userMapperImpl2" class="com.wyqian.mapper.UserMapperImpl2">
    <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
</bean>
```

5、测试方法

```
@Test
public void selectUser2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserMapperImpl2 userMapperImpl2 = context.getBean("userMapperImpl2", UserMapperImpl2.class);
    List<User> userList = userMapperImpl2.selectUser();
    for (User user : userList) {
        System.out.println(user);
    }
}
```

## 13、声明式事务

### 13.1、回顾事务

- 把一组业务当成一个业务来做；要么都成功，要么都失败！
- 食物在项目开发中，十分的重要，设计到数据一致性的问题，不能马虎！
- 确保完整性和一致性！

事务ACID原则：

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏
- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响！被持久化地写到存储器中！

### 13.2、Spring中的事务管理

- 声明式事务：AOP
- 编程式事务：需要在代码中，进行事务的管理

思考：

为什么需要事务？

- 如果不配置十五，可能存在数据提交不一致的情况！
- 如果我们不在Spring中配置声明式事务，我们呢就需要在代码中手动配置事务！~
- 事务在项目的开发中十分重要，涉及到数据的一致性和完整性问题，不容马虎！

UserMapper接口：

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;
import org.apache.ibatis.annotations.Param;

import java.util.List;

public interface UserMapper {
    public List<User> selectUser();

    public int addUser(User user);

    public int deleteUser(@Param("id") int id);
}
```

UserMapperImpl

```
package com.wyqian.mapper;

import com.wyqian.pojo.User;
import org.mybatis.spring.support.SqlSessionDaoSupport;

import java.util.List;

public class UserMapperImpl extends SqlSessionDaoSupport implements UserMapper{
    public List<User> selectUser() {
        User user = new User(5, "小唐", "dfhuas");
        UserMapper mapper = getSqlSession().getMapper(UserMapper.class);
        mapper.addUser(user);
        mapper.deleteUser(4);
        return mapper.selectUser();
    }

    public int addUser(User user) {
        return getSqlSession().getMapper(UserMapper.class).addUser(user);
    }

    public int deleteUser(int id) {
        return getSqlSession().getMapper(UserMapper.class).deleteUser(id);
    }
}
```

UserMapper.xml

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.wyqian.mapper.UserMapper">
    <select id="selectUser" resultType="user">
        select * from mybatis.user
    </select>

    <insert id="addUser" parameterType="user">
        insert into mybatis.user (id, name ,pwd) value(#{id}, #{name}, #{pwd})
    </insert>

    <delete id="deleteUser" parameterType="_int">
        deletes from mybatis.user where id = #{id}
    </delete>
</mapper>
```

User类

```
package com.wyqian.pojo;


import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private int id;
    private String name;
    private String pwd;
}
```

mybatis-config.xml

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <!--取别名-->
    <typeAliases>
        <package name="com.wyqian.pojo"/>
    </typeAliases>
    <!--设置-->
<!--    <settings>-->
<!--        <setting name="" value=""/>-->
<!--    </settings>-->
</configuration>
```

spring-dao.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd
       http://www.springframework.org/schema/tx
       http://www.springframework.org/schema/tx/spring-tx.xsd
">
    <!--DataSource:使用Spring的数据源替换Mybatis的配置  c3p0  dbcp   druid
    我们这里使用Spring提供的JDBC ：org.springframework.jdbc.datasource.DriverManagerDataSource
    -->
    <bean id="datasource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;characterEncoding=UTF-8"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>

    <!--SqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="datasource" />
        <!--绑定Mybatis的配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/wyqian/mapper/*.xml"/>
    </bean>

    <!--sqlSessionTemplate:就是我们使用的sqlSession-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <!--只能使用构造器注入，因为它没有set方法-->
        <constructor-arg index="0" ref="sqlSessionFactory" />
    </bean>

    <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <constructor-arg ref="datasource" />
    </bean>

    <!--结合AOP实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="add" propagation="REQUIRED"/>
            <tx:method name="delete" propagation="REQUIRED"/>
            <tx:method name="update" propagation="REQUIRED"/>
            <tx:method name="query" read-only="true"/>
            <tx:method name="*" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>

    <!--配置事务切入-->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.wyqian.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>


</beans>
```

applicationContext.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="spring-dao.xml"/>
    <!--注册UserMapperImpl类-->
    <bean id="userMapperImpl" class="com.wyqian.mapper.UserMapperImpl">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>

</beans>
```

测试：

```
import com.wyqian.mapper.UserMapper;
import com.wyqian.pojo.User;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.List;

public class MyTest {
    @Test
    public void testTransaction(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserMapper userMapperImpl = context.getBean("userMapperImpl", UserMapper.class);
        List<User> userList = userMapperImpl.selectUser();
        for (User user : userList) {
            System.out.println(user);
        }
    }
}
```