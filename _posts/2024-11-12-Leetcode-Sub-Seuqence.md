---
title: LEETCODE - 子数组和相关问题
author: Boron
date: 2024-11-12 14:08:00 +0100
categories: [Blogs, Coding]
tags: [C++, Coding, 算法]
---

# **子数组问题总结**

- **滑动窗口** 和 **前缀和 + 哈希表** 是处理大多数**连续子数组**问题的首选方法，因为其时间复杂度通常是 **O(n)**。
- **动态规划** 主要用于**最大子数组和、最大积**等最优子数组问题。
- **单调队列 / 单调栈** 适合处理需要**快速查找最值**的窗口问题。
- **分治法** 和 **二分查找** 适用于需要**分解问题**或**有序查找**的场景。
- **双指针** 通常用于在**有序数组**中查找满足条件的子数组问题。

| 解法分类                               | 适用场景                         | 常见问题                                                               | 解题思路                                     |
| -------------------------------------- | -------------------------------- | ---------------------------------------------------------------------- | -------------------------------------------- |
| 滑动窗口 (Sliding Window)              | 连续子数组问题                   | 长度最小的子数组 (209), 和为 K 的子数组 (560), 最长无重复子数组 (3)    | 使用双指针调整窗口边界，找到满足条件的子数组 |
| 前缀和 + 哈希表 (Prefix Sum)           | 计算子数组和                     | 和为 K 的子数组 (560), 和相等的二元子数组 (930), 子数组和为奇数 (1524) | 维护前缀和数组，用哈希表快速查找子数组和     |
| 动态规划 (Dynamic Programming)         | 子数组的最优解                   | 最大子数组和 (53), 子数组最大积 (152), 子数组最大平均数 I (643)        | 使用 DP 数组存储中间结果，减少重复计算       |
| 单调队列 / 栈 (Monotonic Queue)        | 快速查找子数组中的最值           | 滑动窗口最大值 (239), 子数组范围和 (2104), 最短无序连续子数组 (581)    | 通过维护单调队列/栈来优化查询                |
| 分治算法 / 二分查找 (Divide & Conquer) | 复杂子数组问题, 有序数组查找     | 最大子数组和 (53), 子数组最大平均数 II                                 | 分治将问题递归分解，或使用二分查找优化       |
| 双指针 (Two Pointers)                  | 查找有序数组中的满足条件的子数组 | 和为 K 的子数组（无重复元素）(532), 三数之和 (15), 四数之和 (18)       | 利用双指针缩小搜索范围                       |
| 枚举 + 暴力解法 (Brute Force)          | 数据量小或难以优化的问题         | 优美子数组 (1248), 所有连续子数组枚举                                  | 枚举所有可能子数组进行计算                   |

# 常见题目思路与模板

## 滑动窗口 / 双指针 / 前缀和

这些思路相对简单，总结来说：

1. 利用前缀和实现快速计算子数组和
2. 根据题目条件，记录/累加结果
3. 有时需要搭配哈希表记录子数组的相关信息（比如元素，

## 动态规划

判断使用 DP 思路：

1. 需要找到满足某种条件的**最优解**（如最大值、最小值、最优积等）时
2. **具有最优子结构**：问题可以被分解为更小的子问题，这些子问题的解可以用于构建原问题的解
3. **重叠子问题**：问题的子问题是重叠的，即在解决当前问题时会多次遇到相同的子问题。

DP 五步骤：

1. 确定 DP 含义，一般根据题目要计算的内容即可定义 DP 含义，主要是一维 DP 还是二位 DP 数组
2. 确定状态转移方程，推导`DP[i]`是如何用其他已记录的值推导而来的，可能是前也可能是后面的值
3. 确定初始化方法，使用 0， or 1， or 其他值进行初始化
4. 遍历
5. 寻找结果，最后一个值 or 过程最大值 or 其他？
6. （优化）可以尝试优化空间复杂度，二维的通常可以使用 1 行 + 1 个， 一维的通常可以只记录前一个结果

举例：

```C++
class Solution {
public:
	int maxProduct(vectot<int>& nums){
		int n = nums.size();
		// 初始化DP数组，优化后只保留两个数字
		int last_max = nums[0], last_min = nums[0], ans = nums[0];
		for(int i = 1; i < n; i++){
			int mx = last_max, mn = last_min;
			last_max = max(nums[i], max(nums[i] * mx, nums[i] * mn));
			last_min = min(nums[i], min(nums[i] * mx, nums[i] * mn));
			ans = max(last_max, ans);
		}
		return ans;
	}
}
```

## 单调栈

**单调栈**是一种数据结构，通常用于解决**区间最值**、**子数组边界**等问题。在处理子数组问题时，单调栈能够高效地找到每个元素左侧和右侧第一个**大于**或**小于**它的元素。这种技术可以帮助我们在**O(n)** 的时间复杂度下解决许多涉及子数组的问题。

### **单调栈的基本原理**

- **单调递增栈**：栈中的元素按从栈底到栈顶递增。当遍历到一个新元素时，如果新元素小于栈顶元素，则弹出栈顶元素。通常用于查找左侧或右侧第一个小于某元素的值。
- **单调递减栈**：栈中的元素按从栈底到栈顶递减。当遍历到一个新元素时，如果新元素大于栈顶元素，则弹出栈顶元素。通常用于查找左侧或右侧第一个大于某元素的值。
- [单调栈【基础算法精讲 26】\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1VN411J7S7/?vd_source=64d148e234fce6362649a575b7d2ccd5)

### **单调栈的适用场景**

- **查找左右两侧最近的更大/更小元素**。
- **区间最值问题**。
- **子数组的最大/最小值的和、差问题**。

例题：
[2104. 子数组范围和 - 力扣（LeetCode）](https://leetcode.cn/problems/sum-of-subarray-ranges/solutions/1153054/cong-on2-dao-ondan-diao-zhan-ji-suan-mei-o1op/)

举例

```C++
class Solution {
public:
    long long solve(vector<int>& nums) {
        int n = nums.size();
        vector<int> left(n), right(n);
        fill(right.begin(), right.end(), n); // n 表示右侧没有更大的元素
        stack<int> st; // 单调递减栈
        for(int i = 0; i < n; i++){
            while(!st.empty() && nums[st.top()] <= nums[i]){
                right[st.top()] = i;
                st.pop();
            }
            left[i] = st.empty() ? -1 : st.top();
            st.push(i);
        }

        long long ans = 0;
        for(int i = 0; i < n; i++){
            ans += static_cast<long long>(nums[i]) * (i - left[i]) * (right[i] - i);
        }
    }

    long long subArrayRanges(vector<int>& nums) {
        // 计算每一个num 有多少次作为子数组最大值 & 多少次作为子数组最小值， 然后累计起来
        // left[i]， i 左侧第一个小于i的位置， right[i]， i右侧第一个小于i的位置
        long long ans = 0;
        ans += solve(nums);
        for(int & num : nums){
            num = -num;
        }
        ans += solve(nums);
        return ans;        
    }
};
```

## 分治法/二分法

[300. 最长递增子序列 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-increasing-subsequence/)

```C++
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        // 用 tails 数组记录递增子序列的最小结尾元素
        vector<int> tails(nums.size(), -10005);
        int ans = 0; // 当前最长递增子序列的长度

        // 遍历 nums 数组中的每个元素
        for (int num : nums) {
            int i = 0, j = ans;
            // 二分查找找到第一个大于 num 的位置
            while (i < j) {
                int mid = i + (j - i) / 2;
                if (tails[mid] < num) i = mid + 1;
                else j = mid;
            }
            tails[i] = num; // 更新 tails 数组
            // 如果 num 大于 tails 数组中的所有元素，扩展子序列长度
            if (j == ans) ans++;
        }
        return ans;
    }
};

```

## 线段树

在处理**多次询问的区间问题**时，线段树（Segment Tree）是一种非常高效的数据结构。它能够在 **O(log n)** 的时间复杂度内完成区间查询和修改操作，因此非常适合解决像「**区间最长连续上升序列问题**」和「**区间最大子段和问题**」这种需要多次查询的场景。

- [ ] Comimng soon!
