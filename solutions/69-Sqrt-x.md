---
layout: postitle into titlecase
title: 69. Sqrt(x)
date: 2022-01-29 10:41:47
tags: 二分查找
categories: Leetcode
---

# 69. Sqrt(x)
## 题目
给你一个非负整数 x ，计算并返回 x 的 算术平方根 。

由于返回类型是整数，结果只保留 整数部分 ，小数部分将被 舍去 。

注意：不允许使用任何内置指数函数和算符，例如 pow(x, 0.5) 或者 x ** 0.5 。

> 示例 1：
>
> 输入：x = 4 
> 输出：2 


> 示例 2：
> 输入：x = 8 
> 输出：2 
> 解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。

## 解题代码C++（核心）

> 本题的核心思路是二分查找 直接用二分查找的套路即可
> 易错点是：不要用mid*mid ==x 去判定，这是因为当x很大的时候，容易出现整数溢出的问题！
> 因此这里用x/mid就会消除这类问题

```cpp
class Solution {
public:
    int mySqrt(int x) {
        int left=1;
        int right=x;
        int mid;
        //二分查找标准步骤
        while(left <= right){
            mid = left + ((right - left) / 2);
            //注意此处，是用x/mid 而不是mid*mid 这是因为要防止整数溢出问题
            if(mid < x/mid) left = mid + 1;
            else if (mid > x/mid) right = mid - 1;
            else return mid;
        }
        //此处 找不到 说明是小数，返回整数部分
        return left-1;
    }
};
```

## 解题代码C++ (本地运行)

> 此处给出的是在本地编译运行的代码，是对leetcode的补充
> 可以在本地直接运行

```cpp
#include <iostream>

using namespace std;


class Solution {
public:
	int mySqrt(int x) {
		int left = 0;
		int right = x;
		int mid;
		while (left <= right) {
			mid = left + ((right - left) / 2);
			if (mid > x / mid) right = mid - 1;
			else if (mid < x / mid) left = mid + 1;
			else return mid;
		}
		return right;
	}
};
int main() {
	cout << "请输入想要开方的值：" << endl;
	int target;
	cin >> target;
	Solution solution;
	cout << solution.mySqrt(target) << endl;
	return 0;
}
```

## 算法效率

> 执行用时：4 ms, 在所有 C++ 提交中击败了53.20%的用户
> 内存消耗：5.8 MB, 在所有 C++ 提交中击败了76.80%的用户
