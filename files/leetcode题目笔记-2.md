title: leetcode 题目笔记 - 2
author: azlar
date: '2016-10-13 12:02:21'
tags: [leetcode, 算法, Median of Two Sorted Arrays, Longest Palindromic Substring, ZigZag Conversion, Reverse Integer]

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


## 6. ZigZag Conversion
### problem
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

	P   A   H   N
	A P L S I I G
	Y   I   R
	
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:

	string convert(string text, int nRows);
	
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

### solution(148ms - 72.63%, 16.10.17)
开始不明白题目的意思，搜了一下。

![](//blog.azlar.cc/images/leetcode/ZigZag Conversion.png)

```javascript
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    let text = Array(numRows).fill(''), line = 0, len = s.length;
    
    if(numRows === 1 || len <= numRows) {
        return s;
    }
    
    const keyLoop = 2 * numRows - 2;

    for(let i = 0;i < len;i++) {
        line = i % keyLoop;
        line = line > (numRows - 1) ? (keyLoop - line) : line;
        text[line] += s[i];
    }
    return text.join("");
};
```	

### other good solutions
faster: [https://discuss.leetcode.com/topic/56663/a-fast-javascript-implementation](https://discuss.leetcode.com/topic/56663/a-fast-javascript-implementation)

```javascript
var convert = function(s, numRows) {
    var result = [];
    var step = 1, index = 0;
    for(var i = 0; i < s.length; i++){
        if(result[index] === undefined){//'undefined' will be put into string without this
            result[index] = '';
        }
        result[index] += s[i];
        if(index === 0){
            step = 1;
        }else if(index === numRows - 1){
            step = -1;
        }
        index += step;
    }
    return result.join('');
};
```

## 7. Reverse Integer
### problem
Reverse digits of an integer.

**Example1:** x = 123, return 321
**Example2:** x = -123, return -321

**spoilers:**

	Have you thought about this?
	Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!
	
	If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.
	
	Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?
	
	For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
	

###solution(132ms - 72.79%, 16.10.17)
纯字符串反转，感觉还应该有更好的解决方案。

```javascript
/**
 * @param {number} x
 * @return {number}
 */
 var reverse = function(x) {
    let pn = x >= 0 ? 1 : -1,
    str = Math.abs(x).toString(), newStr = '', len = str.length;
    
    const MAX = 2147483647;
    
    if(len <= 1) {
      return x;
    }
  
    i = len - 1;
    while(i >= 0) {
        newStr += str[i];
        i--;
    }
  
    let number = Number(newStr);
  
    return number > MAX ? 0 : number * pn;
};
```

### other good solutions
看了下讨论区，貌似我会错意了，字符串反转确实略 low。。。一般都用求模逐步求出最后一位。

```javascript
var reverse = function(x) {
var flag = x >= 0 ? 1: -1;
var target = Math.abs(x);
var maxNumIn32Bit = Math.pow(2, 31)-1;
var sum = 0;
  
while(target > 0){
	var tmp = target % 10;
	    
	target = Math.floor(target/10);
	    
	sum = sum * 10 + tmp;
	    
	if(sum == Infinity || sum > maxNumIn32Bit){
	  return 0;
	} 
}
  
return sum * flag;
};
```


	