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
#### Approach 1: Recursive Approach
Lowest common ancestor for two nodes p and q would be the last ancestor node common to both of them. Here `last` is defined in terms of **the depth of the node**. 

For example, p=0, q=5 => common ancestor nodes: **node 6** and **node 2**, but **node 2** is the last (larger depth)

Algorithm:
1. Start traversing the tree from the root node.
2. If both the nodes p and q are in the right subtree, then continue the search with right subtree starting step 1.
3. If both the nodes p and q are in the left subtree, then continue the search with left subtree starting step 1.
4. If both step 2 and step 3 are not true, this means we have found the node which is common to node p's and q's subtrees. and hence we return this common node as the LCA.
**Values of BINARY TREE: 左边的都比root小，右边的都比root大**
```python
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # Value of current node or parent node.
        parent_val = root.val

        # Value of p
        p_val = p.val

        # Value of q
        q_val = q.val

        # If both p and q are greater than parent
        if p_val > parent_val and q_val > parent_val:    
            return self.lowestCommonAncestor(root.right, p, q)
        # If both p and q are lesser than parent
        elif p_val < parent_val and q_val < parent_val:    
            return self.lowestCommonAncestor(root.left, p, q)
        # We have found the split point, i.e. the LCA node.
        else:
            return root
```            
72 ms, faster than 49.35% _O(N)_; 20.1 MB, less than 6.82% _O(N)_

#### Approach 2: Iterative Approach
Algorithm

The steps taken are also similar to approach 1. The only difference is instead of recursively calling the function, we **traverse down the tree iteratively**. This is possible without using a stack or recursion since we **don't need to backtrace** to find the LCA node. In essence of it the problem is iterative, it just wants us _**to find the split point**_. The point from where p and q won't be part of the same subtree or when one is the parent of the other.
```python
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """

        # Value of p
        p_val = p.val

        # Value of q
        q_val = q.val

        # Start from the root node of the tree
        node = root

        # Traverse the tree
        while node:

            # Value of current node or parent node.
            parent_val = node.val

            if p_val > parent_val and q_val > parent_val:    
                # If both p and q are greater than parent
                node = node.right
            elif p_val < parent_val and q_val < parent_val:
                # If both p and q are lesser than parent
                node = node.left
            else:
                # We have found the split point, i.e. the LCA node.
                return node
 ```               
 72 ms, faster than 49.35% _O(N)_; 21.1 MB, less than 6.82%   _O(1)_             
                
