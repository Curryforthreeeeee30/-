# java集合和Hash Set

### java集合的概念



定义：如果一个Java对象能够在内部持有其他Java对象，并对外提供访问接口，那么这个对象就是集合。
有各种各样的集合，比如：
1.数组
2.元素不重复的集合
3.可变大小的顺序链表
。。。。。。
java.util自带集合类，主要提供三种集合类：
1.list: 有序列表的集合
2.Set: 没有重复元素的集合
3.Map: “key-value”类型的集合
今天主要记录的是Set，其中最著名的是Hash Set。

### Hash Set

Hash Set是无序的，而Tree Set则是有序的。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/hashSet.jpg)

比如说，举个栗子：

```
public class Main {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("apple");
        set.add("banana");
        set.add("pear");
        set.add("orange");
        for (String s : set) {
            System.out.println(s);
        }
    }
}
```

这种情况是HashSet，其结果见下图，很容易看到它是无序的。
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/Hashset.png)

```
public class Main {
    public static void main(String[] args) {
        Set<String> set = new TreeSet<>();
        set.add("apple");
        set.add("banana");
        set.add("pear");
        set.add("orange");
        for (String s : set) {
            System.out.println(s);
        }
    }
}
```

这种情况是TreeSet，其结果见下图，可以看到结果是有序的。
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/TreeSet.png)

#### Set提供的方法

主要有以下三个：
**add**：添加元素
**remove**：移除元素
**contains**：判断Set是否包含元素