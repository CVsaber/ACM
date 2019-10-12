# ACM
ACM撸啊撸，一直撸，一直爽

### 第一章 简单计算编程

掌握C++基本语法格式

###### 1. 牛刀小试：计算平均工资

- 题目描述：

```
Description

Larry graduated this year and finally has a job. He's making a lot of money, but somehow never seems to have enough. Larry has decided that he needs to grab hold of his financial portfolio and solve his financing problems. The first step is to figure out what's been going on with his money. Larry has his bank account statements and wants to see how much money he has. Help Larry by writing a program to take his closing balance from each of the past twelve months and calculate his average account balance.
Input

The input will be twelve lines. Each line will contain the closing balance of his bank account for a particular month. Each number will be positive and displayed to the penny. No dollar sign will be included.
Output

The output will be a single number, the average (mean) of the closing balances for the twelve months. It will be rounded to the nearest penny, preceded immediately by a dollar sign, and followed by the end-of-line. There will be no other spaces or characters in the output.
Sample Input

100.00
489.12
12454.12
1234.10
823.05
109.20
5.27
1542.25
839.18
83.99
1295.01
1.75
Sample Output

$1581.42
```

- 思路：

```
简单的输入-处理-输出模式，只要注意小数位和前面的单位即可
测试平台：北大POJ-1004
```

- C++实现：

```
# 实现
#include<iostream>
#include <iomanip> 
using namespace std;
int main()
{
	float avg, sum = 0.0, a[12] = {0};	//定义
	int i;
	for(i = 0; i < 12; i++)
	{
		cin >> a[i];
		sum += a[i];
	}
	avg = sum/12;
	cout <<'$' << fixed << setprecision(2) << avg;
	return 0;
}
```

###### 2.牛刀小试：多测试用例

- 题目描述：给定2~15个正整数，计算有多少对满足一个是另一个的两倍。

```
Description
As part of an arithmetic competency program, your students will be given randomly generated lists of from 2 to 15 unique positive integers and asked to determine how many items in each list are twice some other item in the same list. You will need a program to help you with the grading. This program should be able to scan the lists and output the correct answer for each one. For example, given the list 
1 4 3 2 9 7 18 22
your program should answer 3, as 2 is twice 1, 4 is twice 2, and 18 is twice 9. 
Input
The input will consist of one or more lists of numbers. There will be one list of numbers per line. Each list will contain from 2 to 15 unique positive integers. No integer will be larger than 99. Each line will be terminated with the integer 0, which is not considered part of the list. A line with the single number -1 will mark the end of the file. The example input below shows 3 separate lists. Some lists may not contain any doubles.
Output
The output will consist of one line per input list, containing a count of the items that are double some other item.
Sample Input
1 4 3 2 9 7 18 22 0
2 4 8 10 0
7 5 11 13 1 3 0
-1
Sample Output
3
2
0
```

- 思路：

```
包含多测试用例。需要循环处理每个用例
1.通过一层循环读取当前测试用例的数组a
2.通过两层循环结构，判断是否满足一个是另一个两倍
```

- C++实现

```C++
#include<iostream>
using namespace std;

int main()
{
	int a[20];  //整型数组，存储测试用例
	cin >> a[0];
	while(a[0] != -1)	//整个输入的结束标志
	{
		int n = 1;
		for (;;n++)
		{
			cin >> a[n];
			if(a[n] == 0)
				break;	//单行测试用例的结束标志
		}
		
		int count = 0;	//当前测试用例中有多少对满足条件
		for(int i = 0; i < n-1; i++)
		{
			for(int j = i+1; j <n; j++)
			{
				if (a[i]*2 == a[j] || a[i] == a[j]*2)
					count++;	//满足条件，加1
			}
		}
		cout << count << endl;	//输出结果
		cin >> a[0];	//输入下一个测试用例
	}
	return 0;
}
```

