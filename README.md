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

