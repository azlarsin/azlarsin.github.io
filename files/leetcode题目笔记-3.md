title: leetcode 题目笔记 - 3
author: azlar
date: '2016-10-25 14:42:47'
tags: []

---

<!-- desc -->

# 10.25

## 10. Regular Expression Matching

### problem
Implement regular expression matching with support for `'.'` and `'*'`.

	'.' Matches any single character.
	'*' Matches zero or more of the preceding element.
	
	The matching should cover the entire input string (not partial).
	
	The function prototype should be:
	bool isMatch(const char *s, const char *p)
	
	Some examples:
	isMatch("aa","a") → false
	isMatch("aa","aa") → true
	isMatch("aaa","aa") → false
	isMatch("aa", "a*") → true
	isMatch("aa", ".*") → true
	isMatch("ab", ".*") → true
	isMatch("aab", "c*a*b") → true

### solution
卡壳。。

感觉难点就在找错后怎样回头继续查找。想了很久，觉得还是应该有一次性遍历（不需要回溯）的方式来解决。

### other solutions
找了一些比较高效简洁的，找着写了下，先学习学习。

#### non-recursive
摘自评论区：
> [http://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/](http://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/)

```javascript
let isMatch = (str, pattern) => {
    if(!str || !pattern ) {
        return false;
    }
	
    let match = false,
        matchingChar = '';
	
    let i = 0, p = 0;
	
    while(i < str.length) {
        if(pattern.length > p && !match) {
            matchingChar = pattern.charAt(p);
	
            ++p;
	
            if(pattern.length > p && pattern.charAt(p) == '*') {
                match = true;
	
                ++p;
            }
        }else if(!match) {
            matchingChar = '';
        }
	
        if(str.charAt(i) == matchingChar || matchingChar == '.') {
            ++i;
        } else {
            if(!match) {
                return false;
            }else {
                match = false;
            }
        }
    }
	
    while(p < pattern.length) {
        let next = p + 1;
	
        if(pattern.length <= next || pattern.charAt(next) != '*') {
            return false;
        }
	
        p = next + 1;
    }
	
    return true;
};
```

#### use recursive
作者讲解：
> [**http://articles.leetcode.com/regular-expression-matching**](http://articles.leetcode.com/regular-expression-matching)

```javascript
let isMatch = (s, p) => {
    if(p[0] == undefined) {
        return s[0] == undefined;
    }

    if(p[0] == s[0] || p[0] == '.' && s) {
        return p[1] != '*' ?
            isMatch(s.substring(1), p.substring(1))
            :
            isMatch(s.substring(1), p) || isMatch(s, p.substring(2));
    } else {
        return p[1] == '*' && isMatch(s, p.substring(2));
    }
};
```

# 10.26
## 11. Container With Most Water
### problem
Given n non-negative integers *a<mi>1</mi>, a<mi>2</mi>, ..., a<mi>n</mi>*, where each represents a point at coordinate (*i, a<mi>i</mi>*). n vertical lines are drawn such that the two endpoints of line i is at (*i, a<mi>i</mi>*) and (*i, 0*). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container.


### solution
#### wrong
<font color='red'>**TLE**</font>
> running 15000 values.

简单无脑的双循环：

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {   
	let i = 0, j = 0, max = 0, temp = 0;
	while(height[i] !== undefined) {
		if(height[i + 1] === undefined) {
			break;
		}
		
		for(j = i + 1;j < height.length;j++) {
       	temp = Math.min(height[i], height[j]) * (j - i);
       	max = max >= temp ? max : temp;
		}
		i++;
	}
	
	return max;
};
```

后来将判断条件改为：

```javascript
let tempY = 0, tempX = 0, maxX = 0, maxY = 0;
if((tempY > maxY && tempX >= maxX) || (tempX > maxX && tempY >= maxY) || (tempX * tempY > maxX * maxY)) {
	maxY = tempY;
	maxX = tempX;
}
```	

想通过简单的判断来节省一些时间，仍然超时。

### other good solutions
#### O(n)
先来一个改写讨论区里大家用的比较多的：

> [https://discuss.leetcode.com/topic/503/anyone-who-has-a-o-n-algorithm/2](https://discuss.leetcode.com/topic/503/anyone-who-has-a-o-n-algorithm/2)
> 
> [https://discuss.leetcode.com/topic/3462/yet-another-way-to-see-what-happens-in-the-o-n-algorithm/15](https://discuss.leetcode.com/topic/3462/yet-another-way-to-see-what-happens-in-the-o-n-algorithm/15)
> 


```javascript
var maxArea = function(height) { 
  let max = 0, i = 0, j = height.length - 1;
  while(i < j)
  {
    max = Math.max(max, Math.min(height[i], height[j]) * (j - i));
    if(height[i] < height[j])
      i++;
    else
      j--;
  }

  return max;
};
```

再一个注释解释的比较清楚的。
> [https://discuss.leetcode.com/topic/35117/share-my-short-java-code-with-%E4%B8%AD%E6%96%87-explanation](https://discuss.leetcode.com/topic/35117/share-my-short-java-code-with-%E4%B8%AD%E6%96%87-explanation)
> 

```java
/*
    设置两个指针i, j, 一头一尾, 相向而行. 假设i指向的挡板较低, j指向的挡板较高(height[i] < height[j]).
    下一步移动哪个指针?
    -- 若移动j, 无论height[j-1]是何种高度, 形成的面积都小于之前的面积.
    -- 若移动i, 若height[i+1] <= height[i], 面积一定缩小; 但若height[i+1] > height[i], 面积则有可能增大.
    综上, 应该移动指向较低挡板的那个指针.
*/
public class Solution {
    public int maxArea(int[] height) {
        if (height==null || height.length==0) { return 0; }
        int max = 0;
        int i = 0, j = height.length-1;
        while (i < j) {
            max = Math.max(max, (j-i) * Math.min(height[i], height[j]));
            if (height[i] < height[j]) {  // should move i
                int k; for (k=i+1; k<j && height[k]<=height[i]; ++k) {}
                i = k;
            } else {  // should move j
                int k; for (k=j-1; k>i && height[k]<=height[j]; --k) {}
                j = k;
            }
        }
        return max;
    }
}
```

**Editorial Solution**
> [https://leetcode.com/articles/container-most-water/](https://leetcode.com/articles/container-most-water/)
>
> *array =>* `[1 8 6 2 5 4 8 3 7]`
> 
> ![](http://blog.azlar.cc/images/leetcode/11_Container_Water.gif)
> 
> ![](https://leetcode.com/media/original_images/11_Container_Water.gif)

感觉这题，挺难想到的。












