---
author: "Nolan"
title: "Linked list sort"
date: "2021-09-01"
categories: ["algorithm", "linked-list"]
draft: false
description: "Another programing challenge"
tags: ["python", "algorithm"]
ShowToc: false
TocOpen: false
---

## Challenge

Given a linked list, your task is to sort it in ascending order.


## Solution 1 - TLE

Using a bubble sort approach.
```python
class Solution:
    
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        not_sorted = True
        if not head:
            return
        while not_sorted:
            tmp = head
            not_sorted = False
            while tmp.next:
                if tmp.val > tmp.next.val:
                    tmp.val, tmp.next.val  = tmp.next.val, tmp.val
                    not_sorted = True
                tmp = tmp.next
        return head
```

Time Complexity: O(n^2)  

## Solution 2

Using a merge sort approach sort approach.

```python
class Solution:

    def get_len(self, head):
        tmp = head
        l = 0
        while tmp:
            l += 1
            tmp = tmp.next
        return l

    def merge_sort(self, head):
        lenn = self.get_len(head)
        if lenn < 2:
            return head
        mid = lenn // 2
        l = head
        i = 0
        while i < mid-1:
            l = l.next
            i += 1
        r = l.next
        l.next = None
        left = self.merge_sort(head)
        right = self.merge_sort(r)
        return self.merge(left, right)

    def print_list(self, head):
        tmp = head
        while tmp:
            print("val:", tmp.val)
            tmp = tmp.next

    def merge(self, left, right):
        head = ListNode()
        tmp = head
        while left and right:
            if left.val > right.val:
                tmp.next = ListNode(right.val)
                right = right.next
                tmp = tmp.next
            else:
                tmp.next = ListNode(left.val)
                left = left.next
                tmp = tmp.next
        while left:
            tmp.next = ListNode(left.val)
            left = left.next
            tmp = tmp.next
        while right:
            tmp.next = ListNode(right.val)
            right = right.next
            tmp = tmp.next
        return head.next

    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        return self.merge_sort(head)
```

Time complexity: O(n*log n)  