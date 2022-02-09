---
author: "Nolan"
title: "Interval list intersection"
date: "2022-02-08"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "lists"]
ShowToc: false
TocOpen: false
---


## Challenge

Given two lists of intervals, return the intersection of these two interval lists.

Example:

```python
list1 = [[0, 2], [5,6], [24, 25]]
list2 = [[1,5],[8,13], [25, 26]]
OUTPUT = [[1,2],[5,5],[25,25]]
```



## Solution #1 - Memory Limit Exceeded

```python
class Solution:
    
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        if not firstList or not secondList:
            return []
        max_val = max(firstList[-1][1],secondList[-1][1])
        first = [0 for i in range(0, max_val+1)]
        second = [0 for i in range(0, max_val+1)]
        for f in firstList:
            for i in range(f[0],f[1]):
                first[i] = 1
                
        for s in secondList:
            for i in range(s[0],s[1]):
                second[i] = 1
        i = 0
        output  = []
        while i < max_val + 1:
            if first[i] == second[i] == 1:
                start_index = i
                while first[i] == second[i] == 1:
                    i += 1
                else:
                    end_index = i
                output.append([start_index, end_index])
            i += 1
        i = 0 
        while i < max_val + 1:
            if first[i-1] == 0 and first[i] == 1 and second[i-1] == 1 and second[i] == 0:
                output.append([i,i])
            if second[i-1] == 0 and second[i] == 1 and first[i-1] == 1 and first[i] == 0:
                output.append([i,i])
            i += 1
        return sorted(output)
```

Memory inefficient because the biggest value of the two lists is used to crate `first` and `second`.