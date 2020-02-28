Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a **height-balanced binary tree** is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:
```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
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
### My Answer: Divide and Conquer
```Python
class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums: return None
        
        middle = len(nums) // 2
        root = TreeNode(nums[middle])
        root.left = self.sortedArrayToBST(nums[:middle])
        root.right = self.sortedArrayToBST(nums[middle+1:])
        
        return root
```        
Success: 68 ms, faster than 25.64% ; 16 MB, less than 63.64%

Idea: cause inorder traversal in BST will get sorted order，
so the **middle of sorted list**  always be the root no matter for whole tree or left/right children.



        
 
