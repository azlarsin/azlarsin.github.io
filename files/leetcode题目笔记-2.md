title: leetcode 题目笔记 - 2
author: azlar
date: '2016-10-13 12:02:21'
tags: []

---
[leetcode](https://leetcode.com) 做题记录。
<!-- desc -->

## 4. Median of Two Sorted Arrays
### problem
There are two sorted arrays **nums1** and **nums2** of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**Example 1:**

	nums1 = [1, 3]
	nums2 = [2]

	The median is 2.0
	
**Example 2:**

	nums1 = [1, 2]
	nums2 = [3, 4]

	The median is (2 + 3)/2 = 2.5
	
### solution (188ms - 50.82%)
不知道这题为什么难度是 hard，可能有更快的方法吧

```javascript
var findMedianSortedArrays = function(nums1, nums2) {
	let nums = nums1.concat(nums2);
	
	nums.sort((a, b) => { return a - b; });
	
	let len = nums.length;
	let key = parseInt(len / 2);
	
	return len % 2 === 0 ? 
		(nums[key - 1] + nums[key]) / 2
		:
		nums[key];
};
```
### another solution (159ms - 90.57%)
在 discuss 区看了下，发现其实是有更好的解法的，上面的解法必须要排序一次。于是按别人的思路，又写了这个不需要排序的：算出两个中间 k 后，从头开始比对计数（只计算 k 次即可）。

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
	var findMedianSortedArrays = function(nums1, nums2) {
	var len = nums1.length + nums2.length;
	  
	var k = parseInt(len / 2);
		
	return len % 2 === 0 ?
		(findByK(nums1, nums2, k - 1) + findByK(nums1, nums2, k)) / 2
		:
		findByK(nums1, nums2, k);
	  
  
	function findByK(nums1, nums2, k) {
		var i = 0, j = 0, val = 0; 
		    
		while(i < nums1.length && j < nums2.length && k >= 0) {  
			val = (nums1[i] < nums2[j]) ? nums1[i++] : nums2[j++];  
			k--;  
		}
		//j = num2.length, k = k - j  
		while(i < nums1.length && k >= 0) {  
			val = nums1[i++];  
			k--;  
		}  
		//i = num1.length, k = k - i
		while(j < nums2.length && k >= 0) {  
			val = nums2[j++];  
			k--;  
		}  
			
		return val; 
  }
  
};


console.log(findMedianSortedArrays([1, 10], [2, 3, 4, 5,6, 7, 8, 9]));
//
5.5
```

### else 
还在 [这里](!http://blog.csdn.net/whucyl/article/details/23524045) 找到第三种解决方案：递归二分。还没测试，有点看不太懂。

## 5. Longest Palindromic Substring
Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

### solution
已卡壳。。。
思路：用 hash 存储

	