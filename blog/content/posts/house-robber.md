---
author: "Nolan"
title: "Catalan Number"
date: "2021-08-23"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "dynamic programming"]
ShowToc: false
TocOpen: false

---

## Challenge

The array nums represent the value inside each house.
What is stopping you to rob everything is that you cannot rob two consecutive houses without triggering the alarm.
Determine the maxium amout of money you can rob without triggering the alarm.


## Solution 1 - Recursion

```python
class Solution:
    
    
    def helper(self, index, nums, val):
        
        if index > len(nums)-1:
            self.m = max(self.m, val)
            return 
        
        self.helper(index+1, nums, val)
        self.helper(index+2, nums, nums[index] + val)
        
        
    def rob(self, nums: List[int]) -> int:
        self.m = float("-inf")
        self.helper(0, nums, 0)
        return self.m
        
        
```
Time Complexity: O(n^2)  



## Solution 2 - Dynamic Programming

```python
def houseRobber(nums):
    res = []
    dp = [0 for i in range(len(nums))]
    if not nums:
        return 0
    if len(nums) < 3:
        return max(nums)
    dp[0] = nums[0]
    print(dp)
    if nums[1] > nums[0]:
        dp[1] = nums[1]
    else:
        dp[1] = nums[0]

    for i in range(2, len(nums)):
        val = max(dp[i-1], dp[i-2] + nums[i])
        dp[i]= val
    return dp[-1]
```


