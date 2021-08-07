---
author: "Nolan"
title: "Rod Cutting"
date: "2021-08-06"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "dynamic programming"]
ShowToc: false
TocOpen: false
---

## Challenge


## Solution


```python
class Solution:

    def helper(self, n, cost):
        if n < 0:
            return 0
        if n == 0:
            return cost
        if n in self.memo:
            return self.memo[n]
        res = 0
        for i in range(1, len(self.cost)+1):
            res = max(res, self.helper(n-i, cost + self.cost[i]))
        self.memo[n] = res
        return self.memo[n]

    def rodCutting(self, n, cuts):
        self.res = 0
        self.memo = {}
        cost  = {}
        for i, e in enumerate(cuts):
            cost[i+1] = e
        self.cost = cost
        return self.helper(n, 0)
```