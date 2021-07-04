# JVM探究



- 请你谈谈你对JVM的理解？Java8虚拟机和之前的变化更新？
- 什么是OOM，什么是栈溢出 StackOverFlowError?怎么分析？
- JVM的常用调优参数有哪些？
- 内存快照如何抓取？怎么分析Dump文件？知道吗？
- 谈谈JVM中，类加载器你的认识？rt.jar ext application

1. JVM的位置

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_144404.png)

2. JVM的体系机构

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_145025.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_145213.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_145320.png)

3. 类加载器

   作用：加载Class文件~new Student();

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_152622.png)

   1. 虚拟机自带的加载器

   2. 启动类（根）加载器

   3. 扩展类加载器

   4. 应用程序加载器

   5. 百度：***双亲委派机制\***

      https://blog.csdn.net/codeyanbao/article/details/82875064

4. 双亲委派机制

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/20201217213314510.png)

   ```
   package java.lang;
   
   public class String {
   
       //双亲委派机制：安全
       //1.APP-->EXC---Bootstrap(最终执行)
       //ROOT
       //EXC
       //APP
   
       public String toString() {
           return "Hello";
       }
   
       public static void main(String[] args) {
           String s = new String();
           System.out.println(s.toString());
           System.out.println(s.getClass().getClassLoader());
       }
   
       /*
       1. 类加载器收到类加载的请求
       2. 将这个请求向上委托给父类加载器去完成，一直向上委托，直到启动类加载器
       3. 启动加载器检查是否能够加载当前这个类，能加在就结束，使用当前的加载器，否则，抛出异常，通知子加载器进行加载
       4. 重复步骤3
       Class Not Found~
       null: java调用不到~ C  C++
       Java ==> C++ 去掉了指针和内存管理，于是乎Java被称为C++--
        */
   
   }
   ```

   ```
   public class Car {
   
       public int age;
   
       public static void main(String[] args) {
           //类是抽象的模板，对象是具体的
   //        Class<Car> carClass = Car.class;
   
           Car car1 = new Car();
           Car car2 = new Car();
           Car car3 = new Car();
   
   
           Class<? extends Car> aClass = car1.getClass();
   
   
   
           ClassLoader classLoader = aClass.getClassLoader();//AppClassLoader
           System.out.println(aClass.getClassLoader());
           ClassLoader parent = classLoader.getParent();//ExtClassLoader   \jre1.8.0_152\lib\ext
           System.out.println(parent);
           ClassLoader parentParent = parent.getParent();//null  1.不存在   2.java程序获取不到~   rt.jar
           System.out.println(parentParent);
   
       }
   }
   ```

5. 沙箱安全机制

    Java安全模型的核心就是Java沙箱（sandbox），什么是沙箱？沙箱是一个限制程序运行的环境。沙箱机制就是将Java代码限定在虚拟机（JVM）特定的运行范围中，并且严格限制代码对本地系统资源的访问，通过这样的措施来保护对代码的有效隔离，防止对本地系统造成破坏。沙箱主要限制系统资源访问，那系统资源包括什么？CPU、内存、文件系统、网络。不同级别的沙箱对这些资源访问的限制也可以不一样。

    所有的java程序都可以指定沙箱，可以定制安全策略。

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_165143.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_165219.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_165318.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_165531.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_170142.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-25_170419.png)

6. Native

   ```
   public class Demo {
       public static void main(String[] args) {
           new Thread(()-> {
           }, "my thread name").start();
       }
       /*
       native：凡是带了native关键字的，说明java的范围达不到了，回去调用底层C语言的库
       会进入本地方法栈
       调用本地方法本地接口  JNI
       JNI作用：扩展Java的使用，融合不同的编程语言为Java所用！最初：C、C++
       Java诞生的时候C、C++横行，想要立足，必须要有调用C、C++的程序
       他在内存区域中专门开辟了一块标记区域：Native Method Stack,登记native方法
       在最终执行的时候，加载本地方法库中的方法通过JNI
        */
   
       //java程序驱动打印机，管理系统，掌握即可，在企业级应用中较为少见！
       private native void start0();
   
       //调用其他接口(异构领域间通信)：Socket、WebService、http
   }
   ```

7. PC寄存器

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-26_090045.png)

8. 方法区

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-26_090800.png)

9. 栈：数据结构

   程序 = 数据结构 + 算法：持续学习~

   程序 = 框架 + 业务逻辑~~：吃饭~~

   栈：先进后出、后进先出：桶

   队列：先进先出（FIFO：First Input First Output）

   喝多了吐就是栈，吃多了拉就是队列

   为什么main()先执行，最后结束~

   栈：栈内存，主管程序的运行，生命周期和线程同步；

   线程结束，栈内存也就是释放了，对于栈来说，不存在垃圾回收问题

   一旦线程结束，栈就Over!

   栈：8大基本类型+对象引用+实例的方法

   栈运行原理：栈帧

   栈满了：StackOverFlowError

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-26_092948.png)

栈+堆+方法区 交互关系

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-26_093341.png)

**画出一个对象实例化的过程在内存中：百度、看视频~**

https://blog.csdn.net/Tony__Jaa/article/details/107612059

1. 三种JVM

   - Sun公司 HotSpot
   - BEA JRockit
   - IBM J9VM

   我们学习都是：HotSpot

2. 堆

   Heap，一个JVM只有一个堆内存，堆内存的大小是可以调节的。

   类加载器读取了类文件后，一般会把什么东西放到堆中呢？类，方法，常量，变量~，保存我们所有引用类型的真实对象！

   堆内存中还要细分为三个区域：

   - 新生区 Young/New（伊甸园区）
   - 养老区 old
   - 永久区 Perm

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-26_134802.png)

   GC垃圾回收主要是在伊甸园区和养老区~

   假设内存满了，OOM，堆内存不够!

   在jdk8以后，永久存储区有另外一个名字（元空间）

3. 新生区

   - 类：诞生和成长的地方，甚至死亡；
   - 伊甸园，所有的对象都是在伊甸园区new出来的！
   - 幸存者区（0，1）
   - ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-27_193806.png)

   真理：经过研究，99%的对象都是临时对象！

4. 老年区

5. 永久区

   这个区域常驻内存的，用来存放JDK自身携带的Class对象。Interface元数据，存储的是Java运行时的一些环境或类信息~~这个区域不存在垃圾回收！关闭虚拟机就会释放这个区域的内存~~

   一个启动类，加载了大量的第三方jar包。Tomcat部署了太多的应用，大量动态生成的反射类。不断地被加载，直到内存满，就会出现OOM；

   - jdk1.6之前，永久代，常量池是在方法区中；
   - jdk1.7，永久代，但是慢慢的退化了，`去永久代`，常量池在堆中
   - jdk1.8之后，无永久代，常量池在元空间
   - ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-27_195510.png)
   - ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-27_195405.png)

   元空间逻辑上存在，物理上不存在~

6. 堆内存调优

   例子1：元空间逻辑上存在，物理上不存在

   ```
   public class Demo02 {
       public static void main(String[] args) {
           //返回虚拟机试图使用的最大内存
           long max = Runtime.getRuntime().maxMemory();
           //返回jvm的总内存
           long total = Runtime.getRuntime().totalMemory();
   
           System.out.println("max=" + max +"字节\t" + (max/(double)1024/1024)+"MB");
           System.out.println("total=" + total +"字节\t" + (total/(double)1024/1024)+"MB");
           // 默认情况下：分配的总内存(max)是电脑内存的1/4，而初始化内存(total)：1/64
   
           //OOM:
               //1、尝试扩大堆内存看结果，如果堆内存扩大了程序还报OOM，那说明是程序写错了
               //2、分析内存，看一下哪个地方出现了问题（专业工具）
           //-Xms1024m -Xmx1024m -XX:+PrintGCDetails
   
           //305664K(新生代)+699392K(老年代)=981.5MB
       }
   }
   ```

   例子2：轻重GC展示

   ```
   import java.util.Random;
   
   //-Xms8m -Xmx8m -XX:+PrintGCDetails
   public class Hello {
       public static void main(String[] args) {
           String str = "wyqian";
           while(true){
               str += str + new Random().nextInt(99999999)+new Random().nextInt(88888888);
           }
       }
   }
   ```

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-27_203215.png)

   在一个项目中，突然出现OOM故障，那么该如何排除？研究为什么出错~

   - 能够看到代码第几行出错：内存快照分析工具，MAT，JProfiler
   - Debug，一行行分析代码！

   ***MAT，JProfiler作用：\***

   - 分析Dump内存文件，快读定位内存泄漏；
   - 获得堆中的数据
   - 获得大的对象~
   - ……

   ```
   import java.util.ArrayList;
   
   //-Xms：设置初始化分配内存大小 默认1/64
   //-Xmx：设置最大分配内存大小 默认1/4
   //-XX:PrintGCDetails  打印GC垃圾回收信息
   //-Xms1m -Xmx8m -XX:+HeapDumpOnOutOfMemoryError   OOM Dump文件
   public class Demo03 {
       byte[] array = new byte[1024*1024];
   
       public static void main(String[] args) {
           ArrayList<Demo03> list = new ArrayList<Demo03>();
           int count = 0;
   
           try{
               while(true){
                   list.add(new Demo03());
                   count++;
               }
           }catch(Error e){
               System.out.println("count:"+count);
               e.printStackTrace();
           }
   
       }
   }
   ```

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_102356.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_102412.png)

7. GC：垃圾回收机制，不能手动回收

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_163610.png)

   JVM在进行GC时，并不是对这三个区域统一回收。大部分时候，回收都是新生代~

   - 伊甸园区
   - 幸存区（from， to）
   - 老年区

   GC两种类：轻GC(普通的GC)、重GC(全局GC)

   题目：

   - JVM的内存模型和分区~详细到每一个区放什么
   - 堆里面的分区有哪些？Eden，from，to，老年区，说说他们的特点！
   - GC的算法有哪些？标记清除法，标记整理法，复制算法，引用计数法，怎么用的？
   - 轻GC和重GC分别在什么时候发生？

   ***引用计数法：\***

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_164559.png)

   ***复制算法：\***

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_165649.png)

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_170110.png)

   - 好处：没有内存的碎片
   - 坏处：浪费了内存空间~：多了一半空间永远是空to。假设对象100%存活（极端情况）

   复制算法最佳使用场景：对象存活度较低的时候；新生区~

   ***标记清除算法：\***

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_170911.png)

   - 优点：不需要额外的空间！
   - 缺点：两次扫描，严重浪费时间，会产生内存碎片。

   ***标记清除压缩算法：\***

   先标记清除几次，再压缩！he

   再优化：

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_171242.png)

8. 总结

内存效率：复制算法>标记清除算法>标记压缩算法（时间复杂度）

内存整齐度：复制算法=标记压缩>标记清除算法

内存利用率：标记压缩算法=标记清除算法>复制算法

思考：难道没有最优的算法吗？

答案：没有，没有最好的算法，只有最合适的算法！—->GC：分代收集算法

年轻代：

- 存活率低
- 复制算法！

老年代：

- 区域大：存活率高
- 标记清除（内存碎片不是太多）+标记压缩混合 实现

一天时间学JVM，不现实，要深究，必须要下去花时间，和多看面试题，以及《深入理解Java虚拟机》

但是，我们可以掌握一个学习JVM的方法。

18、JMM：Java Memory Model

1. 什么是JMM？

2. 它干嘛的？：官方，其他人的博客，对应的视频！

   作用：缓存一致性协议，用于定义数据读写的规则（遵守，找到这个规则 ）

   JMM定义了线程工作和主内存之间的抽象关系：线程之间的共享变量存储在主内存（Main Memory）中，每个线程都有一个私有的本地内存（Local Memory）

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-28_185803.png)

   解决共享对象可见性问题：volidate

3. 它如何学习？

   JMM：抽象概念，理论

   volidate ：

   ![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/2021-03-29_171421.png)

4. 百度

5. 思维导图