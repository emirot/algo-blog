---
author: "Nolan"
title: "Integer to roman number"
date: "2022-02-08"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "lists"]
ShowToc: false
TocOpen: false
---

## Challenge

Given a integer converts it to it's Roman notation.
E.g 14 becomes XIV


## Solution

First I was thinking about adding all conversion in a hash map but it not that will be ask in a real interview scenario.


```python
class Solution:

    def find_representation(self, num, one, five, ten):
        # if less than 3
        rep = ""
        if 0:
            return ""
        if num <= 3:
            for i in range(num):
                rep += one
        # four is five "minus" one
        if num == 4:
            rep += one + five
        # five use five
        if num == 5:
            return five
        # between five and nine use five + one(s)
        if num > 5 and num < 9:
            rep = five
            for i in range(num - 5):
                rep += one
        if num == 9:
            rep += one + ten
        if num == 10:
            rep += ten
        return rep

    def intToRoman(self, num: int) -> str:
        thousand = self.find_representation((num % 10000) // 1000, "M","","")
        hundred =  self.find_representation((num % 1000) // 100, "C","D","M")
        ten = self.find_representation((num % 100) // 10 , "X", "L", "C")
        ones = self.find_representation(num % 10, "I", "V", "X")
        return thousand + hundred + ten + ones
```