# java学习笔记之字符串专栏

### 字符串相等比较



应该使用string.equals()方法，而不是==。如果不在乎大小写的情况下比较字符串相等，使用string.equalsIgnoreCase()方法，举个栗子。

```java
public class stringprac {
	public static void main(String[] args) {
		String s1 = "HELLO";
		String s2 = "hello".toUpperCase();
		String s3 = "hello";
		if(s1 == s2) {
			System.out.println("s1等于s2~");
		}
		if(s1.equals(s2)) {
			System.out.println("s1等于s2!");
		}
		if(s1.equalsIgnoreCase(s3)) {
			System.out.println("s1等于s3^_^");
		}
	}
}
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20161706.png)

### 字符串的一些方法

```java
public class stringprac2 {
	public static void main(String[] args) {
		String s = "StephenCurry";
		System.out.println(s.indexOf("e"));//求索引号
		System.out.println(s.contains("te"));//是否包含某个字串
		System.out.println(s.lastIndexOf("e"));//求最后一次出现的索引号
		System.out.println(s.startsWith("Ste"));//验证开头
		System.out.println(s.endsWith("ry"));//验证结尾
		System.out.println(s.substring(2));//从索引号为2开始的子串
		System.out.println(s.substring(2,6));//从索引号为2开始,6结束（不包括6）的子串
	}
}
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20163327.png)

### 关于去除字符串首尾空白字符

```java
public class stringprac3 {
	public static void main(String[] args) {
		String string = "   \tHello\r\n";
		System.out.println(string.trim());//全部去除	
		String string2 = "  \u3000我Hello爱\n";
		System.out.println(string2.strip());//全部去除，包括类似中文空格字符，这是与trim()方法不同之处。
		System.out.println(string2.stripLeading());//去首
		System.out.println(string2.stripTrailing());//去尾
		
		System.out.println("".isEmpty());//isEmpty()方法检验字符串是否为空
		System.out.println("  ".isEmpty());
		
		System.out.println("  \t\r".isBlank());//isBlank()方放法检验字符串是否为空白字符串
		System.out.println(" Hello ".isBlank());
	}
}
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20164903.png)

### 替换子串

使用replace方法或者正则表达式，正则表达式的方法后续再添加上。

```java
//替换字串
String string3 = "Hello";
System.out.println(string3.replace('H', 'L'));//结果为Lello
System.out.println(string3.replace("ll", "gg"));//结果为Heggo
```

### 分割字符串

使用split方法，传入的是正则表达式。

```java
//分割字符串
String string4 = "A,B,C,D,E";
String[] res = string4.split("\\,");
for(String s: res) {
	System.out.printf("%s\t",s);
}
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20170141.png)

### 拼接字符串

使用**静态方法join()**,举个栗子：

```java
//拼接字符串,使用静态方法join()
String[] string5 = {"Hello", "world", "Go"};
String string6 = String.join("&", string5);
System.out.println(string6);
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20170818.png)

### 格式化字符串

使用字符串实例方法string.formatted()和**静态方法String.format()**，举个栗子。

```java
//格式化字符串
String string7 = "Hello %s, 我是%s, 我今年%d岁了";
System.out.println(String.format(string7, "NJU", "小蓝鲸", 21));
System.out.println(string7.formatted("NJU", "小蓝鲸", 21));
```

运行结果：
![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%89%B9%E6%B3%A8%202020-06-13%20171716.png)

### 类型转换

#### 其他数据类型转字符串型

要把任意基本类型或引用类型转换为字符串，可以使用**静态方法valueOf()**。这是一个*重载方法*，编译器会根据参数自动选择合适的方法。
举个栗子：

```java
String.valueOf(123);//返回"123"
String.valueOf(true)//返回"true"
```

#### 字符串转其他数据类型

如果要把字符串转换成其他类型，可以采用对应类型的parse方法。举个栗子。

```java
Integer.parseInt("123")//返回123
Integer.parseInt("123", 16);//按16进制返回
Boolean.parseBoolean("true");//返回true
```

#### 字符数组和字符串互相转换

```java
char[] arr = "Hello".toCharArray();
String s = new String(arr);
```