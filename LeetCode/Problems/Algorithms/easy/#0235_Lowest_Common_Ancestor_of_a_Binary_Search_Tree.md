Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we **allow a node to be a descendant of itself**).”

Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]
```
       6
    /    \
   2      8
 / \     / \
0   4   7   9
   / \
  3   5
```

Example 1:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

Example 2:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
```

Note:
- All of the nodes' values will be unique.
- p and q are different and both values will exist in the BST.

```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```
---
### My Answer
```python
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        def nodeInTree(node, tree_root):
            if not tree_root: return False
            tree = [tree_root]
            while tree:
                n = tree.pop()
                if n.val == node.val:
                    return True
                if n.right:
                    tree.append(n.right)
                if n.left:
                    tree.append(n.left)    
            return False
        
        if not root: return None
        stack = [root]
        while stack:
            lca = stack.pop()
            left, right = lca.left, lca.right
            
            if lca.val == p.val or lca.val == q.val:    # if the current node is one searched value
                return lca
            
            if (nodeInTree(p,left) and nodeInTree(q,right)) or (nodeInTree(q,left) and nodeInTree(p,right)):  # if the two values in two separated subtrees
                return lca
            elif left and (left.val == p.val or left.val == q.val):
                return left
            elif right and (right.val == p.val or right.val == q.val):
                return right
            
            if right: stack.append(right)
            if left: stack.append(left)
```            
104 ms, faster than 5.59% ; 20.9 MB, less than 6.82%

---
### Solutions


