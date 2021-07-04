# java学习笔记之面向对象基础

### 静态字段与静态方法

#### 静态字段

静态字段是为类所拥有的，不为实例所拥有，在代码中，实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为类名.静态字段来访问静态对象。

```java
public class Static {
	public static void main(String[] args) {
		St student1 = new St(16, "小明");
		St student2 = new St(12, "小红");
		student1.number = 17;
		System.out.println(student2.number);//实例.字段
		student2.number = 20;
		System.out.println(student1.number);//实例.字段
		System.out.println(St.number);//类名.字段
	}
}

class St{
	public int age;
	public String name;
	public static int number;
	
	public St(int age, String name) {
		this.age = age;
		this.name = name;
	}
	
}
```

#### 静态方法

静态方法则只能访问静态字段，不能访问非静态的实例字段，因此不能使用this指针。静态方法也是为类所拥有，常用于工具类的函数中，比如Math.random()。

```java
import java.util.Scanner;

public class Static_practice {
	public static void main(String[] args) {
		
		Scanner scanner = new Scanner(System.in);
		boolean loop = true;
		while(loop) {
			System.out.println("(a)增加一个实例");
			System.out.println("(b)查看实例的个数");
			System.out.println("(e)退出");
			
			char key = scanner.next().charAt(0);
			
			switch (key) {
			case 'a': 
				new Person_S(12, "Curry");
				break;
			case 'b':
				System.out.println(Person_S.getCount());
				break;
			case 'e':
				loop = false;
				System.out.println("退出程序");
				break;
			default:
				throw new IllegalArgumentException("Unexpected value: " + key);
			}
		}
	}
}

class Person_S{
	private int age;
	private String name;
	private static int count;
	
	public Person_S(int age, String name) {
		this.name = name;
		this.age = age;
	}
	
	public static int getCount() {
		count++;
		return count;
	}
}
```