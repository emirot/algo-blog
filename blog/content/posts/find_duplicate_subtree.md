---
author: "Nolan"
title: "Find duplicate subtrees"
date: "2021-09-10"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "tree"]
ShowToc: false
TocOpen: false
---


## Challenge

Given the root of a binary tree, return all duplicate subtrees.
You only need to return the root of any of them.

## Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def __init__(self):
        self.all_node = []
        self.ans = []
        self.s = set()
        
    def preorder(self, root, arr):

        arr.append(root.val)
            
        if root.left:
            self.preorder(root.left, arr)
        else:
            arr.append(None)
            
        if root.right:
            self.preorder(root.right, arr )
        else: 
            arr.append(None)
        return arr
    
    def get_subtree(self, root):
        res = [self.preorder(root, []), root]
        current, root = res
        
        if current in self.all_node and tuple(current) not in self.s:
            self.ans.append(root)
            self.s.add(tuple(current))
        else:
            self.all_node.append(current)

    
    def findDuplicateSubtrees(self, root: Optional[TreeNode]) -> List[Optional[TreeNode]]:
        queue = [root] 
        while queue:
            node = queue.pop(0)
            self.get_subtree(node)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        return self.ans
```

Time Complexity: O(n^2)  