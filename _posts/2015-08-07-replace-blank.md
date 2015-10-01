---
layout: post
title: 空格替换
date: 2015-08-07
categories: Algorithm
tags: algorithm 剑指offer
---

## 1. 问题定义

实现一个函数，把字符串中的每个空格替换成“%20”。例如输入，“We are happy.”，输出“We%20are%20happy.”。

注：字符串的总容量大于输出字符串的大小。

## 2. 解题思路

一般的想法是遍历字符串，遇到空格把之后的所有字符串向后移动；但是这样的时间复杂度为O(n^2)；

另一种思路如下：

- 计算得到新的字符串的大小（原始字符串 + 2 * 空格数）。
- 设置两个指针，p1指向新字符串末尾，p2指向原始字符串末尾;
- p1向前移动，如果没遇到空格，把所指向的字符赋值给p2的位置；如果遇到空格，则依次把0,2,%赋值给p2所指向的位置；

## 3. 参考代码

{% highlight c %}
#include<stdio.h>

//length为字符数组string的总容量
void ReplaceBlank(char string[], int length) {
	//特殊输入测试	
	if(string == NULL || length <= 0) 
		return;

	//originalLength为字符串string的实际长度
	int originalLength = 0;
	int numberOfBlank = 0;
	int i = 0;
	//计算原始字符串大小以及空格数量
	while(string[i] != '\0') {
		if(string[i] == ' ')
			numberOfBlank++;
		originalLength++;
		i++;
	}
	
	//newLength为把空格替换成'%20'之后的长度
	int newLength = originalLength + 2 * numberOfBlank;
	if(newLength > length) 
		return;
	
	//从后向前替换；
	int indexOfOriginal = originalLength;
	int indexOfNew = newLength;
	while(indexOfOriginal >= 0 && indexOfNew > indexOfOriginal) {
		if(string[indexOfOriginal] == ' ') {
			string[indexOfNew--] = '0';
			string[indexOfNew--] = '2';
			string[indexOfNew--] = '%';
		} else {
			string[indexOfNew--] = string[indexOfOriginal];
		}

		indexOfOriginal--;
	}
}

int main() {
	char string[] = "hello world!";
	int length = 100;
	ReplaceBlank(string, length);
	printf("%s\n", string);
	return 0;
}
{% endhighlight c %}

## 4. 思考

可以从前向后遍历，自然也可以从后向前遍历；有时候正着不可以，可以反着尝试一下；

## 5. 扩展

### 5.1 题目

有两个排序的数组A1和A2,内存在A1的末尾有足够多的空余空间容纳A2。实现一个函数，把A2中的所有数字插入到A1中并且所有的数字是排序的；

### 5.2 思路

从尾到头比较A1和A2中的数字，并把较大的数字复制到A1中的合适位置

### 5.3 代码

{% highlight c %}
#include<stdio.h>
#include<malloc.h>

void sortTwoArray(int *a1, int a1_size, int *a2, int a2_size) {

	int indexNew = a1_size + a2_size - 1;
	int *temp = (int*)malloc(sizeof(int) * (indexNew + 1)); 

	int indexA1 = a1_size - 1;
	int indexA2 = a2_size - 1;

	while(indexA1 >= 0 && indexA2 >= 0) {
		if(a1[indexA1] > a2[indexA2]){
			temp[indexNew--] = a1[indexA1--];
		} else {
			temp[indexNew--] = a2[indexA2--];
		}
	}

	while(indexA1 >= 0) {
		temp[indexNew--] = a1[indexA1--];
	}

	while(indexA2 >= 0) {
		temp[indexNew--] = a2[indexA2--];
	}

	for(int i = 0; i <= 10; i++) {
		a1[i] = temp[i];
	}
}

int main() {
	int a1[11] = {1,2,3,4,5,5};
	int a2[4] = {3,3,4,5};
	sortTwoArray(a1, 6, a2, 4);
	int i = 0;
	printf("\n");
	while(i < 11) {
		printf("%d\t", a1[i]);
		i++;
	}
	return 0;
}
{% endhighlight c %}

### 5.4 思考

区分指针和引用的区别；

- [c++中的指针和引用](http://blog.wangmingkuo.com/pointer-and-reference/)

## 6. 参考文献

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)