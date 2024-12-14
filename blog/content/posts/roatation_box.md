---
author: "Nolan"
title: "Rotating box"
date: "2024-11-24"
categories: ["algorithm", "python"]
draft: false
tags: ["algo", "blog"]
ShowToc: false
TocOpen: false
---

###  Challenge

Leetcode 1861

You are given an m x n matrix of characters boxGrid representing a side-view of a box. Each cell of the box is one of the following:

A stone '#'
A stationary obstacle '*'
Empty '.'
The box is rotated 90 degrees clockwise, causing some of the stones to fall due to gravity. Each stone falls down until it lands on an obstacle, another stone, or the bottom of the box. Gravity does not affect the obstacles' positions, and the inertia from the box's rotation does not affect the stones' horizontal positions.

It is guaranteed that each stone in boxGrid rests on an obstacle, another stone, or the bottom of the box.

Return an n x m matrix representing the box after the rotation described above.


### Solution


```python3
class Solution:

    def rotate(self, arr):

        new_arr = [ ['.']  * len(arr) for r in range(len(arr[0])) ]
        r = len(arr) -1
        for row in arr:
            c = 0 
            for col in row:
                print(c, r)
                new_arr[c][r] = col
                c += 1
            r -= 1
        return new_arr
        
    def move_stones(self, box):
        N = len(box)
        col = len(box[0]) -1
        i = 0
        while i < N:
            j =  len(box[0]) -1
            while j >= 0:
                k = j
                if box[i][j] == "#":
                    while k < col:
                        if k + 1 <= col and box[i][k] == '#' and box[i][k+1] == '.':
                            box[i][k], box[i][k+1] = box[i][k+1] , box[i][k]
                        else:
                            break
                        k += 1
                j -= 1
            i += 1

    def rotateTheBox(self, box: List[List[str]]) -> List[List[str]]:
        self.move_stones(box)
        arr = self.rotate(box)
        return arr
```




