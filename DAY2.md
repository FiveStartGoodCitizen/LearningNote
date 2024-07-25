## 1.Leetcode 977 . 有序数组的平方
==双指针法==
按非递减顺序排序的整数数组nums，返回每个数字的平方组成的新数组，要求按非递减顺序排序。
vector<int> sortedSquares(vector<int>& nums)
&nbsp;&nbsp;1.return为vector<int>  
&nbsp;&nbsp;2.==暴力方法==很容易想到但是时间复杂度为O（n+logn）
&nbsp;&nbsp;3.思考题目  数组是有序的  如果是无序的 这就是中等题
&nbsp;&nbsp;&nbsp;&nbsp;考虑==最大值在两端 不在中间==  因此可以考虑是否可以使用双指针
&nbsp;&nbsp;&nbsp;&nbsp;本题的难度并不是双指针的用法 而是==判断什么时候可以用双指针==
&nbsp;&nbsp;4.总结
&nbsp;&nbsp;&nbsp;&nbsp;在排序时，数组是==有序==的，==极值在两端==时，可以考虑双指针。

2. Leetcode 209 .长度最小的子数组 中等
给定一个含有 n 个正整数的数组和一个正整数 target 。
找出该数组中满足其总和大于等于 target 的长度最小的 子数组
子数组
 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 

&nbsp;&nbsp;1.看到数组 一般会考虑到几种常见的解法 双指针(滑动窗口也是双指针的一种) 哈希 
排序 分治 动态规划   
&nbsp;&nbsp;&nbsp;&nbsp;一般看上去比较难的题目会优先考虑到动态规划
&nbsp;&nbsp;&nbsp;&nbsp;此题可以使用dp或双指针解 本次使用双指针
&nbsp;&nbsp;2.这题的难点在于怎么==更新子串的长度==，每次满足子串的大小>=target时，更新子串的长度，并且==取最短==的子串长度。
&nbsp;&nbsp;&nbsp;&nbsp;子串长度不难想，快指针往后推，慢指针指向开始的索引，满足条件时，记录下子串的长度。
```cpp
 		subLength = (j - i +1);
```
               
&nbsp;&nbsp;&nbsp;&nbsp;之后思考怎么==更新子串的最短长度==。于此同时 ==慢指针向后推进==查看是否满足条件，满足条件时，更新子串长度。
```cpp
		result = result < subLength ? result:subLength;
```

&nbsp;&nbsp;3.在更新子串长度时，需要和比记录的长度大的==比较==才行，如果开始result=0时，则结果一直为0，所以result取最大值。
```cpp
		int result = INT32_MAX;
```
&nbsp;&nbsp;4.总结
&nbsp;&nbsp;&nbsp;&nbsp;画图思考滑动窗口，或者说指针是怎么移动的。