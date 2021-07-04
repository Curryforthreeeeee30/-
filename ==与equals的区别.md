# ==与equals的区别

转载自[CSDN博客](https://blog.csdn.net/goforitaaa/article/details/91416373?utm_medium=distribute.pc_relevant.none-task-blog-OPENSEARCH-1.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-OPENSEARCH-1.channel_param)

## ==和equals区别



对于基本数据类型：（byte，short，char，int，float，double，long，boolean），比较的是值

他们是作为常量在方法区中的常量池里面以HashSet策略存储起来的，对于这样的字符串 “123” 也是相同的道理，在常量池中，一个常量只会对应一个地址，因此不管是再多的 123,”123” 这样的数据都只会存储一个地址，所以所有他们的引用都是指向的同一块地址，因此基本数据类型和String常量是可以直接通过==来直接比较的。

对于引用数据类型 ，有equals和==两种方法比较

==比较的是引用，比较的是引用的地址值 ，equals方法，是object中的方法，如果不进行重写的话，比较的也是引用的地址值,实际和==一样。

如果自己所写的类中已经重写了equals方法,那么就安装用户自定义的方式来比较俩个对象是否相等,如果没有重写过equal方法,那么会调用父类(Object)中的equals方法进行比较,也就是比较地址值。

一）JVM把内存划分成两种：一种是栈内存，一种是堆内存。

　　①在函数中定义的一些基本类型的变量和对象的引用变量（变量名）都在函数的栈内存中分配。

　　②当在一段代码块定义一个变量时，Java就在栈中为这个变量分配内存空间，当超过变量的作用域后，Java会自动释放掉为该变量所分配的内存空间，该内存空间可以立即被另作他用。

　　③堆内存用来存放由new创建的对象（包括由基本类型包装起来的类：Integer、String、Double，实际上每个基本类型都有他的包装类）和数组。
二) Object类中的equals方法：

```
public boolean equals(Object obj) {
return (this == obj);
```

} // 可以看出Object类中equals方法是用==判断对象引用是否指向同一内存地址。

下面看几个例子

```
String st1 = "hello";
String  st2 = "hello";
System.out.println( st1==st2); //true
st1.equals(st2);//true
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/20180823172902306.png)

讲解：String类型，它已经实现了重写，比较的时候，先比较当前对象的地址和要比较的对象的地址是否相等，若相等，则返回true,否则，提前结束比较

如果不相等，则判断是否为String的实例化对象，如果是，在判断长度是否相等，再判断数组的每个值，字母是否相等。如果都相等，则返回true.

上面的判断当执行String s1 = “hello”;这条语句时,会在堆中的字符常量池里找”hello”这个字符串,若没有找到,则将”hello”这个字符串放入字符串常量池中.而在栈中开辟一块名为s1的空间存放”hello”,这块空间的引用.当执行String s2 = “hello”;这条语句时,会在堆中的字符串常量池里找”hello”这个字符串,很显然,可以找到,于是便把字符常量池里”hello”这个字符串的引用地址赋给s2,因此s1与s2存放的都是堆中字符常量池中的同一个”hello”的引用

(2)

```
String  st2 = "hello";
String  st3 = new String("hello");
System.out.println(st2==st3);  //false  因为重现new出来的，就会重新开辟一块地址，所以比较的的是引用的地址值， false
st1.equals(st2);//true  因为String已经重写了equals方法，比较的是值，则相等，true.)String sss1 = new String("aaa");
```

(3)

```
String sss2 = new String("aaa");
System.out.println(sss1 == sss2); //false
System.out.println(sss1.equals(sss2)); // true
```

sss1和sss2都为new出来的对象，各占有一块内存空间，所以内存地址不同，但是字符串内容相同。
(4)
非String类，例如StringBuffer类 没有重写equals方法，所以不比较内容。==和equals都是比较的内存地址

```
StringBuffer stringBuffer = new StringBuffer("aaa");
StringBuffer stringBuffer2 = new StringBuffer("aaa");
System.out.println(stringBuffer == stringBuffer2); // false
System.out.println(stringBuffer.equals(stringBuffer2)); // false
```