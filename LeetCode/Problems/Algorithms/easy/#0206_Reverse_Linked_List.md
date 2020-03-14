Reverse a singly linked list.

Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None
```

---
### My Answer
#### 1. Iterative
Create a new linked list, and add node (the head of the old list) at the beginning subsequently.

```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return None
        
        new_head = head
        new_head.next = None
        head = head.next
        
        while head:
            add_node = head
            add_node.next = new_head
            new_head = add_node
            head = head.next
            
        return new_head
```        
**FALSE**: =赋值 其实是指向同一个object，所以当改变new_head时，head的内容也改变了，原list中断了。

[1,2,3,4,5] -> returns [1], BUT expected [5,4,3,2,1]

Create a new Node in each step?
```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return None
        
        new_head = ListNode(head.val)
        head = head.next
        
        while head:
            add_node = ListNode(head.val)
            add_node.next = new_head
            new_head = add_node
            head = head.next
            
        return new_head
```        
Success: 32 ms, faster than 16.94%  ;  15.6 MB, less than 19.44%         

In-Space: move the head to the tail => NO: Cannot find the tail!!!

In-Space: Changing the direction of arrows one by one: Time complexity : _O(n)_
```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return None
        
        tail1, head2 = head, head.next
        tail1.next = None
        
        while head2:
            move_node = head2
            head2 = head2.next
            
            move_node.next = tail1
            tail1 = move_node
            
        return tail1
```        
Success: 20 ms, faster than 88.57% ; 13.7 MB, less than 44.44% 

---
### Solution - Recursive
The recursive version is slightly trickier and the key is to work **backwards**. Assume that the rest of the list had already been reversed, now how do I reverse the front part?

Consider `n_1 → … → n_{k-1} → n_k → n_{k+1} → … → n_m → Ø`:

Assume from node n_{k+1} to n_m had been reversed and you are at node nk: `n_1 → … → n_{k-1} → n_k → n_{k+1} ← … ← n_m`

We want n_{k+1}’s next node to point to n_k. So, _**n_k.next.next = n_k**_;

Be very careful that n1's next must point to Ø. If you forget about this, your linked list has a cycle in it. 
```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        
        p = self.reverseList(head.next)
        head.next.next = head
        head.next = None
            
        return p
```        
24 ms, faster than 68.59% ; 17.3 MB, less than 9.26%




