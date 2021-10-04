
---
author: "Nolan"
title: "Longest Increasing Subsequence"
date: "2021-10-01"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "dynamic programming"]
ShowToc: false
TocOpen: false
---

## Challenge

You are given an integer array called nums, your task is to return the longest increasing subsequence.

E.g
`[0,1,2,7]` is the longest subsequence of the array `[0,3,1,6,2,2,7]`
## Solution 1 - Recursion


```py
class Solution:

    def first_solution(self, nums, index, prev, ct):

        if index > len(nums):
            self.m = max(self.m, ct)
            return
        self.first_solution(nums, index + 1, prev, ct)
        if index < len(nums) and nums[index] > prev:
            self.first_solution(nums, index + 1, nums[index], ct + 1)
        return ct

    def lengthOfLIS(self, nums: List[int]) -> int:
        self.m = 0
        self.first_solution(tuple(nums), 0, float("-inf"), 0)
        return self.m
```

Time complexity: O(n^2)  


## Solution 2 - Dynamic Programming

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        res = []
        dp = [1 for i in range(len(nums))]
        for i in range(len(nums)):
            for j in range(i,-1,-1):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j]+1)
        return max(dp)
```

Time Complexity: O(n^2)

## Solution 3 - Using Patience sort

```python
def lis_using_patience_sort(arr):
    stack = [[]]
    for n in arr:
        i = 0
        while i < len(arr)-1:
            if i < len(stack) and len(stack[i]) == 0:
                stack[i].insert(0, n)
                break
            elif i < len(stack)  and len(stack[i]) > 0 and n <= stack[i][0]:
                stack[i].insert(0, n)
                break
            elif i == len(stack)-1 and len(stack[i]) > 0 and n >= stack[i][0]:
                stack.append([n])
                break
            i += 1
    return len(stack)
```

Simplified implementation using bisect  

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        res = []

        for num in nums:
            if not res or num > res[-1]:
                res.append(num)
            else:
                idx = bisect.bisect_left(res,num)
                res[idx] = num
        return len(res)
```


Time Complexity: O(n log n)  

Credits: [youtube video](https://www.youtube.com/watch?v=22s1xxRvy28&ab_channel=StableSort)