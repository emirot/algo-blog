---
author: "Nolan"
title: "Implementing queue with stacks"
date: "2021-03-04"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "stacks"]
ShowToc: false
TocOpen: false
---


## Challenge

Implement a queue (FIFO) using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).  


## Solution

```python
class MyQueue:

    def __init__(self):
        self.stack1 = []
        self.stack2 = []
        self.mypeek = None
        
    def push(self, x: int) -> None:
        if not self.stack1:
            self.mypeek = x
        self.stack1.insert(0, x)
        return None
    
    def pop(self) -> int:
        while len(self.stack1):
            val = self.stack1.pop(0)
            self.stack2.insert(0, val)
        if self.stack2:
            ret = self.stack2.pop(0)
        while len(self.stack2):
            val = self.stack2.pop(0)
            self.stack1.insert(0, val)

        return ret

    def peek(self) -> int:
        if self.stack1:
            self.mypeek = self.stack1[len(self.stack1)-1]
        return self.mypeek if self.peek else None

    def empty(self) -> bool:
        if len(self.stack1) == 0:
            return True
        return False
```