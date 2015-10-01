---
layout: post
title: n个色子的点数
date: 2015-09-01
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

把n个色子扔在地上，所有色子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率；

## 2. 解题思路

思路一：递归

- 把n个色子分为两堆，第一堆只有一个，第二堆有n-1个；计算单独那一个1-6的点数与n-1个色子的点数之和；
- 对n-1个那一堆也做这样处理；

思路二：循环

递归需要有大量重复的计算，会影响性能；

- 设置两个数组来存储色子点数的每一个总数出现的次数。
- 一次循环中，第一个数组中的第n个数字表示色子和为n出现的次数；
- 下一次循环中，加上一个新的色子，此时和为n的色子出现的次数等于上一次循环中色子点数和为n-1,n-2,n-3,n-4,n-5,n-6的次数的中和；
- 交换两个数组，继续循环；

## 3. 参考代码

//递归参考代码
{% highlight c++ %}
int g_maxValue = 6;
void Probability(int number, int* pProbabilities);
void Probability(int original, int current, int sum, int *pProbabilities);

void PrintProbability(int number) {
	if(number < 1)
		return;

	int maxSum = number * g_maxValue;
	int* pProbabilities = new int[maxSum - number + 1];
	for(int i = number; i <= maxSum; i++) 
		pProbabilities[i-number] = 0;

	Probability(number, pProbabilities);

	int total = pow((double)g_maxValue, number);
	for(int i = number; i <= maxSum; i++) {
		double ratio = (double)pProbabilities[i-number] / total;
		printf("%d: %e\n", i, ratio);
	}

	delete[] pProbabilities;
}

void Probability(int number, int* pProbabilities) {
	for(int i = 1; i <= g_maxValue; i++) 
		Probability(number, number, i, pProbabilities);
}

void Probability(int original, int current, int sum, int* pProbabilities) {
	if(current == 1) {
		pProbabilities[sum-original]++;
	} else {
		for(int i = 1; i <= g_maxValue; i++) {
			Probability(original, current-1, i+sum, pProbabilities);
		}
	}
}
{% endhighlight c++ %}

//循环参考代码
{% highlight c++ %}
int g_maxValue = 6;
void PrintProbability(int number) {
	if(number < 1) 
		return;

	//初始化
	int* pProbabilities[2];
	pProbabilities[0] = new int[g_maxValue * number + 1];
	pProbabilities[1] = new int[g_maxValue * number + 1];
	for(int i = 0; i < g_maxValue * number + 1; i++) {
		pProbabilities[0][i] = 0;
		pProbabilities[1][i] = 0;
	}
	
	//第一个色子
	int flag = 0;
	for(int i = 1; i <= g_maxValue; i++) 
		pProbabilities[flag][i] = 1;

	for(int k = 2; k <= number; k++) {
		//k个色子最小也为k
		for(int i = 0; i < k; i++) {
			pProbabilities[1-flag][i] = 0;
		}

		for(int i = k; i <= g_maxValue * k; i++) {
			pProbabilities[1-flag][i] = 0;
			//j <= i保证i-j >= 0;
			for(int j = 1; j <= i && j < g_maxValue; j++) 
				pProbabilities[1-flag][i] += pProbabilities[flag][i-j];
		}
		flag = 1 - flag;
	}
	
	double total = pow((double)g_maxValue, number);
	for(int i = number; i <= g_maxValue * number; i++) {
		double ratio = (double)pProbabilities[flag][i] / total;
		printf("%d: %e\n", i, ratio);
	}

	delete[] pProbabilities[0];
	delete[] pProbabilities[1];
}
{% endhighlight c++ %}
## 4. 思考

递归啊递归！！！

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)