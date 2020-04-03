Given a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.

Example:
```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```
**Depth-first Search**

---
### My Answer
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        if not root: return []
        
        stack = [(root,str(root.val))]
        res = []
        while stack:
            node, path = stack.pop()
            if node.left == None and node.right == None:
                res.append(path)
            if node.left:
                stack.append((node.left, path+'->'+str(node.left.val)))
            if node.right:
                stack.append((node.right, path+'->'+str(node.right.val)))
                
        return res
```        
Success: 20 ms, faster than 62.25% ; 12.7 MB, less than 5.26% 
