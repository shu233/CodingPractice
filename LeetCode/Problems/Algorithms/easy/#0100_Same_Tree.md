Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

Topic: **Depth-fist Search**

```Python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```


Example 1:
```
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```
Example 2:
```
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```
Example 3:
```
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

---
### My Answer - Recursion
```Python
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if p != None and q != None:
            if p.val != q.val:
                return False
            else:
                return(self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right))
        elif (p == None and q != None) or (p != None and q == None):
            return False
        else:
            return True
```            
Success: 20 ms, faster than 47.66%  ;  12.1 MB, less than 5.00%

---
### Other Solution
#### Approach 2: Iteration
**Intuition**

Start from the root and then at each iteration pop the current node out of the deque. Then do the same checks as in the approach 1 :

- `p` and `p` are not `None`,

- `p.val` is equal to `q.val`,

and if checks are OK, push the child nodes.
```Python
from collections import deque
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        def check(p, q):
            # if both are None
            if not p and not q:
                return True
            # one of p and q is None
            if not q or not p:
                return False
            if p.val != q.val:
                return False
            return True
        
        deq = deque([(p, q),])
        while deq:
            p, q = deq.popleft()
            if not check(p, q):
                return False
            
            if p:
                deq.append((p.left, q.left))
                deq.append((p.right, q.right))
                    
        return True
```
16 ms, faster than 77.46% ; 12 MB, less than 7.50%
