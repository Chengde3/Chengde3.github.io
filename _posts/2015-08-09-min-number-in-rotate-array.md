---
layout: post
title: 旋转数组中的最小数字
date: 2015-08-09
categories: Algorithm
tags: algorithm array
---

## 1. 问题定义

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素；例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。

## 2. 解题思路

利用二分查找法实现logn时间复杂度的查找，思路如下：

- 如果数组中间的元素 >= 开始的元素，则中间元素位于前面的递增子数组，最小元素位于中间元素的后面；
- 如果数组中间的元素 <= 结束的元素，则中间元素位于后面的递增子数组，最小元素位于中间元素的前面；
- 如果数组中间元素 = 数组开始元素 = 数组结束元素，无法判断最小元素位置，则需要顺序查找；


## 3. 参考代码

{% highlight c++ %}
#include<iostream>
#include<exception>
using namespace std;

int MinInOrder(int* numbers, int index1, int index2);

int Min(int* numbers, int length) {
	if(numbers == NULL || length <= 0)
   		throw new std::exception();

	int index1 = 0;
	int index2 = length-1;
	//如果数组已经是排好序的，第一个数组就是最小的数字，因此indexMid初始为index1；
	int indexMid = index1;

	while(numbers[index1] >= numbers[index2]) {
		//循环结束条件
		if(index2 - index1 == 1) {
			indexMid = index2;
			break;
		}
		indexMid = (index1 + index2) / 2;

		//如果下标为index1,index2,indexMid指向的三个数字相等，则只能顺序查找;
		if(numbers[index1] == numbers[indexMid] && numbers[index1] == numbers[index2]) {
			return MinInOrder(numbers, index1, index2);
		}
		
		//缩小查找范围
		if(numbers[indexMid] >= numbers[index1])
			index1 = indexMid;
		else if(numbers[indexMid] <= numbers[index2])
			index2 = indexMid;
	}	
	return numbers[indexMid];
}

int MinInOrder(int* numbers, int index1, int index2) {
	int result = numbers[index1];
	for(int i = index1+1; i < index2; i++) {
		if(result > numbers[i]) {
			result = numbers[i];
		}
	}
	return result;
}

int main() {
	int numbers[5] = {3,4,5,1,2};
	int numbers1[5] = {1,0,1,1,1};
	int numbers2[5] = {1,1,1,0,1};
	cout << Min(numbers, 5) << endl;
	cout << Min(numbers1, 5) << endl;
	cout << Min(numbers1, 5) << endl;
	return 0;
}
{% endhighlight c++ %}

## 4. 注意事项

需要考虑两个特殊的示例：

- 数组已经排好序；可以直接返回；
- 前中后元素都相等，比如10111,11101。无法判断最小数字位于那个递增子数组；

## 5. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)