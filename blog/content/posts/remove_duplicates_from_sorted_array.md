---
author: "Nolan"
title: "Remove duplicates in sorted array"
date: "2022-03-13"
categories: ["algorithm", "array"]
draft: false
description: "Another challenge"
tags: ["algo", "array"]
ShowToc: false
TocOpen: false
---

## Challenge


Given a sorted integer array, remove duplicate in place that elements appears at most twice.  

Constraints:

- The relative order of the elements should be kept the same.  
- Do not allocate extra space for another array. Modify the input array in-place with O(1) extra memory.   


Don't change the length of the array return the index of the last element after your operations.  


## Solution 1 

```python
class Solution:
    
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        ct = 1
        diff = 0
        my_end = len(nums)
        while i < my_end:
            j = i
            ct = 1
            while j < my_end-1:
                if nums[j] == nums[j+1]:
                    ct += 1
                else:
                    break
                j += 1

            if ct > 2:
                # overwrite
                start = i + 2
                end = i + ct
                my_end -= end - start
                z = 0
                while end + z < len(nums):
                    nums[start+z] = nums[end+z]
                    z += 1
            i += 1
        return my_end 
```


## Solution 2  Soon