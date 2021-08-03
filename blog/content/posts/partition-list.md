---
author: "Nolan"
title: "Partition List"
date: "2021-08-01"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "Linked List"]
ShowToc: false
TocOpen: false
---

## Challenge

![Partition List](https://algo.nolanemirot.com/partition-list.jpg)

---


Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

The order of the initial linked list must be preserved.

## Solution

```python
from copy import deepcopy
class Solution:
    
    def add_to_list(self, head, node,x):
        node.next = None
        if head is None and node.val < x:
            self.left_part = node
            self.left_tail = node
            return
        elif head is None and node.val >= x:
            self.right_part = node
            self.right_tail = node
            return
        if head == self.left_part:
            self.left_tail.next = node
            self.left_tail = node
        if head == self.right_part:
            self.right_tail.next = node
            self.right_tail = node
        
    def partition(self, head: ListNode, x: int) -> ListNode:
        self.left_part = None
        self.right_part = None
        tmp = head
        while tmp:
            tmp_cpy = deepcopy(tmp)
            if tmp.val < x:
                self.add_to_list(self.left_part, tmp_cpy,x)
            else:
                self.add_to_list(self.right_part, tmp_cpy,x)
            tmp = tmp.next
        tmp = self.left_part
        if not tmp:
            return self.right_part
        self.left_tail.next = self.right_part
        return self.left_part
```

Time complexity: O(n)  
Space complexity: O(1)