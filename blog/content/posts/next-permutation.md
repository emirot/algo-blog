---
author: "Nolan"
title: "Next Permutation"
date: "2025-11-15"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo"]
ShowToc: false
TocOpen: false

---

## Description

Given an integer find the next permutation in given an integer.

Examples:
`12645` next is `12654`


## Solution


```python

def next_permuation(arr):
    i = len(arr) -2
    while i >= 0 and arr[i] >= arr[i+1]:
        i -= 1

    pivot = i
    if i >= 0:
        j = pivot 
        sw = pivot
        while j < len(arr):
            if arr[pivot] < arr[j]:
                sw = j
            j += 1
        arr[pivot], arr[sw] = arr[sw], arr[pivot]

    res = arr[:pivot+1] + arr[pivot+1:][::-1]
    return res

if __name__ == "__main__":
    arr = [1, 6, 3, 7, 5] # next permuation is [1, 6, 5, 3, 7]
    print(next_permuation(arr))
    arr = [3, 2, 1]
    print(next_permuation(arr))
    nums = [1, 5, 8, 4, 7, 6, 5, 3, 1]
    print(next_permuation(nums)) # Output: [1, 5, 8, 5, 1, 3, 4, 6, 7]
```