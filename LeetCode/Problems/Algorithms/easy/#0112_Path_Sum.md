Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note**: A leaf is a node with no children.

Example:

Given the below binary tree and `sum = 22`,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```
return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.

Topic: **Depth-first Search**

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
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root: return False
        
        queue = [(root,root.val)]
        while queue:
            node, s = queue.pop(0)
            
            if node.left == None and node.right == None and s == sum: return True
            if node.left != None: queue.append((node.left,s+node.left.val))
            if node.right != None: queue.append((node.right,s+node.right.val))
                
        return False
```
Success: 28 ms, faster than 91.92% ; 15.6 MB, less than 6.82%
