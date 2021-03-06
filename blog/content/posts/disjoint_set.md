---
author: "Nolan"
title: "Disjoint Set"
date: "2021-10-10"
categories: ["algorithm", "python", "data-structure"]
description: "Another challenge"
tags: ["algo", "tree"]
ShowToc: false
TocOpen: false
---

## Challenge

Given an adjency matrix, find the group of nodes that are connected together.

E.g ```isConnected = [[1,1,0],[1,1,0],[0,0,1]]```
Will return 2

## Data Structure

Creating a Disjoin Set data structure using a dictionary.  

```python
class DisjointSet:

    def __init__(self, n):
        self.rank = {i:i for i in range(n)}

    def __repr__(self):
        return f"Repr:{self.rank}"

    def find(self, val):
        # adding collapsing find
        original_v = val
        while self.rank[val] != val:
            val = self.rank[val]
        if original_v != val:
            self.rank[original_v] = val
        return val
    
    def union(self,val1, val2):
        v1 = self.find(val1)
        v2 = self.find(val2)
        self.rank[v2] = v1
```

## Solution


```python
class Solution:
    
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        ds = DisjointSet(len(isConnected[0]))

        for n, node in enumerate(isConnected):
            for j, v in enumerate(node):
                if v == 1 and j !=n:
                    ds.union(n, j)


        ct = 0
        for k,v in ds.rank.items():
            if k == v:
                ct += 1
        return ct
```
