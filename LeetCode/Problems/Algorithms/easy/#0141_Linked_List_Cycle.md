Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. 
If `pos` is -1, then there is no cycle in the linked list.

Example 1:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

Example 2:
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

Example 3:
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

Follow up:

Can you solve it using _O(1)_ (i.e. constant) memory?

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None
```

---
### My Answer - Two Pointers
创建两个指针，一个的速度是另一个的两倍，如果有循环那他们就会相遇，叫弗洛伊德判圈算法（龟兔赛跑算法）
```Python
class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head == None or head.next == None:return False
        
        try:
            p1 = head
            p2 = head.next
            while p1 is not p2:
                p1 = p1.next
                p2 = p2.next.next
            return True
        except:
            return False
```            
44 ms, faster than 39.56% ; 18.4 MB, less than 22.70%

The space complexity can be reduced to _O(1)_ by considering two pointers at different speed - a slow pointer and a fast pointer. The slow pointer moves one step at a time while the fast pointer moves two steps at a time.

If there is no cycle in the list, the fast pointer will eventually reach the end and we can return false in this case.



---
### Solution
#### Approach 1: Hash Table
To detect if a list is cyclic, we can check whether a node had been visited before. A natural way is to use a hash table.

We go through each node one by one and record each node's **reference (or memory address)** in a hash table. If the current node is `null`, we have reached the end of the list and it must not be cyclic. If current node’s reference is in the hash table, then return true.
```Python
class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        nodes = set()
        while head is not None:
            if head in nodes:
                return True
            else:
                nodes.add(head)
                head = head.next
        return False
```        
36 ms, faster than 84.09% ; 18.8 MB, less than 12.06%

Time complexity : _O(n)_ ; Space complexity: _O(n)_

#### 
