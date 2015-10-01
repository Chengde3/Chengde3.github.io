---
layout: post
title: 最小的k个数
date: 2015-08-29
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

输入n个整数，找出其中最小的k个数字。

## 2. 解题思路

思路一（需要修改数组，时间复杂度O(n)）：

- 随机从数组中选择一个数字（或者选择第k个数字），然后调整数组，使得比这个数字大的数字都位于数组的左边，其余的位于右边；
- 如果这个数字在调整后的数组中恰好位于第k位，则可以自己得出结果；
- 如果不是，则分别在两边查找；

思路二（特别适合处理海量数据，时间复杂度O(n*logk)）：

- 使用一个数据容器来存储最小的k个数字；
- 遍历数组，如果容器中数字的个数小于k，则将该元素插入到容器中；
- 如果容器中数字的个数等于k，则比较该元素与容器中的最大元素，然后处理；
- 使用最大堆或者红黑树；

## 3. 参考代码

思路一参考代码：

{% highlight c++ %}
void Swap(int* a, int* b) {
	int tmp = *a;
	*a = *b;
	*b = tmp;
}

int Partition(int data[], int length, int start, int end) {
	if(data == NULL || length <= 0 || start < 0 || end >= length) 
		throw new std::exception("Invalid Parameters");

	int index = RandomInRange(start, end);
	Swap(&data[index], $data[end]);

	int small = start - 1;
	for(index = start; index < end; index++) {
		if(data[index] < data[end]) {
			small++;
			if(small != index)
				Swap(&data[index], &data[small]);
		}
	}

	small++;
	Swap(&data[small], &data[end]);

	return small;
}

void GetLeastNumbers(int* input, int n, int* output, int k) {
	if(input == NULL || output == NULL || k > n || n <= 0 || k <= 0)
		return;

	int start = 0;
	int end = n - 1;
	int index = Partition(input, n, start, end);
	while(index != k-1) {
		if(index > k - 1) {
			end = index;
			index = Partition(input, n, start, end);
		} else {
			start = index;
			index = Partition(input, n, start, end);
		}
	}

	for(int i = 0; i< k; i++)
		output[i] = input[i];
}
{% endhighlight c++ %}

思路二参考代码：

{% highlight c++ %}
typedef multiset<int, greater<int> > intSet;
typedef multiset<int, greater<int> >::iterator setInterator;

void GetLeastNumbers(const vector<int>& data, intSet& leastNumbers, int k) {
	leastNumbers.clear();

	if(k < 1 || data.size() < k) 
		return;

	vector<int>::const_iterator iter = data.begin();
	for(; iter != data.end(); iter++) {
		if((leastNumbers.size()) < k)
			leastNumbers.insert(*iter);
		else {
			setInterator iterGreatest = leastNumbers.begin();

			if(*iter < *(leastNumbers.begin())) {
				leastNumbers.erase(iterGreatest);
				leastNumbers.insert(*iter);
			}
		}
	}
}
{% endhighlight c++ %}

## 4. 思考

- 对于Partition函数仍然无法掌握，需要加强理解以及实践；
- 红黑树以及二叉搜索树没有掌握；
- 本题可以扩展为查找n个数中第k大的数字；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)