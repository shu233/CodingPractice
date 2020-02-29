Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

**Note**: A leaf is a node with no children.

Example:

Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
return its minimum depth = 2.
```

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
Idea: traversal the tree level by level, if the node is a leaf, then return the depth and end the code
```Python
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        
        queue = [(root,1)]
        while queue:
            node, depth = queue.pop(0)
            
            if self.isLeaf(node):return depth
            if node.left != None: queue.append((node.left,depth+1))
            if node.right != None: queue.append((node.right,depth+1))
                
    
    def isLeaf(self, node):
        return node.left == None and node.right == None
```        
Success: 32 ms, faster than 73.85%  ; 14.7 MB, less than 38.46%     

---
### Other Solution
```Python
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        
        if root.left and root.right:
            return min(self.minDepth(root.left), self.minDepth(root.right)) + 1
        else:
            return max(self.minDepth(root.left), self.minDepth(root.right)) + 1
```            
40 ms, faster than 27.01% ; 14.7 MB, less than 56.41%            
