Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:
```
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```
return its depth = 3.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
```

---
### My Answer
```Python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        
        if not root: return 0
        return max(self.maxDepth(root.left),self.maxDepth(root.right)) + 1
```        
Success: 36 ms, faster than 25.03% ; 14.6 MB, less than 59.26%        

---
### Other Solution - with the help of stack
```Python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        
        stack = [(root,1)]
        re = 0 # Current max depth
        while stack:
            node, level = stack.pop()
            
            if not node.left and not node.right:
                re = max(re,level)
                
            if node.left:
                stack.append((node.left,level+1))
            if node.right:
                stack.append((node.right,level+1))
                
        return re
```        
36 ms, faster than 25.03% ; 14.6 MB, less than 53.09%        
        
---

[Binary Tree](https://blog.csdn.net/sinat_35261315/article/details/78921925)


