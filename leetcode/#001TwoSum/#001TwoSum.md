#Two Sum
###问题描述
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
###翻译

###思路

####解法1：双循环，简单暴力
时间复杂度：O(n^2)　空间复杂度：O(1)  
两层循环，遍历两次数组，相加合为target的值的下标就是所需示值  



####解法2：hashMap
时间复杂度：O(n)　空间复杂度：O(n)  


####解法3：双指针夹逼
时间复杂度：O(n*log^n)　空间复杂度：O(n)  
排序O(log^n)，再夹逼O(n)  
  



