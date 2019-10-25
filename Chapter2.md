# 第二章 简单模拟编程实验

生活中，很多现象都具有不确定性质，有些问题很难去建立数学模型，或者很难用计算机建立递推、递归、枚举、回溯等算法，这时一般采取模拟策略。  

所谓模拟就是模拟某个过程，通过改变数学模型的参数，进而观察这些参数的变化所引起的过程状态的变化，并由此展开算法设计。

模拟形式一般有随机模拟和过程模拟。  

**随机模拟**：题目给定，或者隐含某一概率。设计者利用随机函数或取整函数设定某一范围的随机数，将符合概率的随机值作为参数。然后根据这一模拟的数学模型展开算法设计。由于借助了计算机的伪随机数，比真实问题的真实随机变量稍微差些，模拟效果具有不确定因素存在。

**过程模拟**：题目不给出概率，要求设计者按照题意设计数学模型的各种参数，观察参数对过程状态的影响，展开算法设计。模拟效果完全取决于模拟的真实性和算法正确性，不含不确定因素，结果无二义性。本章重点讨论过程模拟。

过程模拟方法一般有三种：  

1）直叙式模拟  

2）筛选法模拟  

3）构造法模拟  

#### 直叙式模拟实验

直叙式模拟只需严格按照题意要求模拟过程即可。模拟对象所包含的动态变化的属性多少决定了难度的大小，动态属性越多，难度越大。

##### 行驶距离的计算

- 题目描述：知道每段时间内的平均时速，求总的行驶路程。

```
Description
Bill and Ted are taking a road trip. But the odometer in their car is broken, so they  
don't know how many miles they have driven. Fortunately, Bill has a working stopwatch, so 
they can record their speed and the total time they have driven. Unfortunately, their   
record keeping strategy is a little odd, so they need help computing the total distance 
driven. You are to write a program to do this computation. 
```

For example, if their log shows 

| Speed in miles per hour | Total elapsed time in hours |
| ----------------------- | --------------------------- |
| 20                      | 2                           |
| 30                      | 6                           |
| 10                      | 7                           |

```
this means they drove 2 hours at 20 miles per hour, then 6-2=4 hours at 30 miles per  
hour, then 7-6=1 hour at 10 miles per hour. The distance driven is then (2)(20) + (4)(30)
+ (1)(10) = 40 + 120 + 10 = 170 miles. Note that the total elapsed time is always since  
the beginning of the trip, not since the previous entry in their log.  

Input
The input consists of one or more data sets. Each set starts with a line containing an 
integer n, 1 <= n <= 10, followed by n pairs of values, one pair per line. The first   
value in a pair, s, is the speed in miles per hour and the second value, t, is the total 
elapsed time. Both s and t are integers, 1 <= s <= 90 and 1 <= t <= 12. The values for  
t are always in strictly increasing order. A value of -1 for n signals the end of the 
input. 

Output
For each input set, print the distance driven, followed by a space, followed by the word 
"miles"

Sample Input
3
20 2
30 6
10 7
2
60 1
30 5
4
15 1
25 2
30 3
10 5
-1

Sample Output
170 miles
180 miles
90 miles
```

- 思想

```
很简单的计算题，假设上一记录驾驶时间为z,当前记录的速度为x,驾驶的时间为y,则当前跑的距离为(y-z)x  
将该距离记入总距离即可。
```

- C++代码

```c++
#include <iostream>
using namespace std;
int main()
{
	int n,x,y,z,ans;  //定义用例中值的个数，当前速度，当前时间，上一时刻时间
	cin >> n;
	while(n > 0)
	{
		ans = z = 0;
		for(int i = 0; i < n; i++)
		{
			cin >> x >> y;
			ans += (y-z) * x;	//总里程
			z = y;	//更新上一时刻时间
		}
		
		cout << ans << " miles" << endl;
		cin >> n;
	}
	return 0;
}
```

##### 行驶时间计算

- 题目描述：跟随某人C从A地到B地，如果在路上发现有比C快的人D，那么就跟随D前往B地，......，问C从A地到B地的时间。

```
Description
Many graduate students of Peking University are living in Wanliu Campus, which is 4.5 
kilometers from the main campus – Yanyuan. Students in Wanliu have to either take a bus 
or ride a bike to go to school. Due to the bad traffic in Beijing, many students choose 
to ride a bike. 

We may assume that all the students except "Charley" ride from Wanliu to Yanyuan at a 
fixed speed. Charley is a student with a different riding habit – he always tries to 
follow another rider to avoid riding alone. When Charley gets to the gate of Wanliu, he 
will look for someone who is setting off to Yanyuan. If he finds someone, he will follow 
that rider, or if not, he will wait for someone to follow. On the way from Wanliu to 
Yanyuan, at any time if a faster student surpassed Charley, he will leave the rider he is 
following and speed up to follow the faster one. 

We assume the time that Charley gets to the gate of Wanliu is zero. Given the set off 
time and speed of the other students, your task is to give the time when Charley arrives 
at Yanyuan. 

Input
There are several test cases. The first line of each case is N (1 <= N <= 10000) 
representing the number of riders (excluding Charley). N = 0 ends the input. The 
following N lines are information of N different riders, in such format: 

Vi [TAB] Ti 

Vi is a positive integer <= 40, indicating the speed of the i-th rider (kph, kilometers
per hour). Ti is the set off time of the i-th rider, which is an integer and counted in 
seconds. In any case it is assured that there always exists a nonnegative Ti. 
Output
Output one line for each case: the arrival time of Charley. Round up (ceiling) the value 
when dealing with a fraction.

Sample Input
4
20	0
25	-155
27	190
30	240
2
21	0
22	34
0

Sample Output
780
771
```



- 思想

```
1.因为C的出发时间从0开始计，因此在一个测试用例中，我们求出最快到达B地的同学，即为C最快到达的时间
2.需要注意的是有些同学的出发时间是从负数开始的，这些数据是无效的：
	(1) 如果提前出发的同学快，则C追不上
	(2) 如果提前出发的同学慢，可以追上，但C不会跟随，因为C本身是快的，不符合跟随的条件
```

- C++代码

```c++
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
	const double DISTANCE = 4.50;
	int n;
	cin >> n;
	while(n)
	{
		double v,t,temp,min = 1e100;	//定义速度(km/h)和时间(s) 定义最小时间	
		 
		for(int i = 0; i < n; ++i)
		{
			cin >> v >> t;
			if(t >=0 && (temp = DISTANCE * 3600 / v + t) < min)
				min  = temp;
		}
		cout << ceil(min) << endl;	//向上取整，向下floor(x)
		cin >> n;	//输入下一组数据
	}
	return 0;
}
```

