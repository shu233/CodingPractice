Invert a binary tree.

Example:
```
Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
Output:
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```

---
### My Answer - Recursive
```python
class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root: 
            return root
        
        if root.left == None and root.right == None:
            return root
        
        node = root.left
        root.left = self.invertTree(root.right)
        root.right = self.invertTree(node)
        
        return root
```
Success: 16 ms, faster than 80.17% ; 11.9 MB, less than 12.50%

---
### Other Solution - Iterative
 in a manner similar to breadth-first search
 
 - The idea is that we need to swap the left and right child of all nodes in the tree. 
 - So we create a **queue** to store nodes whose left and right child have not been swapped yet. 
 - Initially, only the root is in the queue. 
 - As long as the queue is not empty, remove the next node from the queue, swap its children, and add the children to the queue. 
 - Null nodes are not added to the queue. 
 - Eventually, the queue will be empty and all the children swapped, and we return the original root.
 
 ```python
 class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root: return root
        
        queue = [root]

        while queue:
            node = queue.pop(0)

            temp = node.left
            node.left = node.right
            if node.left != None:
                queue.append(node.left)

            node.right = temp
            if node.right != None:
                queue.append(node.right)

        return root
```        
 16 ms, faster than 80.17% ; 11.8 MB, less than 55.00%


