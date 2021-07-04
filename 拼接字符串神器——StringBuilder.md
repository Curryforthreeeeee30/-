# 拼接字符串神器——StringBuilder

### StringBuilder介绍



一般来说，我们拼接字符串时使用的”+”，但是某些情况下有一些缺点，举个栗子：

```
String s = "";
for(int i=0; i<1000; i++){
    s = s + "," + i;
}
```

这种情况下，循环中每次都要创建新的字符串对象，但都是临时对象，所以浪费内存，效率非常低。StringBuilder解决了这个问题，StringBuilder实际上是一个java标准库的类，内置了很多方法，常见的有：

```
.append(), .insert(),  
.delete()
```

### 实例——用StringBuilder构造一条INSERT语句

```
public class Main {
    public static void main(String[] args) {
        String[] fields = { "name", "position", "salary" };
        String table = "employee";
        String insert = buildInsertSql(table, fields);
        System.out.println(insert);
        String s = "INSERT INTO employee (name, position, salary) VALUES (?, ?, ?)";
        System.out.println(s.equals(insert) ? "测试成功" : "测试失败");
    }

    static String buildInsertSql(String table, String[] fields) {
        // TODO:
        StringBuilder stringbuilder = new StringBuilder(10);
        stringbuilder.append("INSERT INTO ")
                     .append(table)
                     .append(" ")
                     .append("(");
        for(int i=0;i<fields.length-1;i++){
             stringbuilder.append(fields[i]);
             stringbuilder.append(", ");        
        }
        stringbuilder.append(fields[fields.length-1]);
        stringbuilder.append(") VALUES (?, ?, ?)");
        String s = new String(stringbuilder);             
        return s;
    }
}
```