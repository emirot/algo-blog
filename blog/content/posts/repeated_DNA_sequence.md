---
author: "Nolan"
title: "Repeated DNA sequence"
date: "2022-02-15"
categories: ["algorithm", "string"]
draft: false
description: "Another challenge"
tags: ["algo", "string"]
ShowToc: false
TocOpen: false
---


## Challenge

The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.  
For example, "ACGAATTCCG" is a DNA sequence.  
When studying DNA, it is useful to identify repeated sequences within the DNA.  
Given a string s that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA chain.  

## Solution 1 - Iteration

```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        res = set()
        _set = set()
        for i in range(len(s)):
            seq = s[i:i+10]
            if seq in _set and seq not in res:
                res.add(seq)
            _set.add(seq)
        return res
```
Time Complexity: 0(n*m)
## Solution 2 - Rabin-Karp

```python
class Solution:

    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        h = 0
        p  = 4
        tl = 10
        dic = {'A':1, 'C':2, 'G':3, 'T':4}
        nums = [dic[e] for e in s]
        seen = set()
        res = set()
        # mod no need
        for e in range(len(s) - 10 + 1):
            if e == 0:
                j = 9
                for i in range(10):
                    h += nums[i] * p ** j
                    j -=1
            else:
                previous_hash = nums[e-1] * (p ** 9)
                h = (h - previous_hash) * p + (nums[e + 9])
            if h in seen:
                res.add(s[e:e+10])
            seen.add(h)
        return res
```
Time complexity: O(n)