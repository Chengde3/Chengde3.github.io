---
layout: post
title: 字符流中第一个不重复的字符
date: 2015-09-08
categories: Algorithm
tags: algorithm
---

## 1. 问题描述

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如当从字符流中只读出前两个字符“go”时，第一个只出现一次的字符是‘g’。当从该字符流中读出前六个字符“google”时，第一个只出现一次的字符是'l'

## 2. 解题思路

- 字符只能一个接着一个从字符流中读出来。
- 定义一个数据容器来保存字符在字符流中的位置。当一个字符第一次从字符流中读出时，把它在字符流中的位置保存到数据容器里；
- 当这个字符再次从字符流中读出时，这时把数据容器中的值更新成一个特殊的值（比如负数值）
- 数据容器可以用哈希表来实现，用字符的ASCII码作为哈希表的键值，而把字符对应的位置作为哈希表的值；


## 3. 参考代码

{% highlight c++ %}

class CharStatistics {
	public:
		CharStatistics() : index(0) {
			//初始化
			for(int i = 0; i < 256; i++)
				occurrence[i] = -1;
		}

		void Insert(char ch) {
			//只出现一次的字符的值赋为index，index逐渐增大；也就是说，第一个不重复的字符其index是最小的；
			if(occurrence[ch] == -1)
				occurrence[ch] = index;
			//出现多次的情况；
			else if(occurrence[ch] >= 0)
				occurrence[ch] = -2;

			index++;
		}

		char FirstAppearingOnce() {
			char ch = '\0';
			int minIndex = numric_limits<int>::max();
			//找到数组值大于0，同时数组值最小的字符；
			for(int i = 0; i < 256; i++) {
				if(occurrence[i] >= 0 && occurrence[i] < minIndex) {
					ch = (char)i;
					minIndex = occurrence[i];
				}
			}
			return  char;
		}

	private:
		//occurrence[i]: A character with ASCII value i;
		//occurrence[i] = -1; The character has not found;
		//occurrence[i] = -2; The character has been found for multiple times
		//occurrence[i] >= 0: The character has been found only once
		int occurrance[256];
		int index;
};
{% endhighlight c++ %}

## 4. 思考

- 哈希表的字符数组的实现方式；

## 5. 参考

- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)