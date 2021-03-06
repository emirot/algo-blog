---
author: "Nolan"
title: "Reverse linked list in between"
date: "2021-07-25"
categories: ["algorithm", "linked-list"]
draft: false
description: "Another programing challenge"
tags: ["python", "algorithm"]
ShowToc: false
TocOpen: false
---

![Linked List](https://algo.nolanemirot.com/linked-list.jpg)
## Challenge

Given the head of a singly linked list and two integers, reverse the nodes of the list from position left to position right.

E.g: reverseBetween(head, 2, 4)

```bash
1 -> 2 -> 3 -> 4 -> 5
```
Returns

```bash
1 -> 4 -> 3 -> 2 -> 5
```


## Solution 

```python
class Solution:
    

    def reverse(self, head, steps):
        tmp = head
        prev = None
        tail = head
        i = 0
        while tmp and i < steps:
            current = tmp
            n = current.next
            current.next = prev
            prev = current
            tmp = n
            i+=1
        head = current
        tail.next =n
        t = head
        return head
    
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        tmp=head
        j = 1
        prev = None
        if right -left ==0:
            return head
        while tmp and j < left:
            prev = tmp
            tmp=tmp.next
            j =j+1
        a = self.reverse(tmp,  right+1 - left)
        if not prev:
            return a
        prev.next = a
        return head
```


Time complexity: O(n)  
Space complexity: 1