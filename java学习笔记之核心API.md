# java学习笔记之核心API

### Java Number & Math 类



#### 说明

1.所有的包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类Number 的子类。当内置数据类型被当作对象使用的时候，编译器会把内置类型装箱为包装类。相似的，编译器也可以把一个对象拆箱为内置类型。

2.Math 的方法都被定义为 static 形式，通过 Math 类可以在主函数中直接调用。
主要有：**Math.sin, Math.cos, Math.tan, Math.atan, Math.toDegrees**.

#### Number和Math的常用API：

------

**###Value()**: 将 Number 对象转换为xxx数据类型的值并返回。
比如：intValue(), longValue(), doubleValue(), shortValue(), floatValue(), byteValue()，不是静态方法。

------

**compareTo()**：将number对象与参数比较。
语法形式：

```
public int compareTo(NumberSubClass referenceName);
```

这里NumberSubClass可以是Byte, Double, Float, Integer, Short和Long中的一个。
返回值： 若相等返回0，小于（指定小于参数）返回-1， 大于返回1。

------

**equals()**：用于判断 Number 对象与方法的参数是否相等。
语法形式：

```
public boolean equals(Object o);
```

只有类型和值都相等才会返回true，否则返回false。

------

**valueOf()**: 方法用于返回给定参数的原生 Number 对象值，是一个静态方法。
语法形式：

```
static Integer valueOf(int i);
static Integer valueOf(String s);
static Integer valueOf(String s, int redix);//redix表示指定的进制数。
```

比如：

```
Integer x = Integer.valueOf(8);//生成一个值为8的Integer实例。
Double y = Double.valueOf("80");//生成一个值为80.0的Double实例。
Double z = Double.valueOf(80);//生成一个值为80.0的的Double实例。
Integer w = Integer.valueOf("444", 16);//使用16进制。
```

------

**toString**方法：用于返回以一个字符串表示的 Number 对象值。
语法形式有两种，其中一种是静态方法。

```
String toString();
static String toString(int i);
```

比如：

```
Integer x = 5;
x.toString();//返回String对象
Integer.toString(12);//返回String对象
```

------

**parseInt**方法：将字符串参数解析成int整型。
语法形式：

```
static int parseInt(String s);
static int parseInt(String s, int i);//i为进制数
```

这里和valueOf()方法有相同之处————都是静态的，但是两者不同的地方是返回值类型不同，valueOf()返回的是Integer对象，而parseInt则返回一个int整型变量。
举个栗子：

```
int x = Integer.parseInt("9");
Double y = Double.parseDouble("10");//返回值为5.0的double变量
int z = Integer.parseInt("444", 16);//16进制
```

------

**abs**方法：调用形式为Math.abs(x);
**ceil**方法：上舍入（大于等于给定值）
**floor**方法：下舍入（小于等于给定值）
**ceil**和**floor**的语法形式：

```
double ceil(double x);
double ceil(float x);
double floor(double y);
double floor(float y);
```

**rint**方法：返回最接近参数的整数值
语法形式：

```
double rint(double y);
```

**round**方法：四舍五入，算法是Math.floor(x+0.5)。

------

**min**和**max**方法：返回两者之间最小值和最大值。
**exp**方法：Math.exp(x).(另：Math.E表示表示自然对数的底数e。
**log**方法：Math.log(x).
**pow**方法：Math.pow(x, y).返回的是x的y次方。
**sqrt**方法：返回算术平方根。
**toDegrees**方法和**toRadians**方法分别是弧度转换成角度和角度转换成弧度的API。

------

**random()**方法：这是一个产生随机数的静态方法，语法形式：

```
static double random();
```

返回值范围在0.0 =< Math.random < 1.0。

------

### Java Character 类

#### 装箱和拆箱的区别说明

比如：将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱。
再比如：将一个int类型参数转换成Integer对象是装箱，将Integer对象转换成int类型参数是拆箱。

#### 常见的Character类的API

------

**isLetter()**方法：用于判断指定字符是否是字母。
语法形式：

```
public static boolean isLetter(char ch);
```

比如：

```
Character.isLetter('C');//返回值为true.
```

------

**isDigit()**方法：用于判断指定字符是否是数字。
语法形式：

```
public static boolean isDigit(char ch);
```

比如：

```
Character.isDigit('5');//返回值为true.
```

------

**isWhitespace()**方法：用于判断指定字符是否是空白字符，包括：***tab键、空格键和换行符\***。
语法形式：

```
public static boolean isWhitespace(char ch);
```

比如：

```
Character.isWhitespace(' ');//返回true.
Character.isWhitespace('\t');//返回true.
Character.isWhitespace('\n');//返回true.
```

------

**isUpperCase()**方法：用于判断指定字符是否为大写字母。
语法形式：

```
public static boolean isUpperCase(char ch);
```

**isLowerCase()**方法：用于判断指定字符是否为大写字母。
语法形式：

```
public static boolean isLowerCase(char ch);
```

------

**toUpperCase()**方法：用于将小写字符转换成大写。

```
public static char toUpperCase(char ch);
```

比如：

```
Character.toUpperCase('c');//返回字符'C'.
```

**toLowerCase()**方法：用于将小写字符转换成大写。

```
public static char toLowerCase(char ch);
```

比如：

```
Character.toLowerCase('C');//返回字符'c'.
```

------

**toString()**方法：用于返回一个指定char值的String对象。
语法形式：

```
public static String toString(char c);
```

举个栗子：

```
Character.toString('a');//返回一个String对象，值为"a".
```

------

### Java String 类

#### 说明

String 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了。

如果需要对字符串做很多修改，那么应该选择使用 StringBuffer & StringBuilder 类（之前的博客中有介绍）。

#### String类中常用的API

------

**charAt()**方法：用于返回指定索引处的字符。索引范围为从 0 到 length() - 1。
语法形式：

```
public char charAt(int index);
```

比如：

```
String s = "Hello,NJU!";
char c = s.charAt(2);//返回'l'.
```

------

**compareTo()**方法：比较字符串大小。
语法形式：

```
public int compareTo(String anotherString);
```

举个栗子：

```
String str1 = "HelloNJU";
String str2 = "HelloCSU";
str1.compareTo(str2);//返回'N'与'S'的ASCII码差值-5.
str1.compareTo(str1);//返回0
str2.compareTo(str1);//返回5.
```

**compareTo()**方法还有一个孪生兄弟，那就是**compareToIgnoreCase()**，语法上和前者保持一致，主要差别是后者在比较的时候会忽略字母的大小写，举个栗子。

```
String str4 = "HELLONJU";
str1.compareToIgnoreCase(str4);//返回0.
```

------

**concat()**方法：用于连接字符串。
语法形式：

```
public String concat(String s);
```

举个例子：

```
String str1 = "金州勇士";
String str2 = str1.concat("总冠军！");//返回"金州勇士总冠军！".
```

------

**contentEquals()**方法：用于将此字符串与指定的 StringBuffer 比较。
语法形式：

```
public boolean contentEquals(StringBuffer sb);
```

举个例子：

```
String str1 = "String1";
String str2 = "String2";
StringBuffer sb = new StringBuffer(str1);
str1.contentEquals(sb);//返回true.
str2.contentEquals(sb);//返回false.
```

------

**copyValueOf()**方法：将字符数组参数转成成字符串。
语法形式：

```
public static String copyValueOf(char []data);
public static String copyValueOf(char []data, int offset, int count);
```

举个栗子：

```
char []data = new char[]{'H', 'E', 'L', 'L', 'O'};
String str1 = String.copyValueOf(data);//返回字符串"Hello"
String str2 = String.copyValueOf(data, 2, 3);//返回字符串"LLO".
```

------

**endsWith()**方法：判断字符串是否以指定后缀结束。
语法形式：

```
public boolean endsWith(String suffix);
```

举个例子：

```
String str = "HelloNJU";
str.endsWith("NJU");//返回true.
```

同理，还有一个**startsWith()**方法，与**endsWith()**方法不一样的是，它的语法形式还多了一种，可以指定从哪里开始。

------

**equals()**方法：将字符串与指定对象进行比较。
语法形式：

```
public boolean equals(Object o);
```

举个栗子：

```
String str1 = new String("Hexo");
String str2 = str1;
str1.equals(str2);//返回true.
```

和之前的**compareTo()**方法一样，**equals()**方法也有一个孪生兄弟，那就是**equalsIgnoreCase()**方法，即忽略大小写判断是否相等。语法形式上略有不同。

```
public boolean equalsIgnoreCase(String anotherString);//参数数据类型不同.
```

------

**getChars()**方法：将字符从字符串复制到目标字符数组。
语法形式：

```
public void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin);
```

举个栗子：

```
String str = "HelloNJU";
Char[] dst = new char[5];
str.getChars(0, 6, dst, 0)//dst数组变为{'H', 'e', 'l', 'l', 'o'}.
```

------

**hashCode()**方法：返回字符串的哈希码
语法形式：

```
public int hashCode(String s);
```

------

**indexOf()**方法：返回指定字符串中某个字符的下标或子字符串的下标.
语法形式：

```
public int indexOf(int ch);//实际参数使用也可用char c
public int indexOf(int ch, int fromindex);
public int indexOf(String s);
public int indexOf(String s, int fromindex);
```

此外，**lastlndexOf()**方法返回的是从后往前数，指定字符串中某个字符的下标或子字符串的下标，语法形式与**indexOf()**方法类似。

------

**regionMatches()**方法：用于检测两个字符串在一个区域内是否相等。
语法形式：

```
public boolean regionMatches(int toffset, String other, int ooffset, int len);
public boolean regionMatches(boolean IgnoreCase, int toffset, String other, int ooffset, int len);
说明：ignoreCase -- 如果为 true，则比较字符时忽略大小写。
toffset -- 此字符串中子区域的起始偏移量。
other -- 字符串参数。
ooffset -- 字符串参数中子区域的起始偏移量。
len -- 要比较的字符数。
```

举个栗子：

```
String str1 = "HELLONJU";
String str2 = "NJU";
str1.regionMatches(5, str2, 0, 3);//返回true.
```

------

**replace()**方法：换字符串中的字符。
语法形式：

```
public String replace(char oldChar, char newChar);
```

举个例子：

```
String str = "HELLONJU";
str.replace('N', 'S');//返回字符串"HELLOSJU"
```

------

**subSequence()**方法：返回字符串的子序列。
语法形式：

```
public CharSequence subSequence(int beginIndex, int endIndex);
```

------

**subString()**方法：返回字符串的子字符串。
语法形式：

```
public String subString(int beginIndex, int endIndex);
```

举个栗子：

```
String str1 = "HELLONJU";
String str2 = str1.subString(0,5);//返回字符串"HELLO".
****
**toCharArray()**方法：将字符串转换成字符数组
语法形式：
​```java
public Char[] toCharArray();
```

举个栗子：

```
String str1 = "HELLONJU";
char[] chars = str1.toCharArray();
System.out.println(chars);
for(char ch : chars){
    System.out.println(ch);
}
//复习一下数组的输出哈哈哈
```

------

**toUpperCase()**方法：将字符串变成大写。
语法形式：

```
public String toUpperCase();
```

同理，还有**toLowerCase()**方法，将字符串变成小写。

------

**toString()**方法：返回此对象本身。
语法形式：

```
public String toString();
```

举个栗子：

```
String s = new String("HELLONJU");
s.toString();//返回字符串"HELLONJU".
```

------

**trim()**方法：去除字符串首尾空白。
语法形式：

```
public String trim();
```

------

**valueOf()**方法：返回字符串形式，静态方法。
语法形式：

```
public static String valueOf(char[] data);
public static String valueOf(char[] data, int offset, int count);
public static String valueOf(char c);
public static String valueOf(int a);
......
```

------

### Java StringBuffer 类

#### 说明

当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

#### StringBuffer类常用API

------

**append()**方法：将指定的字符串追加到此字符序列。
语法形式：

```
public StringBuffer append(String s);
```

------

**reverse()**方法：将此字符序列用其反转形式取代。
语法形式：

```
public StringBuffer reverse();
```

------

**delete()**方法：移除此序列的子字符串中的字符。
语法形式：

```
public StringBuffer delete(int start, int end);
```

------

**insert()**方法：在原字符序列插入字符。
语法形式：

```
public StringBuffer insert(int offset, int i);//以String.valueOf(i)插入原字符序列的offset处。
```

------

**replace()**方法：使用给定 String 中的字符替换此序列的子字符串中的字符。
语法形式：

```
public StringBuffer replace(int start, int end, String str);
```

