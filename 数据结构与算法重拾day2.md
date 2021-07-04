# 数据结构与算法重拾day2

## 队列的介绍

### 队列有哪些特点

1、队列是一个有序列表，可以由数组或者链表来实现。
2、队列遵循”先进先出，后进后出”的原则。比如用数组来实现的时候，队列有两个指针，一个是front，另一个是rear。当加入数据到队列时，rear指针加一；当从队列取出数据的时候，front指针加一。

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E9%98%9F%E5%88%97%E4%BB%8B%E7%BB%8D.png)

### 队列空与队列满怎么判断

#### 队列满

rear = maxSize - 1;

#### 队列空

rear = front;

### 实例-利用数组来模拟队列的实现

```java
import java.util.Scanner;
public class Queue {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Isqueue queue = new Isqueue(3);
		Scanner scanner = new Scanner(System.in);
		boolean loop = true;
		while(loop) {
			System.out.println("s(显示队列)");
			System.out.println("a(为队列添加数据)");
			System.out.println("g(从队列中取出数据)");
			System.out.println("e(退出程序)");
			System.out.println("h(查看队列头数据)");
			System.out.println("请输入s/a/g/e/h中的一个：");
			char choice = scanner.next().charAt(0);
			
			switch(choice) {
			case 's':
				queue.showArr();
				break;
			case 'a':
				try {
					System.out.println("输入一个数：");
					int num = scanner.nextInt();
					queue.addArr(num);
				}catch(Exception e) {
					System.out.println(e.getMessage());
				}
				break;
			case 'g':
				try{
					int res = queue.getArr();
					System.out.printf("取出的数据是%d\n",res);
				}catch(Exception e){
					System.out.println(e.getMessage());
				}
				break;
			case 'e':
				loop = false;
				break;
			case 'h':
				try{
					int res = queue.HeadArr();
					System.out.printf("队列的头数据是%d\n",res);
				}catch(Exception e){
					System.out.println(e.getMessage());
				}
				break;
			default:
				break;
			}
		}
		System.out.println("退出程序啦~~");		
	}

}

class Isqueue{
	private int arrSize;
	private int front;
	private int rear;
	private int[] Arr;
	
	//创建队列
	public Isqueue(int maxSize) {
		 this.arrSize = maxSize;
		 Arr = new int[maxSize];
		 front = -1;
		 rear = -1;
	}
	
	//判断队列是否满
	public boolean isFull() {
		return rear == arrSize - 1;
	}
	
	//判断队列是否空
	public boolean isEmpty() {
		return front == rear;
	}
	
	//添加数据到队列
	public void addArr(int n) {
		if(isFull()) {
			System.out.println("队列是满的，不能添加数据~~");
		}
		rear++;
		Arr[rear] = n;
	}
	
	//从队列中取出数据
	public int getArr() {
		if(isEmpty()) {
			 throw new RuntimeException("队列是空的，无法取出数据~~");
		}
		front++;
		return Arr[front];
	}
	
	//显示队列的头数据
	public int HeadArr() {
		if(isEmpty()) {
			 throw new RuntimeException("队列是空的，无法显示头数据~~");
		}
		return Arr[front+1];
	}
	
	//显示队列所有数据
	public void showArr() {
		if(isEmpty()) {
			System.out.println("队列为空，没有数据哦~~");
		}
		for(int i = 0; i < Arr.length; i++) {
			System.out.printf("Arr[%d]=%d\n", i, Arr[i]);
		}
	}
}
```

#### 对代码的解读

首先创建一个类，这个类就是用数组来模拟队列。变量字段有maxSize、front、rear和Arr数组。下面就是写模拟队列的函数。
**第一步就是创建队列**，引入参数（数组的大小），赋值给数组，然后初始化front指针和rear指针（均设置为-1）；**第二步是判断队列是否为空和是否为满**，是否为空的条件是rear和front指针相等，是否为满的条件是rear指针等于maxSize-1；**第三步是写添加数据到队列的函数**，先要判断队列是否为满，如果满的话打印提示信息，否则先将rear++，然后将添加的数值赋给Arr[rear]；**第四步是写从队列中取出数据的函数**，先要判断队列是否为空，如果为空抛出一个异常RuntimeException，否则将front++，然后返回Arr[front]的值；**第五步是写返回队列头数据的函数**，同样要先判断队列是否为空，如果为空，抛出异常RuntimeException，否则返回Arr[front+1]；**第六步是写一个函数来显示队列中所有的数据**，先要判断队列是否为空，如果为空就抛出异常RuntimeException，否则就遍历数组。