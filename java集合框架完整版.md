# java集合框架完整版

### 集合



#### 集合概念

对象的容器，实现了对对象常用的操作，类似数组功能。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-04%20143415.png)

位置：**java.util.\*;**

#### Collection体系结构

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-04%20143805.png)

##### Collection父接口的特点

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-04%20144113.png)

##### Collection使用（1）

```
package com.wanyun.Collection;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class TestCollection {
    public static void main(String[] args) {
        Collection collection = new ArrayList();
        //添加元素
        collection.add("苹果");
        collection.add("西瓜");
        collection.add("榴莲");
        System.out.println(collection.size());
        //删除元素
        //collection.remove("西瓜");
        System.out.println(collection.size());
        /*
        遍历集合有两种方式：
        1、使用增强for
        2、使用迭代器来实现
         */
        //方式一、使用增强for循环
        System.out.println("=======方式一、使用增强for循环=======");
        for (Object o : collection) {
            System.out.println(o);
        }
        //方式二、使用迭代器来实现
        //在迭代过程中可以使用Iterator接口的方法：hasNext()、Next()和remove()方法，但是不能使用collection.remove()实现
        System.out.println("=======方式二、使用迭代器来实现=======");
        Iterator it = collection.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
            //it.remove();
        }
        System.out.println(collection.size());
        //判断
        System.out.println(collection.contains("西瓜"));
        System.out.println(collection.isEmpty());
    }
}
```

##### Collection使用（2）

```
package com.wanyun.Collection;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class TestCollection2 {
    public static void main(String[] args) {
        Collection collection = new ArrayList();
        Student s1 = new Student("小王", 17);
        Student s2 = new Student("小倩", 25);
        Student s3 = new Student("小张", 20);
        //添加元素
        collection.add(s1);
        collection.add(s2);
        collection.add(s3);
        System.out.println(collection);
        //删除元素
        //collection.remove(s1);
        //System.out.println(collection);
        //遍历元素
        //方式一：增强for循环
        System.out.println("方式一：增强for循环");
        for (Object o : collection) {
            System.out.println(o);
        }
        //方式二：使用迭代器
        System.out.println("方式二：使用迭代器");
        Iterator it = collection.iterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }
        //判断
        System.out.println(collection.contains(s1));
        collection.clear();
        System.out.println(collection.isEmpty());
    }
}


class Student{
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
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
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

#### List接口

##### List接口的特点

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-04%20161311.png)

##### List接口的使用（1）

```
package com.wanyun.List;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.ListIterator;

/**
 * List接口的使用
 * 1.有序、有下标   2.可以重复
 * @author http://wyqian.top/
 */
public class TestList {
    public static void main(String[] args) {
        //先创建集合
        List list = new ArrayList();
        //1.向集合中添加元素
        list.add("苹果");
        list.add("小米");
        list.add(0, "华为");
        System.out.println("元素个数是：" + list.size());
        System.out.println(list.toString());
        //2.删除元素
//        list.remove("苹果");
//        System.out.println("删除之后的元素个数：" + list.size());
//        list.remove(0);
//        System.out.println("删除后的元素个数：" + list.size());
//        System.out.println(list.toString());
        //3.遍历
        //方式一：使用for循环
        System.out.println("--------方式一：使用for循环---------");
        for(int i = 0; i < list.size(); i++){
            System.out.println(list.get(i));
        }
        //方式二：使用增强for
        System.out.println("--------方式二：使用增强for----------");
        for (Object o : list) {
            System.out.println(o);
        }
        //方式三：使用iterator迭代器
        System.out.println("--------方式三：使用Iterator迭代器----------");
        Iterator it = list.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //方式四：使用listIterator迭代器，与Iterator的区别是：ListIterator迭代器可以从前往后或者从后往前遍历，可以在遍历的同时增加、修改、删除元素
        System.out.println("--------方式四：使用ListIterator迭代器----------");
        System.out.println("首先是从前往后遍历");
        ListIterator lit = list.listIterator();
        while(lit.hasNext()){
            System.out.println(lit.nextIndex() + ":" + lit.next());
        }
        System.out.println("然后是从后往前遍历");
        while(lit.hasPrevious()){
            System.out.println(lit.previousIndex() + ":" + lit.previous());
        }
        //4.判断
        System.out.println(list.contains("华为"));
        System.out.println(list.isEmpty());
        //5.确定位置
        System.out.println(list.indexOf("华为"));
    }
}
```

##### List接口的使用（2）

```
package com.wanyun.List;

import java.util.ArrayList;
import java.util.List;

public class TestList2 {
    public static void main(String[] args) {
        List list = new ArrayList();
        //添加元素
        list.add(20);
        list.add(30);
        list.add(40);
        list.add(50);
        list.add(60);
        System.out.println(list.toString());
        //删除元素
        list.remove(0);//这是传入下标
        System.out.println("删除后的元素个数是：" + list.size());
        System.out.println(list.toString());
        list.remove((Object) 20);//这是使用Object强制转换
        System.out.println("删除后的元素个数是：" + list.size());
        System.out.println(list.toString());
        list.remove(new Integer(20));//这是使用new Integer()强制转换
        System.out.println("删除后的元素个数是：" + list.size());
        System.out.println(list.toString());
        //sublist()方法，子列表，含头不含尾
        List subList = list.subList(1, 4);
    }
}
```

##### List实现类

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-05%20205802.png)

##### ArrayList的使用

ArrayList的存储结构是数组，查找快，增删慢。

```
package com.wanyun.List;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.ListIterator;

public class TestArrayList {
    public static void main(String[] args) {
        //先创建一个集合
        ArrayList arrayList = new ArrayList();
        //1.添加元素
        arrayList.add(new Student("郭富城", 45));
        arrayList.add(new Student("古天乐", 46));
        arrayList.add(new Student("黎明", 48));
        System.out.println("元素个数是：" + arrayList.size());
        System.out.println(arrayList.toString());
        //2.删除元素
        /*
        arrayList.remove(new Student("郭富城", 45));
        System.out.println("删除后元素个数是：" + arrayList.size());
        System.out.println(arrayList.toString());
         */
        //3.遍历元素
        //3.1使用iterator()迭代器
        System.out.println("-------------3.1使用iterator()迭代器----------------");
        Iterator it = arrayList.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //3.2使用listIterator()迭代器正序遍历
        System.out.println("-------------3.2使用listIterator()迭代器正序遍历----------------");
        ListIterator lit = arrayList.listIterator();
        while(lit.hasNext()){
            System.out.println(lit.nextIndex() + ":" + lit.next());
        }
        //3.3使用listIterator()迭代器逆序遍历
        System.out.println("-------------3.3使用listIterator()迭代器逆序遍历----------------");
        while(lit.hasPrevious()){
            System.out.println(lit.previousIndex() + ":" + lit.previous());
        }
        //4.判断
        System.out.println(arrayList.contains(new Student("黎明", 48)));
        System.out.println(arrayList.isEmpty());
        //查找
        System.out.println(arrayList.indexOf(new Student("郭富城", 45)));
    }
}
class Student{
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
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
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    //由于remove，contains，indexOf这些方法都要用到equals，所以需要重写equals方法
    @Override
    public boolean equals(Object obj) {
        //1.判断是否为同一个对象
        if(this == obj){
            return true;
        }
        //2.判断是否为空
        if(obj == null){
            return false;
        }
        //3.如果obj是Student类型的话，就要判断obj和this的成员是否相等
        if(obj instanceof Student){
            if(this.name.equals(((Student) obj).name) && this.age == ((Student) obj).age){
                return true;
            }
        }
        return false;
    }
}
```

##### ArrayList源码分析

默认容量：DEFAULT_CAPACITY = 10;注意：当没有向集合中添加任何元素时，容量是0。但是一旦添加元素后，容量就变成了10。

存放元素的数组：elementData;

实际的元素个数：size

add方法：

```
public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
public boolean add(E e) {
        modCount++;
        add(e, elementData, size);
        return true;
    }
private void add(E e, Object[] elementData, int s) {
        if (s == elementData.length)
            elementData = grow();
        elementData[s] = e;
        size = s + 1;
    }
private Object[] grow() {
        return grow(size + 1);
    }
private Object[] grow(int minCapacity) {
        int oldCapacity = elementData.length;
        //第一次以后的每次扩容
        if (oldCapacity > 0 || elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            int newCapacity = ArraysSupport.newLength(oldCapacity,
                    minCapacity - oldCapacity, /* minimum growth */
                    oldCapacity >> 1           /* preferred growth */);
            return elementData = Arrays.copyOf(elementData, newCapacity);
        } else {
            //首次扩容
            return elementData = new Object[Math.max(DEFAULT_CAPACITY, minCapacity)];
        }
    }
```

##### Vector使用

```
package com.wanyun.List;

import java.util.Enumeration;
import java.util.Vector;

public class TestVector {
    public static void main(String[] args) {
        //创建集合
        Vector vector = new Vector();
        //1.向集合中添加元素
        vector.add("西瓜");
        vector.add("草莓");
        vector.add("香蕉");
        System.out.println("Vector中的元素个数是：" + vector.size());
        System.out.println(vector.toString());
        //2.删除元素
//        vector.remove("西瓜");
//        vector.remove(1);
//        vector.clear();
        //3.遍历元素，使用枚举器
        Enumeration en = vector.elements();
        while(en.hasMoreElements()){
            System.out.println(en.nextElement());
        }
        //判断
        System.out.println(vector.contains("西瓜"));
        System.out.println(vector.isEmpty());
        //其他方法
        vector.firstElement();
        vector.lastElement();
        vector.elementAt(1);
    }
}
```

##### LinkedList使用

与ArrayList使用基本一致。

##### LinkedList源码分析

三个属性：

```
transient int size = 0;

/**
 * Pointer to first node.
 */
transient Node<E> first;

/**
 * Pointer to last node.
 */
transient Node<E> last;
```

add()方法：

```
public boolean add(E e) {
        linkLast(e);
        return true;
    }
/**
     * Links e as last element.
     */
    void linkLast(E e) {
        final Node<E> l = last;
        final Node<E> newNode = new Node<>(l, e, null);
        last = newNode;
        if (l == null)
            first = newNode;
        else
            l.next = newNode;
        size++;
        modCount++;
    }
private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```

自己画的理解图hiahia，太丑了。。。

![img](https://i.loli.net/2020/10/06/li142a5B7z6PXmJ.jpg)

##### ArrayList和LinkedList的区别

![img](https://i.loli.net/2020/10/06/WsjI971EOqyBrwJ.png)

![屏幕截图 2020-10-06 154836](https://i.loli.net/2020/10/06/q294AoSVlMU7Bah.png)

#### 泛型

![屏幕截图 2020-10-06 155101](https://i.loli.net/2020/10/06/Jef9S2VdH3NYRnP.png)

##### 泛型类

```
package com.wanyun.Generic;

/**
 * 泛型类
 * 语法： 类名<T>
 * T是占位符，表示一种引用类型，如果编写多个，使用逗号隔开。
 * @author http://wyqian.top/
 */
public class MyGeneric<T>{
    //1.创建变量
    T t;
    //2.使用泛型作为方法参数
    public void show(T t){
        System.out.println(t);
    }
    //3.泛型作为方法的返回值
    public T getT(){
        return this.t;
    }
}
package com.wanyun.Generic;

public class TestGeneric {
    public static void main(String[] args) {
        //使用泛型类创建对象
        //注意：1.泛型只能使用引用类型   2.不同泛型类型对象之间不能相互赋值
        //1.String类型
        MyGeneric<String> myGeneric = new MyGeneric<String>();
        myGeneric.t = "Hello.nju";
        myGeneric.show("你好，南大");
        String s = myGeneric.getT();
        System.out.println(s);

        //2.Integer类型
        MyGeneric<Integer> myGeneric2 = new MyGeneric<Integer>();
        myGeneric2.t = 123;
        myGeneric2.show(456);
        Integer i = myGeneric2.getT();
        System.out.println(i);
    }
}
```

##### 泛型接口

```
package com.wanyun.Generic;

/**
 * 泛型接口
 * 语法：接口名<T>
 * 注意：不能泛型静态常量
 */
public interface MyInterface<T> {
    String name = "张三";
    T server(T t);
}
```

实现这个泛型接口有两种方法：

第一种就是在实现类的时候直接给出泛型的类型，如下所示。

```
package com.wanyun.Generic;

public class MyInterfaceImpl implements MyInterface<String>{
    @Override
    public String server(String s) {
        System.out.println(s);
        return s;
    }

    public static void main(String[] args) {
        MyInterfaceImpl impl = new MyInterfaceImpl();
        impl.server("Hello,nju");
    }
}
```

第二种就是在实现类的时候也使用泛型形式，然后在主函数创建对象的时候再给出泛型类型，如下所示：

```
package com.wanyun.Generic;

public class MyInterfaceImpl2<T> implements MyInterface<T>{
    @Override
    public T server(T t) {
        System.out.println(t);
        return t;
    }

    public static void main(String[] args) {
        MyInterfaceImpl2<Integer> myInterfaceImpl2 = new MyInterfaceImpl2<Integer>();
        myInterfaceImpl2.server(100);
    }
}
```

##### 泛型方法

```
package com.wanyun.Generic;

/**
 * 泛型方法
 * 语法：<T> 返回值类型
 */
public class MyGenericMethod {
    public <T> T show(T t){
        System.out.println("泛型方法" + t);
        return t;
    }

    public static void main(String[] args) {
        MyGenericMethod myGenericMethod = new MyGenericMethod();
        myGenericMethod.show("金州勇士加油！");
        myGenericMethod.show(123);
    }
}
```

##### 泛型集合

![img](https://i.loli.net/2020/10/06/G6bPjBEiVSNKusD.png)

如上所述，泛型对于集合的的另一个好处就是防止类型转换异常，下面这个例子就很好地说明了这个问题。

```
package com.wanyun.Generic;

import java.util.ArrayList;

public class TestGenericCollection {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList();
        arrayList.add("Hello,nju");
        arrayList.add("bye,csu");
        arrayList.add(123);
        arrayList.add(456);
        for (Object o : arrayList) {
            String s = (String)o;
            System.out.println(s);
        }
    }
}
```

上面这个例子会抛出异常：

![img](https://i.loli.net/2020/10/06/J7UMOkTFdXwPZIN.png)

因此，使用泛型地好处就出来了。

```
ArrayList<Student> student = new ArrayList<Student>();
student.add(new Student("郭富城", 45));
student.add(new Student("古天乐", 46));
student.add(new Student("黎明", 48));
//使用迭代器来遍历
Iterator<Student> it = student.iterator();
while(it.hasNext()){
    Student next = it.next();
    System.out.println(next);
}
```

#### Set子接口

##### Set接口的特点

![img](https://i.loli.net/2020/10/06/9OFL3GArm2I4vxt.png)

##### Set接口的使用

```
package com.wanyun.Set;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

/*
测试Set接口的使用
特点：1.没有下标，无序  2.不能重复
 */
public class TestSet {
    public static void main(String[] args) {
        //创建集合
        Set<String> set = new HashSet();
        //添加元素
        set.add("小米");
        set.add("苹果");
        set.add("华为");
        set.add("华为");
        System.out.println("集合中的元素个数是：" + set.size());
        System.out.println(set.toString());
        //删除元素
        //set.clear();//清空
        //set.remove("苹果");
        //遍历元素
        //方式一：使用增强for
        System.out.println("----------方式一：使用增强for------------");
        for (String s : set) {
            System.out.println(s);
        }
        //方式二：使用迭代器
        System.out.println("------------方式二：使用迭代器------------------");
        Iterator<String> it = set.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //判断
        System.out.println(set.contains("华为"));
        System.out.println(set.isEmpty());
    }
}
```

##### Set实现类

![img](https://i.loli.net/2020/10/06/cIaupTQfqSDy4M9.png)

##### HashSet使用（1）

```
package com.wanyun.Set;

import java.util.HashSet;
import java.util.Iterator;

/**
 * HashSet的使用
 * 存储结构：哈希表（数组+链表+红黑树）
 */
public class TestHashSet {
    public static void main(String[] args) {
        HashSet<String> hashSet = new HashSet<>();
        //添加元素
        hashSet.add("刘德华");
        hashSet.add("周杰");
        hashSet.add("周杰伦");
        hashSet.add("周润发");
        System.out.println("集合中的元素个数是：" + hashSet.size());
        System.out.println(hashSet.toString());
        //删除元素
        hashSet.remove("周杰");
        System.out.println("删除之后集合的元素个数是：" + hashSet.size());
        //遍历集合
        //第一种方式：使用增强for循环
        System.out.println("--------第一种方式：使用增强for循环---------");
        for (String s : hashSet) {
            System.out.println(s);
        }
        //第二种方式：使用迭代器
        System.out.println("-------------第二种方式：使用迭代器-------------");
        Iterator<String> it = hashSet.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //判断
        System.out.println(hashSet.contains("周杰伦"));
        System.out.println(hashSet.isEmpty());
    }
}
```

##### HashSet使用（2）

```
package com.wanyun.Set;

import java.util.HashSet;

/**
 * HashSet的使用
 * 存储结构：哈希表（数组+链表+红黑树）
 * 存储过程（重复依据）
 * 1.根据hashcode计算保存的位置，如果该位置为空就直接存进去，如果不为空，执行第二步
 * 2.执行equals方法，如果equals方法为true，则认为是重复，否则，形成链表
 */
public class TestHashSet2 {
    public static void main(String[] args) {
        //创建集合
        HashSet<Person> hashSet = new HashSet<>();
        //添加元素
        Person p1 = new Person("郭富城", 45);
        Person p2 = new Person("黎明", 43);
        Person p3 = new Person("周杰伦", 40);
        Person p4 = new Person("杜兰特", 35);
        hashSet.add(p1);
        hashSet.add(p2);
        hashSet.add(p3);
        hashSet.add(p4);
        System.out.println("集合中元素个数是：" + hashSet.size());
        System.out.println(hashSet.toString());
        //重写了equals方法和hashcode()之后，添加重复元素，是添不进去的
        hashSet.add(new Person("郭富城", 45));
        System.out.println("添加重复元素后，集合中元素个数是：" + hashSet.size());
        System.out.println(hashSet.toString());

        //删除元素
        hashSet.remove(new Person("郭富城", 45));
        System.out.println("删除后，集合中元素个数是：" + hashSet.size());
        System.out.println(hashSet.toString());
        
    }
}
```

##### HashSet补充

![img](https://i.loli.net/2020/10/06/NXBe1gdxi4QA2uU.png)

##### TreeSet概述

![img](https://i.loli.net/2020/10/06/MY5aJsyp18wbZWB.png)

##### TreeSet的使用

```
package com.wanyun.Set;

import java.util.Iterator;
import java.util.TreeSet;

/**
 * TreeSet的使用
 * 存储结构：红黑树，会对元素进行排序
 */
public class TestTreeSet {
    public static void main(String[] args) {
        //创建集合
        TreeSet<String> treeSet = new TreeSet<String>();
        //添加元素
        treeSet.add("Durant");
        treeSet.add("Curry");
        treeSet.add("Harden");
        System.out.println("集合元素的个数是：" + treeSet.size());
        System.out.println(treeSet.toString());
        //删除元素
        treeSet.remove("Harden");
        System.out.println("删除之后：" + treeSet.toString());
        //遍历集合
        //方式一：增强for
        System.out.println("方式一:使用增强for");
        for (String s : treeSet) {
            System.out.println(s);
        }
        //方式二：使用迭代器
        System.out.println("方式二：使用迭代器");
        Iterator<String> it = treeSet.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }
        //判断
        System.out.println(treeSet.contains("Durant"));
        System.out.println(treeSet.isEmpty());
    }
}
```

如果需要在TreeSet添加如学生类这样的对象，因为TreeSet并不知道按照什么规则排序，因此需要重写Comparable接口的compareTo()方法。

```
package com.wanyun.Set;

import com.sun.source.tree.Tree;

import java.util.TreeSet;

public class TestTreeSet2 {
    public static void main(String[] args) {
        //创建集合
        TreeSet<Person> treeSet = new TreeSet<Person>();
        Person p1 = new Person("Durant", 31);
        Person p2 = new Person("Curry", 32);
        Person p3 = new Person("Harden", 30);
        Person p4 = new Person("James", 36);
        Person p5 = new Person("Curry", 28);
        //添加元素
        treeSet.add(p1);
        treeSet.add(p2);
        treeSet.add(p3);
        treeSet.add(p4);
        treeSet.add(p5);
        System.out.println("元素个数是：" + treeSet.size());
        System.out.println(treeSet.toString());
    }
}


package com.wanyun.Set;

import java.util.Objects;

public class Person implements Comparable<Person>{
    private String name;
    private int age;

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

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age &&
                Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {
        int n1 = this.name.hashCode();
        int n2 = this.age;

        return n1 + n2;
    }

    @Override
    public int compareTo(Person o) {
        int n1 = this.getName().compareTo(o.getName());
        int n2 = this.getAge() - o.getAge();
        return n1 == 0 ? n2 : n1;
    }
}
```

也可以不实现Comparator接口：

```
package com.wanyun.Set;

import java.util.Comparator;
import java.util.TreeSet;

/**
 * TreeSet的使用
 * Comparator:实现定制比较（比较器）
 * Comparable：可比较的
 */
public class TestTreeSet3 {
    public static void main(String[] args) {
        TreeSet<Person> treeSet = new TreeSet<>(new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                int n1 = o1.getAge() - o2.getAge();
                int n2 = o1.getName().compareTo(o2.getName());
                return n1 == 0? n2 : n1;
            }
        });
        Person p1 = new Person("Curry", 32);
        Person p2 = new Person("Harden", 30);
        Person p3 = new Person("James", 28);
        Person p4 = new Person("Curry", 28);

        treeSet.add(p1);
        treeSet.add(p2);
        treeSet.add(p3);
        treeSet.add(p4);

        System.out.println("元素个数是：" + treeSet.size());
        System.out.println(treeSet.toString());

    }
}
package com.wanyun.Set;

import java.util.Comparator;
import java.util.TreeSet;

/**
 * TreeSet的使用
 * 实现字符串长度的比较
 * 利用Comparator接口定制比较规则
 */
public class TestTreeSet4 {
    public static void main(String[] args) {
        //首先创建集合
        TreeSet<String> treeSet = new TreeSet<>(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                int n1 = o1.length() - o2.length();
                int n2 = o1.compareTo(o2);
                return n1 == 0 ? n2 : n1;
            }
        });
        treeSet.add("Hello,nju");
        treeSet.add("Golden State Warriors");
        treeSet.add("LA Lakers");
        treeSet.add("Stephen Curry");
        System.out.println(treeSet.toString());
    }
}
```

#### Map集合

![img](https://i.loli.net/2020/10/10/aiTwcdMouL5E4nj.png)

##### Map父接口

![img](https://i.loli.net/2020/10/10/FJ7Z9OgGSxkljE2.png)

##### Map接口使用

Map集合的两种遍历方式：

![img](https://i.loli.net/2020/10/10/45qFzC1jSmOIYbN.png)

```
package com.wanyun.Map;

import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class TestMap {
    public static void main(String[] args) {
        //创建集合
        Map<String, String> map = new HashMap<>();
        //添加元素
        map.put("cn", "中国");
        map.put("usa", "美国");
        map.put("uk", "英国");

        System.out.println("Map集合中元素个数是：" + map.size());
        System.out.println(map.toString());
        //删除元素
//        map.remove("usa");
//        System.out.println("删除之后的Map元素个数是：" + map.size());
        //遍历元素
        //方式一：使用keySet()方法
        System.out.println("--------方式一：使用keySet()方法---------");
        Set<String> set = map.keySet();
        for (String s : set) {
            System.out.println(s + "-----" + map.get(s));
        }
        //方式二：使用entrySet()方法，这种方法效率更高
        System.out.println("--------方式二：使用entrySet()方法---------");
        Set<Map.Entry<String, String>> entries = map.entrySet();
        for (Map.Entry<String, String> entry : entries) {
            System.out.println(entry.getKey() + "-----" + entry.getValue());
        }

        //4.判断
        System.out.println(map.containsKey("usa"));
        System.out.println(map.containsValue("中国"));
    }
}
```

##### HashMap的使用（1）

```
package com.wanyun.Map;

import com.sun.security.jgss.GSSUtil;

import java.util.HashMap;

/**
 * HashMap的使用
 * 存储结构：哈希表（数组+链表+红黑树）
 */
public class TestHashMap {
    public static void main(String[] args) {
        //创建HashMap
        HashMap<Student, String> hashMap = new HashMap<Student, String>();

        //添加元素
        hashMap.put(new Student("小王",80), "beijing");
        hashMap.put(new Student("小张",81), "shanghai");
        hashMap.put(new Student("小钱",80), "hangzhou");

        System.out.println("HashMap中元素个数是：" + hashMap.size());
        System.out.println(hashMap.toString());
    }
}
```

##### HashMap的使用（2）

```
package com.wanyun.Map;

import com.sun.security.jgss.GSSUtil;

import java.util.HashMap;
import java.util.Map;
import java.util.Set;

/**
 * HashMap的使用
 * 存储结构：哈希表（数组+链表+红黑树）
 */
public class TestHashMap {
    public static void main(String[] args) {
        //创建HashMap
        HashMap<Student, String> hashMap = new HashMap<Student, String>();

        //添加元素
        hashMap.put(new Student("小王",80), "beijing");
        hashMap.put(new Student("小张",81), "shanghai");
        hashMap.put(new Student("小钱",82), "hangzhou");

        //重写了HashCode()方法之后就加不进来了。
        hashMap.put(new Student("小钱",82), "hangzhou");
        System.out.println("HashMap中元素个数是：" + hashMap.size());
        System.out.println(hashMap.toString());

        //遍历
        //方式一：使用keySet()方法
        Set<Student> set = hashMap.keySet();
        for (Student student : set) {
            System.out.println(student + "----" + hashMap.get(student));
        }
        //方式二：使用entrySet()方法
        Set<Map.Entry<Student, String>> entries = hashMap.entrySet();
        for (Map.Entry<Student, String> entry : entries) {
            System.out.println(entry.getKey() + "----" + entry.getValue());
        }
        //判断
        System.out.println(hashMap.containsKey("小张"));
        System.out.println(hashMap.containsValue("小王"));
    }
}
```

##### HashMap的一个注意点

当HashMap中存在了几个键值对之后，如果再次添加一个key相同的元素(但是value不同)，这时候虽然元素加不进来，但是会把原来的值给替换掉。

请看下面这个例子：

```
package com.wanyun.Map;

import java.util.HashMap;

public class TestHashMap2 {
    public static void main(String[] args) {
        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("库里", 30);
        hashMap.put("哈登", 13);
        hashMap.put("詹姆斯", 23);

        System.out.println("集合元素个数是：" + hashMap.size());
        System.out.println("集合中的元素有：" + hashMap.toString());

        hashMap.put("库里", 35);//集合中库里对应的值会被替换成35
        System.out.println("集合元素个数是：" + hashMap.size());
        System.out.println("集合中的元素有：" + hashMap.toString());
    }
}
```

##### HashMap源码分析（1）

首先是为什么**TREEIFY_THRESHOLD**的值为什么是8?这是说当链表长度达到8并且数组长度达到64（在源码中对应的常量是**MIN_TREEIFY_CAPACITY**）的时候，链表就会转换成红黑树，这样的话查找效率就会变高。

![img](https://i.loli.net/2020/10/11/qcwzuDANh8ZnmY3.png)

然后对应的还有一个常量是**UNTREEIFY_THRESHOLD**，意思就是说当链表长度小于6的时候，红黑树又会重新调整回链表这种结构。

![img](https://i.loli.net/2020/10/11/CEnIG2AS7udt9LY.png)

##### HashMap源码分析（2）

刚创建完HashMap之后还没有添加元素之前的话，**size**(变量)等于0和**table**为空。目的就是节省空间。

无参构造函数：

```
public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR; //只给加载因子赋了值，其它不动
    }
```

put方法解读

```
public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
    }
```

然后调到putVal函数中：

```
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            if (p.hash == hash &&
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
```

然后在putVal()函数中，首先关注的是数组大小是怎么变成16的，如下（摘自上面代码）：

```
Node<K,V>[] tab; Node<K,V> p; int n, i;
if ((tab = table) == null || (n = tab.length) == 0)
   n = (tab = resize()).length;
```

这个程序首先是定义了一个tab数组，然后定义了一个p变量，if语句中**(tab = table) == null**显然是成立的，因为table在HashMap刚创建的时候是空的。于是，我们又要进入**resize()**函数，这个函数的源码如下（部分）：

```
final Node<K,V>[] resize() {
    Node<K,V>[] oldTab = table;
    int oldCap = (oldTab == null) ? 0 : oldTab.length;
    int oldThr = threshold;
    int newCap, newThr = 0;
    if (oldCap > 0) {
        if (oldCap >= MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return oldTab;
        }
        else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
            oldCap >= DEFAULT_INITIAL_CAPACITY)
            newThr = oldThr << 1; // double threshold
    }
    else if (oldThr > 0) // initial capacity was placed in threshold
        newCap = oldThr;
    else {               // zero initial threshold signifies using defaults
        newCap = DEFAULT_INITIAL_CAPACITY;
        newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
    }
    if (newThr == 0) {
        float ft = (float)newCap * loadFactor;
        newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                  (int)ft : Integer.MAX_VALUE);
    }
    threshold = newThr;
    @SuppressWarnings({"rawtypes","unchecked"})
    Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
    table = newTab;
```

很容易分析出来，在**resize()**函数中，进入的是：

```
else {               // zero initial threshold signifies using defaults
     newCap = DEFAULT_INITIAL_CAPACITY;
     newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
}
```

于是，数组的容量就变成了16！这两句将**newTab**赋值给了**table**:

```
Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
table = newTab;
```

然后，如果数组中元素个数慢慢增加，达到了阈值（容量*加载因子）的时候，即下面的if语句（摘自**putVal()**函数）：

```
if (++size > threshold)
   resize();
```

可以看出来，又会执行**resize()**函数，但是加的容量永远是前面一次的2倍，同时阈值也会加倍：

```
else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
    oldCap >= DEFAULT_INITIAL_CAPACITY)
    newThr = oldThr << 1; // double threshold（阈值）
}
```

##### HashMap源码分析（3）

总结一下：

![img](https://i.loli.net/2020/10/11/31gRSPbpAvjFqtQ.png)

然后说一下**HashSet**，其实通过观察他的源码会发现**HashSet**就是通过**HashMap**实现的，比如说他的**add()**方法，

![img](https://i.loli.net/2020/10/11/1kZdS4VHQU26At9.png)

##### Hashtable和Properties

![img](https://i.loli.net/2020/10/11/qo3F6tE9yLCHZPw.png)

##### TreeMap的使用

![img](https://i.loli.net/2020/10/11/jbskpcw1f2RChvN.png)

```
package com.wanyun.Map;

import java.util.Comparator;
import java.util.Map;
import java.util.Set;
import java.util.TreeMap;

public class TestTreeMap {
    public static void main(String[] args) {
        //创建集合(定制排序规则)
        TreeMap<Student, String> treeMap = new TreeMap<Student, String>(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                int n1 = o1.getStuID() - o2.getStuID();
                int n2 = o1.getName().compareTo(o2.getName());
                return n1 == 0 ? n2 : n1;
            }
        });
        //添加元素
        treeMap.put(new Student("小王", 100), "beijing");
        treeMap.put(new Student("小张", 101), "shanghai");
        treeMap.put(new Student("小北", 102), "NewYork");
        System.out.println("元素个数是：" + treeMap.size());
        System.out.println(treeMap.toString());

        //删除元素
        treeMap.remove(new Student("小北", 102));
        System.out.println("删除之后的元素个数是：" + treeMap.size());

        //遍历元素
        //方式一：使用keySet()方法
        System.out.println("======方式一：使用keySet()方法======");
        Set<Student> keySet = treeMap.keySet();
        for (Student student : keySet) {
            System.out.println(student + "----" + treeMap.get(student));
        }
        //方式二：使用entrySet()方法
        System.out.println("======方式二：使用entrySet()方法======");
        Set<Map.Entry<Student, String>> entries = treeMap.entrySet();
        for (Map.Entry<Student, String> entry : entries) {
            System.out.println(entry.getKey() + "----" + entry.getValue());
        }

        //判断
        System.out.println(treeMap.containsKey(new Student("小王", 100)));
        System.out.println(treeMap.containsValue("NewYork"));

    }
}
//继承Comparable接口，重写compareTo()方法
@Override
    public int compareTo(Student o) {
        int n1 = this.getStuID() - o.getStuID();
        int n2 = this.getName().compareTo(o.getName());
        return n1 == 0 ? n2 : n1;
    }
```

#### Collections工具类

![img](https://i.loli.net/2020/10/11/xDbkj4A6it5cGuq.png)

```
package com.wanyun.Collections;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

/**
 * 测试Collections工具类
 */
public class TestCollections {
    public static void main(String[] args) {
        //创建一个集合
        List<Integer> list = new ArrayList<Integer>();
        //添加一些元素
        list.add(10);
        list.add(68);
        list.add(54);
        list.add(323);
        list.add(213);
        //sort排序
        Collections.sort(list);
        System.out.println(list.toString());

        //binarySearch二分查找
        int i = Collections.binarySearch(list, 54);
        System.out.println(i);
        int j = Collections.binarySearch(list, 45);
        System.out.println(j);

        //copy复制
        List<Integer> dest = new ArrayList<>();
        for(int k = 0; k < list.size(); k++){
            dest.add(0);
        }
        Collections.copy(dest, list);
        System.out.println(dest.toString());

        //reverse反转
        Collections.reverse(list);
        System.out.println(list);

        //shuffle 打乱顺序
        Collections.shuffle(list);
        System.out.println(list);

        //List转数组
        Integer[] arr = list.toArray(new Integer[0]);//这个地方参照一下api手册，里面有介绍
        System.out.println(arr.length);
        System.out.println(Arrays.toString(arr));

        //数组转List
        List<Integer> list2 = Arrays.asList(arr);
        //数组转List的集合受限，不能添加和删除
        System.out.println(list2);
    }
}
```