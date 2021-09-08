---
author: "Nolan"
title: "Catalan Number"
date: "2021-08-05"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "dynamic programming"]
ShowToc: false
TocOpen: false

---


## Challenge

Your task is to print the [Nth catalan number](https://en.wikipedia.org/wiki/Catalan_number).

```python
catalan(5) = 42
```

## Solution

### Bottom up

```python
def catalan(n):
    res = [0 for i in range(n+1)]
    res[0] = 1
    s = 0
    for i in range(1, n+1):
        for j in range(0, i):
            res[i] += res[j] * res[i-j-1]

    return res[n]
```

Time Complexity: O(n^2)  

### Top Down

```python
def catalan(n):
    if n == 0 or n ==1:
        return 1
    s = 0
    for i in range(n):
        s += catalan(i) * catalan(n-1-i)
    return  s
```

Time Complexity: O(n!)  

## Application

- Find the number of unique BST.
