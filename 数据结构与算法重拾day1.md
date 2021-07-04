# 数据结构与算法重拾day1

## 数据结构的分类

### 线性结构

线性结构主要包括：数组、队列、链表和栈。

### 非线性结构

非线性结构主要包括二维数组、多维数组、广义表、树结构和图结构。

## 稀疏数组

### 稀疏数组的定义

当一个数组大部分元素为0时，为了压缩数组的存储空间，可以考虑使用稀疏数组来保存。
稀疏数组的结构是：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E7%A8%80%E7%96%8F%E6%95%B0%E7%BB%84%E7%9A%84%E7%BB%93%E6%9E%84.png)

整体思路分析如下：

![img](https://gitee.com/Curryforthreeeeee30/HexoPicture/raw/master/img/%E6%95%B4%E4%BD%93%E6%80%9D%E8%B7%AF%E5%88%86%E6%9E%90.png)

### 稀疏数组的实现（java语言）

代码实现如下：

```java
public class sparseArr {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		//创建原始数组
		int[][] chessArr_ori = new int[11][11];
		chessArr_ori[0][1] = 1;
		chessArr_ori[1][2] = 2;
		
		//打印原始数组
		System.out.println("这是原始数组：");
		for(int[] arr : chessArr_ori) {
			for(int arr2 : arr) {
				System.out.printf("%d\t",arr2);
			}
			System.out.println();
		}
		
		//创建稀疏数组
		//1.数清楚有多少个非0的数
		//2.将非零数塞进稀疏数组中
		int sum = 0;
		for(int[] arr : chessArr_ori) {
			for(int arr2 : arr) {
				if(arr2 != 0) {
					sum++;
				}
			}
		}
		System.out.printf("原始数组中有%d个数不为0", sum);
		System.out.println();
		
		int [][] sparseArr = new int[sum+1][3];
		sparseArr[0][0] = chessArr_ori.length;
		sparseArr[0][1] = chessArr_ori.length;
		sparseArr[0][2] = sum;
		
		int count = 0;
		for(int i = 0; i < chessArr_ori.length; i++) {
			for(int j = 0; j < chessArr_ori.length; j++) {
				if(chessArr_ori[i][j] != 0) {
					count++;
					sparseArr[count][0] = i;
					sparseArr[count][1] = j;
					sparseArr[count][2] = chessArr_ori[i][j];
				}
			}
		}
		
		//打印稀疏数组
		System.out.println("这是稀疏数组：");
		for(int[] arr3 : sparseArr) {
			for(int arr4 : arr3) {
				System.out.printf("%d\t",arr4);
			}
			System.out.println();
		}
		
		//稀疏数组还原成原始数组
		//1.提取原始数组的行数和列数，创建恢复数组；
		//2.将稀疏数组中非零数塞进恢复数组。
		int [][] chessArr_back = new int [sparseArr[0][0]][sparseArr[0][1]];
		for(int m = 1; m < sum+1; m++) {
			chessArr_back[sparseArr[m][0]][sparseArr[m][1]] = sparseArr[m][2];		
		}
		
		//打印恢复数组
		System.out.println("这是恢复数组：");
		for(int[] arr5 : chessArr_ori) {
			for(int arr6 : arr5) {
				System.out.printf("%d\t",arr6);
			}
			System.out.println();
		}
			
	}

}
```