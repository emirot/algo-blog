
---
author: "Nolan"
title: "Jump Game"
date: "2021-08-01"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "recursion"]
ShowToc: false
TocOpen: false
---

## Challenge


![Jump Game](https://algo.nolanemirot.com/jump-game.jpg)

Given an array of positive intege, each element represents the max length, you need to find the min number of jump in order to reach the end of the array.

```
Input: nums = [2,4,1,1,17]
Output: 2 # reach to index 1 and then from there last index.
```

---

## Solution - Recursion | TLE

```python
class Solution:    
    
    def helper(self, nums, current_index, steps, l, previous):
        # ending recursion early if already above
        if len(previous) >= self.m:
            return
        if current_index >=l-1:
            self.m = min(self.m, len(previous))
            return 
        
        for i in range(1, steps + 1):
            if current_index + i < l:
                self.helper(nums, current_index + i, nums[current_index + i],l, previous + [1])
        
    def min_jump(self, nums: List[int]):
        if not nums:
            return 0
        self.m = float('inf')
        previous = []
        self.helper(nums, 0, nums[0], len(nums), previous)
        return self.m
```

## 