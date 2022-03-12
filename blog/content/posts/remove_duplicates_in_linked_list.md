---
author: "Nolan"
title: "Remove Duplicates From an Unsorted Linked List"
date: "2021-03-12"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "linked-list"]
ShowToc: false
TocOpen: false
---

## Challenge

Given the head of a linked list, find all the values that appear more than once in the list and delete the nodes that have any of those values.  
  
Return the linked list after the deletions.   

e.g
```
1 -> 2 ->3 ->2 returns 1 -> 3
```

## Solution

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    
    def print_list(self, head):
        tmp = head
        while tmp:
            print(tmp.val, end=", ")
            tmp = tmp.next
    
    def deleteDuplicatesUnsorted(self, head: ListNode) -> ListNode:
        tmp = head
        oc = defaultdict(int)
        while tmp:
            oc[tmp.val] += 1
            tmp = tmp.next
        tmp = head
        prev = head
        while tmp:
            if oc[tmp.val] > 1 and tmp == head:     
                head = tmp.next
                prev = head
            elif oc[tmp.val] > 1:
                prev.next = tmp.next
            else:
                prev = tmp
            tmp = tmp.next
        self.print_list(head)
        return head

```

## Solution 2 - Using dummy node

```python
    def deleteDuplicatesUnsorted(self, head: ListNode) -> ListNode:
        tmp = head
        oc = defaultdict(int)
        while tmp:
            oc[tmp.val] += 1
            tmp = tmp.next
        fake = ListNode()
        fake.next = head
        prev = fake
        tmp = head
        while tmp:
            if oc[tmp.val] > 1:
                prev.next = tmp.next
            else:
                prev = tmp
            tmp = tmp.next
        return fake.next
```