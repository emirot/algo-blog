---
author: "Nolan"
title: "Paint Fence"
date: "2021-07-27"
categories: ["algorithm", "python"]
draft: false
description: ""
tags: ["algo", "blog"]
ShowToc: false
TocOpen: false
---

![Paint Fence](https://algo.nolanemirot.com/paint-fence.jpg)

## Challenge

 ---


You are painting post on a fence of size N.  
Only K consecutive post can have the same color.  
Return the number of way you can paint the fence.  

E.g:
```bash
N = 3
K = 2
-> will return 6
```

## Solution 1 Time Limted Exceeded

```python
class Solution:
    def helper(self,n, k, fence) ->int:
        if len(fence) >= 3 and fence[-3] == fence[-2] == fence[-1]:
            return
        if len(fence) == n:
            self.count += 1
            return
        for i in range(0, k):
            self.helper(n, k, fence + str(i))

    def numWays(self, n: int, k: int) -> int:
        self.count = 0
        self.helper(n, k, "")
        return self.count
```

The code above will create a recursion tree like so:


```
            /         \
           /           \
          R             G
        /  \           /  \
       R     G         R     G
      / \   / \       / \    / \
    R    G  R  G     R   G  R   G
------------------------------------
```      1  2  3     4   5  6

Time complexity: k^n
