---
author: "Nolan"
title: "Catalan Number"
date: "2021-08-03"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "recursion"]
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
    if n == 0:
        return 1
    c = []
    for i in range(n+1):
        c.append(0)
    c[0] = 1
    res = 0
    for j in range(0, n+1):
        for i in range(0, j):
            c[j] += c[i] * c[j-1-i]
    return c[n]
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