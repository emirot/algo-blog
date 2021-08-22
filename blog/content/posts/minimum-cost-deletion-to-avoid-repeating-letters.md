---
author: "Nolan"
title: "Minimum Deletion Cost to Avoid Repeating Letters"
date: "2021-08-21"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "Greedy"]
ShowToc: false
TocOpen: false
---

## Challenge

Given a String S and and an array representing the cost of each deletion.
You goal is to minimize the cost needed to remove all consecutive repetive characters.

Example 1:

```bash
"aba"
[2,3,4]
=> 0
```
Example 2:
```
"abaa"
[2,3,4,1]
=> 1
```

## Solution 1 - Brute Force - TLE

```python
class Solution:
    def no_consequtive_letters(self, s):

        t = ""
        for e in s:
            if e !="#":
                t += e
        for i in range(1,len(t)):
            if t[i-1] == t[i]:
                return False
        return True

    def helper(self, s, current_cost, cost, index):

        if self.no_consequtive_letters(s):
            # print(s,"current_cost", current_cost)
            self.min_cost = min(current_cost, self.min_cost)
            return 0
        if index > self.s_len:
            return 0

        self.helper(s[:index] + "#" +s[index+1:] , current_cost + cost[index], cost,index+1)
        self.helper(s, current_cost, cost,index+1)

        return 0
            
        
    def minCost(self, s: str, cost: List[int]) -> int:
        self.s_len = len(s)-1
        self.min_cost = float("inf")
        self.helper(s, 0, cost, 0)
        return self.min_cost
```

## Solution 2 - Greedy

