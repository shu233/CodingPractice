Given a binary tree, determine if it is _height-balanced_.

For this problem, a height-balanced binary tree is defined as:
> a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

Example 1:

Given the following tree `[3,9,20,null,null,15,7]`:
```
    3
   / \
  9  20
    /  \
   15   7
```   
Return true.

Example 2:

Given the following tree `[1,2,2,3,3,null,null,4,4]`:
```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
``` 
Return false.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
```
---
### My Answer - Recursion
```Python
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root: return True
        
        def height(node):
            if node == None: return 0
            return max(height(node.left), height(node.right)) + 1

        l_height = height(root.left) 
        r_height = height(root.right)
        
        return abs(l_height-r_height)<=1 and self.isBalanced(root.left) and self.isBalanced(root.right)
```
Success: 52 ms, faster than 43.80% ; 17.4 MB, less than 6.25% 

* Put the `height(node)` function outside of `isBalanced()`: slower but less memory (64 ms, faster than 19.90%; 16.5 MB, less than 62.50% )
* Note: in this method there are many duplicated visitings of nodes to calculate the their height.
* How about store the heights in a list to save calculating time?

---
### Other Solution
#### Approach 1:
Store the answer in a global variable and calculate the height at every node. Exit early if an unbalanced subtree is found.
```Python
class Solution(object):
    answer = True
    def height_helper(self, root):
        if root is None or not self.answer:
            return 0
        left_height = self.height_helper(root.left)
        right_height = self.height_helper(root.right)
        if abs(left_height - right_height) > 1:
            self.answer = False
        return max(left_height, right_height) + 1

    def isBalanced(self, root):
        self.height_helper(root)
        return self.answer
```
40 ms, faster than 78.64% ; 16.6 MB, less than 43.75%

