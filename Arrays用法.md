# Arrays用法

### Arrays常用的方法



```
package com.kuang;

import java.lang.reflect.Array;
import java.util.Arrays;
import java.util.List;

public class TestArrays {
    public static void main(String[] args) {
        //将数组转换成字符串，使用toString()方法
        int[] array = new int[]{1, 2, 3};
        String newString = Arrays.toString(array);
        System.out.println(newString);
        //如果是二维数组的话，使用deepToString()方法
        int[][] array2 = new int[][]{{1, 2, 3},{4, 5, 6}};
        String newString2 = Arrays.toString(array2);
        System.out.println(newString2);//看源码就知道这不是打印的二维数组，deepToString才是
        String newString3 = Arrays.deepToString(array2);
        System.out.println(newString3);

        //填充数组，使用fill()方法
        int[] array3 = new int[6];
        Arrays.fill(array3, 1);
        System.out.println(Arrays.toString(array3));
        Arrays.fill(array3, 1,6,-1);
        System.out.println(Arrays.toString(array3));

        //数组元素排序，使用sort()方法和parallelSort()方法，都可以指定范围排序
        int [] array4 = new int[]{5, 9, 4, 0, 3};
        Arrays.sort(array4);
        System.out.println(Arrays.toString(array4));
        array4 = new int[]{5, 9, 4, 0, 3};
        Arrays.sort(array4, 0,4);
        System.out.println(Arrays.toString(array4));
        array4 = new int[]{5, 9, 4, 0, 3};
        Arrays.parallelSort(array4);
        System.out.println(Arrays.toString(array4));

        //数组的比较，使用equals()方法
        int[] array5 = new int[]{1, 2, 3};
        int[] array6 = new int[]{1, 2, 3};
        int[] array7 = new int[]{2, 1, 3};
        System.out.println(Arrays.equals(array5, array6));
        System.out.println(Arrays.equals(array5, array7));

        //如果是二维数组的话，就使用deepEquals()方法
        int[][] array8 = new int[][]{{1, 2, 3},{4, 5, 6}};
        int[][] array9 = new int[][]{{1, 2, 3},{4, 5, 6}};
        System.out.println(Arrays.equals(array8, array9));
        System.out.println(Arrays.deepEquals(array8, array9));

        //数组复制，使用copyOf()方法和copyOfRange()方法
        int[] array10 = new int[]{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int[] copyArray = Arrays.copyOf(array10, 5);
        System.out.println(Arrays.toString(copyArray));
        int[] copyArray2 = Arrays.copyOfRange(array10, 0, 5);
        System.out.println(Arrays.toString(copyArray2));

        //二分查找返回下标，使用binarySearch()方法
        int[] array11 = new int[]{1, 5, 7, 9};
        System.out.println(Arrays.binarySearch(array11, 9));
        System.out.println(Arrays.binarySearch(array11, 8));//返回-4

        //数组转List，使用asList()方法，转载：https://blog.csdn.net/kzadmxz/article/details/80394351?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param
        //这种方法建立出来的
        Integer array12[] = new Integer[]{1, 5, 9};
        List<Integer> list = (List<Integer>) Arrays.asList(array12);
        System.out.println(list.contains(1));

        //Arrays.asList()方法不建议使用在基本数据类型中。适用于对象型数据的数组（String、Integer...）。
        int[] array13 = new int[]{2, 4, 8};
        List<int[]> list2 = Arrays.asList(array13);
        System.out.println(list2.contains(2));

        //对数组元素采用指定的方法计算，正则表达式
        int[] array14 = new int[]{3, 0, 5, 14, 8};
        Arrays.parallelPrefix(array14, (x, y) -> (x + y));
        System.out.println(Arrays.toString(array14));

        array14 = new int[]{3, 0, 5, 14, 8};
        Arrays.setAll(array14, (x) -> (x * x));
        System.out.println(Arrays.toString(array14));//操作的是索引
    }
}
```

### 重写Comparable接口，实现对其他对象数组排序

```
package com.kuang;

import java.util.Arrays;

public class TestComparable {
    public static void main(String[] args) {
        Employee[] e = new Employee[3];
        e[0] = new Employee(10);
        e[1] = new Employee(5);
        e[2] = new Employee(30);
        Arrays.sort(e);
        System.out.println(Arrays.toString(e));
    }
}

class Employee implements Comparable<Employee>{
    private int id;//员工id编号

    public Employee(int id) {
        this.id = id;
    }

    @Override
    public int compareTo(Employee o) {
        return this.id - o.id;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "id=" + id +
                '}';
    }
}
```

### 自定义排序规则，重写Comparator接口

```
package com.kuang;

import java.util.Arrays;
import java.util.Comparator;

public class TestComparator implements Comparator<String> {
    @Override
    public int compare(String o1, String o2) {
        return o1.length() - o2.length();
    }

    public static void main(String[] args) {
        String []names = {"Alice", "Tom", "Durant"};
        Arrays.sort(names, new TestComparator());
        System.out.println(Arrays.toString(names));
    }
}
```

因为，Comparator只有一个方法，所以是函数式接口，也可以用Lambda表达式来实现

```
String[] names2 = {"Alice", "Tom", "Durant"};
Arrays.sort(names2, (first, second) -> {
    return first.length() - second.length();
});
System.out.println(Arrays.toString(names2));
```