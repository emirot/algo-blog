---
author: "Nolan"
title: "Recover BST"
date: "2021-09-24"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "Binary Search Tree"]
ShowToc: false
TocOpen: false
---

## Challenge

You are given the root of a binary search tree, where exactly two nodes of the tree were swapped by mistake.  
Recover the tree without changing its structure.

## Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def in_order_traversal(self, root):
        if root is None:
            return

        self.in_order_traversal(root.left)
        self.arr.append([root.val, root])
        self.in_order_traversal(root.right)

    
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        self.arr = []
        self.in_order_traversal(root)
        i = 0
        to_move = []
        orderone = sorted([e[0] for e in self.arr])
        while i < len(self.arr):
            if self.arr[i][0] != orderone[i]:
                to_move.append(self.arr[i])
            i += 1
        if len(to_move)>1:
            if to_move[0] > to_move[1]:
                to_move[0][1].val, to_move[1][1].val = to_move[1][1].val, to_move[0][1].val
        return 
```

Time complexity: O(n)  
Space complexity: O(n)  