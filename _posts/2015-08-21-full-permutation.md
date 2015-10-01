---
layout: post
title: 全排列全组合问题
date: 2015-08-21
categories: Algorithm
tags: algorithm permutation
---

## 1. 问题描述

输入一个字符串，打印出该字符串的所有排列和所有组合；

## 2. 解题思路

### 2.1 全排列问题

- 如果字符没有重复
	- 参考[字符串的排列](http://blog.wangmingkuo.com/string-permutation/)
- 如果字符有重复
	- 从第一个字符起，每个数字分别与它后面非重复出现的数字交换。即，第i个数与第j个数交换时，要求[i,j)中没有与第j个数相等的数字；

### 2.2 全组合问题

- 不考虑重复元素问题

	- 假设原有元素为a,b,c三个，用1表示取该元素，0表示不取，则a表示为001,ab表示为011。000没有意义，所有共有2^n-1个结果；001,010,011,100,101,110,111 。对应输出组合结果为：a,b,ab,c,ac,bc,abc。
	- 用dfs，参考[这篇文章](http://www.cnblogs.com/TenosDoIt/p/3451902.html)

- 考虑重复的元素

	- 修改上面不重复元素的算法； 



## 3. 参考代码

### 3.1 排列算法（字符重复）

{% highlight c++ %}
//递归代码
#include<stdio.h>

void Permutation(char* pStr, char* pBegin);
void Swap(char* str1, char* str2);
bool IsSwap(char* pBegin, char* pEnd);
void Permutation(char* pStr) {
	if(pStr == NULL)
		return;

	Permutation(pStr, pStr);
}

//交换
void Swap(char* str1, char* str2) {
	char temp = *str1;
	*str1 = *str2;
	*str2 = temp;
}

//判断是否交换
bool IsSwap(char* pBegin, char* pEnd) {
	bool result = true; 
	for(char* pTemp = pBegin; pTemp != pEnd; pTemp++) {
		if(*pTemp == *pEnd) {
			result = false;
			break;
		}
	}
	return result;
}

void Permutation(char* pStr, char* pBegin) {
	if(*pBegin == '\0')
		printf("%s\n", pStr);
	else {
		for(char* pCh = pBegin; *pCh != '\0'; pCh++) {
			if(IsSwap(pBegin, pCh)) {
				Swap(pBegin, pCh);
				Permutation(pStr, pBegin + 1);
				//必须再交换回来；因为要保证是第一个字符和后面的每一个字符交换；
				Swap(pBegin, pCh);
			}
		}
	}
}

int main() {
	char str[] = "122";
	Permutation(str);
	return 0;
}

//非递归版；
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

void Swap(char* a, char* b) {
	char t = *a;
	*a = *b;
	*b = t;
}

//反转区间
void Reverse(char* a, char* b) {
	while(a < b)
		Swap(a++, b--);
}

//下一个排列
bool Next_Permutation(char a[]) {
	char* pEnd = a + strlen(a);
	if(a == pEnd)
		return false;

	char* p, *q, *pFind;
	//pEnd--之后指向最后一个元素；
	pEnd--;
	p = pEnd;
	while(p != a) {
		q = p;
		--p;
		if(*p < *q) {
			//找到降序相邻的2个数，前一个数字即为替换数；
			pFind = pEnd;
			while(*pFind <= *p)
				--pFind;
			//替换
			Swap(pFind, p);
			//替换点后的数全部反转
			Reverse(q, pEnd);
			return true;
		}
	}
	//如果没有下一个排列，全部反转后返回true；
	Reverse(p, pEnd);
	return false;
}

int QsortCmp(const void* pa, const void* pb) {
	return *(char*)pa - *(char*)pb;
}

int main() {
	printf("全排列的非递归实现\n");
	char str[] = "dbac";
	printf("%s的全排列如下\n", str);
	//排序
	qsort(str, strlen(str), sizeof(str[0]), QsortCmp);

	int i = 1;
	do {
		printf("第%3d个排列\t%s\n", i++, str);
	} while(Next_Permutation(str));

	return 0;
}
{% endhighlight c++ %}


### 3.2 全组合算法（字符没有重复）

**解法一：用位图的方式；**

{% highlight c++ %}
#include<stdio.h>
#include<string.h>

void Combination(char* str) {
	if(str == NULL)
		return;

	int len = strlen(str);
	int n = 1 << len;
	for(int i = 1; i < n; i++) {
		//从1循环到2^len-1
		for(int j = 0; j < len; j++) {
			int temp = i;
			if(temp & (1 << j)) //对应位上为1，则输出对应的字符
				printf("%c", *(str+j));
		}
		printf("\n");
	}
}

int main() {
	char str[] = "abc";
	Combination(str);
	return 0;
}
{% endhighlight c++ %}


**解法二，dfs方法，递归**
{% highlight c++ %}
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class Solution {
	private:
		vector<vector<int> >res;

	public:
		//void des(vector<int> &s, int iend, vector<int> &tmpres);
		vector<vector<int> > subSets(vector<int> &s) {
			//先排序，然后dfs每个元素选或者不选，最后叶子结点就是所有解
			res.clear();
			sort(s.begin(), s.end());
			vector<int> tmpres;
			dfs(s, 0, tmpres);
			return res;
		}

		void dfs(vector<int> &s, int iend, vector<int> &tmpres) {
			if(iend == s.size()) {
				res.push_back(tmpres);
				return;
			}
			//选择s[iend]
			tmpres.push_back(s[iend]);
			dfs(s, iend+1, tmpres);
			tmpres.pop_back();
			//不选择s[iend]
			dfs(s, iend+1, tmpres);
		}
};

int main() {
	Solution solu;
	vector<int> input;
	vector<vector<int> > output;
	for(int i = 1; i < 4; i++) {
		input.push_back(i);
	}

	output = solu.subSets(input);
	for(int i = 0; i < output.size(); i++) {
		for(int j = 0; j < output[i].size(); j++) {
			cout << output[i][j];
		}
		cout << "\n";
	}

	return 0;
}
{% endhighlight c++ %}


**解法三，非递归；**

{% highlight c++ %}
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class Solution {
	public:
		vector<vector<int> > subsets(vector<int> &s) {
			int len = s.size();
			sort(s.begin(), s.end());
			//开始加入一个空集
			vector<vector<int> > res(1);

			for(int i = 0; i < len; i++) {
				int resSize = res.size();
				for(int j = 0; j < resSize; j++) {
					//把每个元素依次弹出，再重新压入vector中；
					res.push_back(res[j]);
					//在最后一个元素里面添加当前元素
					res.back().push_back(s[i]);
				}
			}
			return res;
		}
};

int main() {
	Solution solu;
	vector<int> input;
	vector<vector<int> > output;
	for(int i = 1; i < 4; i++) {
		input.push_back(i);
	}

	output = solu.subsets(input);
	
	for(int i = 0; i < output.size(); i++) {
		for(int j = 0; j < output[i].size(); j++) {
			cout << output[i][j];
		}
		cout << "\n";
	}
	return 0;
}
{% endhighlight c++ %}


### 3.3 组合算法（有重复数字）

**解法一，dfs**
{% highlight c++ %}
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class Solution {
	private:
		vector<vector<int> > res;
	public:
		vector<vector<int> > subsetsWithDup(vector<int> &s) {
			//先排序，然后dfs每个元素选或者不选，最后叶子结点就是所有解
			res.clear();
			sort(s.begin(), s.end());
			vector<int> tmpres;
			dfs(s, 0, tmpres);
			return res;
		}

		void dfs(vector<int> &s, int iend, vector<int> &tmpres) {
			if(iend == s.size()) {
				res.push_back(tmpres);
				return;
			}
			int firstSame = iend;
			while(firstSame >= 0 && s[firstSame] == s[iend])
				firstSame--;
			//firstSame是第一个和s[iend]相同的数字；
			firstSame++;
			//和s[iend]相同数字的个数（除自己）
			int sameNum = iend - firstSame;
			if(sameNum == 0 || (tmpres.size() >= sameNum && tmpres[tmpres.size()-sameNum] == s[iend])) {
				//选择s[iend]
				tmpres.push_back(s[iend]);
				dfs(s, iend+1, tmpres);
				tmpres.pop_back();
			}
			
			//不选择s[iend]
			dfs(s, iend+1, tmpres);
		}
};


int main() {
	Solution solu;
	vector<int> input;
	vector<vector<int> > output;
	input.push_back(1);
	input.push_back(2);
	input.push_back(2);
	input.push_back(2);

	output = solu.subsetsWithDup(input);
	
	for(int i = 0; i < output.size(); i++) {
		for(int j = 0; j < output[i].size(); j++) {
			cout << output[i][j];
		}
		cout << "\n";
	}
	return 0;
}
{% endhighlight c++ %}

**解法二，非递归**

{% highlight c++ %}
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class Solution {
	private:
		vector<vector<int> > res;
	public:
		vector<vector<int> > subsetsWithDup(vector<int> &s) {
			int len = s.size();
			sort(s.begin(), s.end());
			//开始加入一个空集
			vector<vector<int> > res(1);
			//上一个数字，即将要进行操作的子集数量
			int last = s[0], opResNum = 1;
			for(int i = 0; i < len; i++) {
				if(s[i] != last) {
					last = s[i];
					opResNum = res.size();
				}

				//如果有重复数字，即将操作的子集数目和上次相同；
				//如果有重复数字，只需要操作后面的几个vector就可以了
				//可以参考http://bangbingsyb.blogspot.com/2014/11/leetcode-subsets-i-ii.html
				int resSize = res.size();
				for(int j = resSize - 1; j >= resSize - opResNum; j--) {
					res.push_back(res[j]);
					res.back().push_back(s[i]);
				}
			}
			return res;
		}
};


int main() {
	Solution solu;
	vector<int> input;
	vector<vector<int> > output;
	input.push_back(1);
	input.push_back(2);
	input.push_back(2);
	input.push_back(2);

	output = solu.subsetsWithDup(input);
	
	for(int i = 0; i < output.size(); i++) {
		for(int j = 0; j < output[i].size(); j++) {
			cout << output[i][j];
		}
		cout << "\n";
	}
	return 0;
}
{% endhighlight c++ %}

## 4. 思考



## 5. 参考

- [STL系列之十 全排列(百度迅雷笔试题)](http://blog.csdn.net/morewindows/article/details/7370155)(主要参考文献)
- [[LeetCode] Next Permutation 解题报告](http://fisherlei.blogspot.com/2012/12/leetcode-next-permutation.html)(里面对next_permutation描述的较为详细)
- [全排列和全组合实现](http://wuchong.me/blog/2014/07/28/permutation-and-combination-realize/)(全组合算法主要参考文献)
- [[LeetCode] Subsets I, II](http://bangbingsyb.blogspot.com/2014/11/leetcode-subsets-i-ii.html)(全组合算法主要参考文献，更好理解，力荐)
- [《剑指offer》](http://www.broadview.com.cn/#book/bookdetail/bookDetailAll.jsp?book_id=12c9bc27-a944-11e4-9c0a-005056c00008&isbn=978-7-121-23245-9)