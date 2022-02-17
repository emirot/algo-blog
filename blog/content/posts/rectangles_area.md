---
author: "Nolan"
title: "Rectangle areas"
date: "2022-02-13"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "geometry"]
ShowToc: false
TocOpen: false
---

## Challenge

Given coordinates of two rectangles compute the total area they cover.


## Solution 1

Use the coordinate to generate the area that overlaps.

```python
class Solution:

    def generates_areas(self, top_left, bottom_right): 
        areas = set()
        y = top_left[1]
        while y  > bottom_right[1] :
            x = top_left[0]
            while x < bottom_right[0]:
                areas.add(((x,y), (x, y-1), (x+1,y), (x+1, y-1)))
                x += 1
            y -= 1
        return areas


    def computeArea(self, ax1: int, ay1: int, ax2: int, ay2: int, bx1: int, by1: int, bx2: int, by2: int) -> int:
        rec1 =  (ay2 - ay1) * (ax2 - ax1)
        rec2 = (by2 - by1) * (bx2 - bx1)
        areas1 = self.generates_areas((ax1,ay2), (ax2, ay1))
        areas2 = self.generates_areas((bx1, by2), (bx2, by1))
        i = areas1.intersection(areas2)
        return rec1 + rec2 - len(i)
```

# Solution 2

Get the overlap by using min and max, and handle case when then don't overlap meaning a negative distance.

```python
class Solution:
    
    def computeArea(self, ax1: int, ay1: int, ax2: int, ay2: int, bx1: int, by1: int, bx2: int, by2: int) -> int:
        rec1 =  (ay2 - ay1) * (ax2 - ax1)
        rec2 = (by2 - by1) * (bx2 - bx1)
        x_area = max(ax1,bx1)
        x2_area = min(ax2,bx2)
        y_area = min(by2, ay2)
        y2_area = max(ay1,by1)
        return rec1 + rec2 - max(0, x2_area - x_area) * max(0, y_area - y2_area)
```