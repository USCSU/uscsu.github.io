#SubArray

##1. Maximum Size Subarray Sum Equals k##

**Description:**

Given an array nums and a target value k, find the maximum length of a subarray that sums to k. 
If there isn't one, return 0 instead.

**Example:**

```
Given nums = [1, -1, 5, -2, 3], k = 3,
return 4. (because the subarray [1, -1, 5, -2] sums to 3 and is the longest)

Given nums = [-2, -1, 2, 1], k = 1,
return 2. (because the subarray [-1, 2] sums to 1 and is the longest)

```
**Idea:**

关键点在于： **sum等于k**

1. 用哈希存在路径中所有的值，当遇到新的sum的时候，判断sum-k是否在哈希里出现过，如果出现过，则判断最长长度
2. edge case：当整个序列相加等于0的时候，如果0没有存入哈希的时候，所以在处理长度的时候需要先存入0的index
3. 由于value是index，key是sum，如果遇到下一个sum-k出现的时候，长度是i-j。

subarray的相关题目很多，这题最重要的是linear时间linear空间解决了**连续相加之和**是否等于某个数的问题


**Code:**

```java
	public int maxSubArrayLen(int[] nums, int k) {
	        if(nums == null || nums.length ==0) return 0;
	        HashMap<Integer,Integer> map = new HashMap<>(); //key is sum, value is index
	        map.put(0,-1); //all sum starts from 0
	        int len = 0;
	        int sum = 0;
	        for(int i =0;i<nums.length;i++){
	            sum+=nums[i];
	            if(map.containsKey(sum-k)){ //found match
	                len = Math.max(len, i-map.get(sum-k));
	            }
	            if(!map.containsKey(sum))
	                map.put(sum,i);
	            
	        }
	        return len;
	    }
```
 

##2. Continuous Subarray Sum##

**Idea:**

这题跟 [第一题]（Maximum Size Subarray Sum Equals k） 很像，唯一的不同就是这道题要求得出的和是k的倍数，那么存入哈希的仅仅是

**Description:**

Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of k, that is, sums up to n*k where n is also an integer.

**Example:**
	
	Input: [23, 2, 4, 6, 7],  k=6
	Output: True
	Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
	
	Input: [23, 2, 6, 4, 7],  k=6
	Output: True
	Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
**Code:**


