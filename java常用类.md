# java常用类

### 转载

[https://blog.csdn.net/qq_42629988/article/details/108046740?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160170872119195188318565%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160170872119195188318565&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-108046740.pc_first_rank_v2_rank_v28_p&utm_term=%E5%B8%B8%E7%94%A8%E7%B1%BB&spm=1018.2118.3001.4187](https://blog.csdn.net/qq_42629988/article/details/108046740?ops_request_misc=%7B%22request%5Fid%22%3A%22160170872119195188318565%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=160170872119195188318565&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-108046740.pc_first_rank_v2_rank_v28_p&utm_term=常用类&spm=1018.2118.3001.4187)

### String类

```
package com.kuang;

import java.util.Arrays;

public class TestString {
    public static void main(String[] args) {
        String s = "abc";
        //1.字符串转字节数组，toCharArray()
        char[] charArray = s.toCharArray();
        System.out.println(Arrays.toString(charArray));

        //2.替换字符串，replace()
        String s1 = s.replace('b','3');
        System.out.println(s);
        System.out.println(s1);

        //3.判断是否含有指定字符串，contains()
        String s3 = "abcgerghe";
        boolean flag1 = s3.contains("abc");
        boolean flag2 = s3.contains("ij");
        System.out.println(Boolean.toString(flag1) + Boolean.toString(flag2));

        //4.比较字符的大小，compareTo()
        String s4 = "abc";
        String s5 = "ab";
        int a = s4.compareTo(s5);
        int b = s5.compareTo(s4);
        System.out.println(a);
        System.out.println(b);

        //5.子字符串第一次，最后一次在字符串中出现的下标，indexOf(), lastIndexOf()
        String s6 = "诚朴雄伟,励学敦行,知行合一,经世致用。";
        System.out.println(s6.indexOf(","));
        System.out.println(s6.lastIndexOf(","));

        //6.制定索引位置，截取子字符串，subString()
        String s7 = s6;
        System.out.println(s7.substring(0,4));

        //7.根据指定字符，转化成数组。split();
        String s8 = "你好-这里是南京市-南大-欢迎你来到电子学院-学习！";
        String [] temp = s8.split("-");
        for (String s2 : temp) {
            System.out.println(s2);
        }

        //8.去掉字符串前后空格,trim()
        String s9 = "   这里是雷达实验室    ";
        System.out.println(s9.trim());

        //9.截取指定位置字符，charAt()
        String s10 = "abcd";
        System.out.println(s10.charAt(1));

        //10.字符串拼接,concat()
        String s11 = "这里是";
        String s12 = "南大";
        String s13 = s11.concat(s12);
        System.out.println(s13);

    }
}
```

### Date类和SimpleDateFormat类

复习时间和日期时请参考廖雪峰的官方网站：https://www.liaoxuefeng.com/

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20170108.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20170401.png)

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20170532.png)

```
package com.kuang;

import java.text.SimpleDateFormat;
import java.util.Date;

public class TestDate {
    public static void main(String[] args) {
        //获取当前时间
        Date date = new Date();
        System.out.println(date.getTime());//时间戳，long类型以毫秒表示的时间戳
        System.out.println(date.getYear() + 1900);
        System.out.println(date.getMonth() + 1);
        System.out.println(date.getDate());

        //转换成String格式
        System.out.println(date.toString());//China Standard Time,简称CST,中国标准时间
        System.out.println(date.toGMTString());//GMT时区表示
        System.out.println(date.toLocaleString());//本地时间表示

        //simpleDateFormat类
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//打印出我们想要的格式
        System.out.println(format.format(date));
    }
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20172158.png)

### Calendar类

`Calendar`可以用于获取并设置年、月、日、时、分、秒，它和`Date`比，主要多了一个可以做简单的日期和时间运算的功能。

```
package com.kuang;

import java.text.SimpleDateFormat;
import java.util.Calendar;

public class TestCalendar {
    public static void main(String[] args) {
        //获取当前时间
        Calendar time = Calendar.getInstance();

        int y = time.get(Calendar.YEAR);
        int m = time.get(Calendar.MONTH) + 1;
        int d = time.get(Calendar.DAY_OF_MONTH);
        int hh = time.get(Calendar.HOUR_OF_DAY);
        int MM = time.get(Calendar.MINUTE);
        int ss = time.get(Calendar.SECOND);
        int ms = time.get(Calendar.MILLISECOND);

        //打印出当前时间
        System.out.println(y + "-" + m + "-" + d + "  " + hh + ":" + MM + ":" + ss + ":" + ms);
        //利用time.getTime()方法可以将Calendar对象转换成Date对象，然后利用format方法显示
        System.out.println(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(time.getTime()));
    }
}
```

### TimeZone类

`Calendar`和`Date`相比，它提供了时区转换的功能。时区用`TimeZone`对象表示。

```
package com.kuang;

import java.util.TimeZone;

public class TestTimeZone {
    public static void main(String[] args) {
        TimeZone tzDefault = TimeZone.getDefault();//当前时区

        TimeZone tzGMT8 = TimeZone.getTimeZone("GMT-8:00");//GMT时区
        TimeZone tzAs = TimeZone.getTimeZone("Asia/Shanghai");//上海时区

        System.out.println(tzDefault.getID());
        System.out.println(tzGMT8.getID());
        System.out.println(tzAs.getID());
    }
}
```

### 转换时区-使用TimeZone类实现

```
package com.kuang;

import java.sql.Time;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.TimeZone;

public class TestChangeTimeZone {
    public static void main(String[] args) {
        Calendar c  = Calendar.getInstance();

        //清除所有
        c.clear();
        //设置时区
        c.setTimeZone(TimeZone.getTimeZone("Asia/Shanghai"));
        //设置时间
        c.set(2020,9,3,19,43,20);
        //下面做转换时区,从中国上海时区转换到美国纽约时区
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd hh:MM:ss");
        sdf.setTimeZone(TimeZone.getTimeZone("America/New_York"));
        System.out.println(sdf.format(c.getTime()));
    }
}
```

### 获取系统当前时间戳

```
System.out.println(System.currentTimeMillis());//获得系统当前时间戳
```

### LocalDateTime类

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20195157.png)

```
package com.kuang;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

public class TestLocateDateTime {
    public static void main(String[] args) {
        LocalTime lt = LocalTime.now();//当前时间
        LocalDate ld = LocalDate.now();//当前日期
        LocalDateTime ldt = LocalDateTime.now();//当前日期和时间

        System.out.println(lt);
        System.out.println(ld);
        System.out.println(ldt);

        //也可以像下面这样：
        LocalDateTime ldt2 = LocalDateTime.now();
        LocalDate ld2 = ldt2.toLocalDate();
        LocalTime lt2 = ldt2.toLocalTime();

        //反过来也可创建LocalDateTime对象
        LocalDateTime DateTimeNow = LocalDateTime.of(2020, 10, 3, 20, 00, 00);
        System.out.println(DateTimeNow);
        LocalDate dateNow = LocalDate.of(2020, 10, 3);
        LocalTime timeNow = LocalTime.of(20, 02, 00);

        //按照ISO8601的格式传入也是没有问题的
        LocalDateTime parse = LocalDateTime.parse("2020-10-03T20:00:45.482437900");

    }
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20200603.png)

### DateTimeFormatter类

```
package com.kuang;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class TestDateTimeFormatter {
    public static void main(String[] args) {
        //用DateTimeFormatter.ofPattern实现和SimpleDateFormat类中format()方法一样的效果
        DateTimeFormatter dTF = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        System.out.println(dTF.format(LocalDateTime.now()));

        //自定义解析
        LocalDateTime ldt = LocalDateTime.parse("2020/10/03 20:16:20", dTF);
        System.out.println(ldt);
    }
}
```

还可以指定Locale，比如说指定中国或者是美国，请看下面这个例子：

```
package com.kuang;

import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class TestDateTimeFormatter2 {
    public static void main(String[] args) {
        //获取当前时间
        ZonedDateTime zDT = ZonedDateTime.now();

        //指定是中国或者美国
        DateTimeFormatter dTF1 = DateTimeFormatter.ofPattern("yyyy MM dd EE HH:mm:ss", Locale.CHINA);
        DateTimeFormatter dTF2 = DateTimeFormatter.ofPattern("EE MM dd yyyy HH:mm:ss", Locale.US);

        System.out.println(dTF1.format(zDT));
        System.out.println(dTF2.format(zDT));
    }
}
```

### Duration类和Period类

```
package com.kuang;

import java.time.Duration;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.Period;
import java.time.format.DateTimeFormatter;

public class TestDateTimeFormatter {
    public static void main(String[] args) {
        //用DateTimeFormatter.ofPattern实现和SimpleDateFormat类中format()方法一样的效果
        DateTimeFormatter dTF = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        System.out.println(dTF.format(LocalDateTime.now()));

        //自定义解析,解析成ISO 861格式
        LocalDateTime ldt = LocalDateTime.parse("2020/10/03 20:16:20", dTF);
        System.out.println(ldt);

        //测试isBefore()方法和isAfter()方法
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime target = LocalDateTime.of(2020,10,4,12,20,23);
        System.out.println(now.isBefore(target));
        System.out.println(now.isAfter(target));

        //测试Duration类和Period类,Duration类只用于LocalDateTime类，Period类只用于LocalDate类
        LocalDateTime d1 = LocalDateTime.now();
        LocalDateTime d2 = LocalDateTime.of(2020, 10, 4,20,29,50);
        Duration timeBetween = Duration.between(d1, d2);
        System.out.println(timeBetween);

        LocalDate d3 = LocalDate.now();
        LocalDate d4 = LocalDate.of(2020, 11, 4);
        Period daysBetween = Period.between(d3, d4);
        System.out.println(daysBetween);
    }
}
```

### ZonedDateTime类

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20211013.png)

```
package com.kuang;

import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;

public class TestZonedDateTime {
    public static void main(String[] args) {
        //创建带时区的日期和时间的方式1：使用ZonedDateTime.now()方法
        //获取当前时间
        ZonedDateTime zDT = ZonedDateTime.now();
        //获取美国纽约时区的当前时间
        ZonedDateTime zDT2 = ZonedDateTime.now(ZoneId.of("America/New_York"));

        System.out.println(zDT);
        System.out.println(zDT2);

        //创建带时区的日期和时间的方式2：使用LocalDateTime中的atZone()方法
        LocalDateTime ldt = LocalDateTime.now();
        ZonedDateTime zDT3 = ldt.atZone(ZoneId.of("America/New_York"));
        ZonedDateTime zDT4 = ldt.atZone(ZoneId.systemDefault());//系统默认时区
        System.out.println(zDT3);
        System.out.println(zDT4);
    }
}
```

### 转换时区-使用ZonedDateTime类实现

比用TimeZone类实现简单多了……

```
package com.kuang;

import java.time.ZoneId;
import java.time.ZonedDateTime;

public class TestChangeTimeZone2 {
    public static void main(String[] args) {
        ZonedDateTime zDT = ZonedDateTime.now(ZoneId.of("Asia/Shanghai"));
        ZonedDateTime zDT2 = zDT.withZoneSameInstant(ZoneId.of("America/New_York"));

        System.out.println(zDT);
        System.out.println(zDT2);
    }
}
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20212955.png)

### Instant

这个类也能实现时间戳，效果和**System.currentTimeMillis()**效果是一样的

```
package com.kuang;

import java.time.Instant;

public class TestInstant {
    public static void main(String[] args) {
        Instant now = Instant.now();
        long epochSecond = now.getEpochSecond();//获取时间戳,是以秒为单位的

        long l = now.toEpochMilli();//这个就是一以ms为单位的

        System.out.println(epochSecond);
        System.out.println(l);
        System.out.println(System.currentTimeMillis());
    }
}
```

Instant是高精度时间戳，它可以实现ZonedDateTime的互换。

```
// 以指定时间戳创建Instant:
Instant ins = Instant.ofEpochSecond(1568568760);
ZonedDateTime zdt = ins.atZone(ZoneId.systemDefault());
System.out.println(zdt); // 2019-09-16T01:32:40+08:00[Asia/Shanghai]
```

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/PicturteBed/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202020-10-03%20215751.png)