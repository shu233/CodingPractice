Given a binary tree, return the bottom-up level order traversal of its **nodes' values**. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```   
return its bottom-up level order traversal as:
```
[
  [15,7],
  [9,20],
  [3]
]
```

Topic: **Breadth-first Search**

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
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return None
        
        traversal = [(root,1)]       
        stack = {1:[root.val]}       
        while traversal:
            node, level = traversal.pop(0)
            
            level_list = [] if stack.get(level+1) == None else stack.get(level+1)
            
            if node.left != None:
                level_list.append(node.left.val)
                traversal.append((node.left, level+1))
            if node.right != None:
                level_list.append(node.right.val)
                traversal.append((node.right, level+1))
                
            stack[level+1] = level_list
            
        res = []
        for k in range(1,len(stack))[::-1]:
            res.append(stack[k])
        
        return res
```
Success: 16 ms, faster than 96.46%  ; 12.4 MB, less than 30.43% 

Idea:
- traversal from the root: FIFO
- return lists: each level has its own list

Improve: remove stack, directly use res list by using index as impliment of level
```Python
class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return None
        
        traversal = [(root,0)]       
        res = [[root.val]]       
        while traversal:
            node, level = traversal.pop(0)
            
            level_list = [] if level+1 > len(res)-1 else res[level+1]
            
            if node.left != None:
                level_list.append(node.left.val)
                traversal.append((node.left, level+1))
            if node.right != None:
                level_list.append(node.right.val)
                traversal.append((node.right, level+1))
                
            if level_list:    
                if level+1 > len(res)-1: res.append(level_list)
                else: res[level+1] = level_list
        
        return res[::-1]
```
Success: 20 ms, faster than 82.95% ; 12.3 MB, less than 56.52%



