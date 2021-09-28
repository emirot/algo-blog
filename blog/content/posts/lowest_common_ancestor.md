---
author: "Nolan"
title: "Lowest Common Ancestors"
date: "2021-08-01"
categories: ["algorithm", "python"]
draft: false
description: "Another challenge"
tags: ["algo", "tree", "recursion"]
ShowToc: false
TocOpen: false
---


## Challenge

Given a binary Tree, find the [lowest common ancestor](https://en.wikipedia.org/wiki/Lowest_common_ancestor) of two nodes.

Example:
LCA(4,9) => 7
LCA()

```
         3
        / \
       7   1
      / \   \
     4   9   2
```


## Solution 1 - Recursion

```python
class Solution:
    
    def helper(self, root, nodes):
        
        if not root:
            return None
        
        if root in nodes:
            return root
        left = self.helper(root.left, nodes)
        right = self.helper(root.right,nodes)
        if left and right:
            return root
        if left and right is None:
            return left
        if right and left is None:
            return right
        
        
    
    def lowestCommonAncestor(self, root: 'TreeNode', nodes: 'List[TreeNode]') -> 'TreeNode':
        return self.helper(root, nodes)
```

## Solution 2 - Iterative

Another strategy is for each node keep in memory his parent.  
Then you can go up the ancestry tree and find the lowest they share.  

E.g searching the common ancestors of multiple nodes.  

```python
class Solution:
    
    def lowestCommonAncestor(self, root: 'TreeNode', nodes: 'List[TreeNode]') -> 'TreeNode':
        if len(nodes)==1:
            return nodes[0]
        ancestors = {}
        stack = [root]
        ancestors[root.val] = None
        ids = {}
        while stack:
            node = stack.pop(0)
            ids[node.val] = node
            if node.left:
                stack.append(node.left)
                ancestors[node.left] = node
            if node.right:
                stack.append(node.right)
                ancestors[node.right] = node
        
        # find paths
        path = defaultdict(int)
        s = defaultdict(int)
        for n in nodes:
            parent = n
            
            while parent:
                path[parent.val] += 1 
                s[path[parent.val]] =   parent.val
                if parent not in ancestors:
                    break
                parent = ancestors[parent]
            

        for k, v in path.items():
            if v == len(nodes):
                return ids[k]
        
            
        return
```