---
author: "Nolan"
title: "Maximum request in time window"
date: "2025-11-06"
categories: ["algorithm", "python"]
draft: false
description: "Another leetcode"
tags: ["algo", "windows"]
ShowToc: false
TocOpen: false
---


## Challenge

Given an integer array timestamp and an integer windowSize, find the maximum number of requests that occur within any continuous time window of a specified range.The function should return an integer denoting the maximum requests observed in any window of windowSize minutes.

## Solution


```python

def maxRequests(timestamp, windowSize):
    timestamp.sort()
    l = 0
    r = 1
    best = 0
    while r < len(timestamp):
        if timestamp[r] - timestamp[l] >= windowSize :
            l += 1
        
        best = max(best, r -l + 1)
        r += 1

    return best

# Test cases
if __name__ == "__main__":
    # Test case 1: Basic example
    timestamp1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    windowSize1 = 5
    print(f"Test 1: timestamp = {timestamp1}, windowSize = {windowSize1}")
    print(f"Result: {maxRequests(timestamp1, windowSize1)}")
    print(f"Expected: 5 (requests at times 1,2,3,4,5 or 6,7,8,9,10)\n")
    
    # Test case 2: Clustered requests
    timestamp2 = [1, 2, 3, 10, 11, 12, 13]
    windowSize2 = 5
    print(f"Test 2: timestamp = {timestamp2}, windowSize = {windowSize2}")
    print(f"Result: {maxRequests(timestamp2, windowSize2)}")
    print(f"Expected: 4 (requests at times 10,11,12,13)\n")
    
    # Test case 3: All requests within window
    timestamp3 = [1, 2, 3, 4]
    windowSize3 = 10
    print(f"Test 3: timestamp = {timestamp3}, windowSize = {windowSize3}")
    print(f"Result: {maxRequests(timestamp3, windowSize3)}")
    print(f"Expected: 4 (all requests fit in window)\n")
```


