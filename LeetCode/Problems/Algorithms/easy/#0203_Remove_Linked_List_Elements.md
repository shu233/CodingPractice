Remove all elements from a linked list of integers that have value _**val**_.

Example:
```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None
```

---
### My Answer
- Notice: handling the first Node!

```python
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        if not head: return None
        if head.val == val:
            head = head.next
            return self.removeElements(head,val)
    
        pre = head
        while pre != None and pre.next != None:
            if pre.next.val == val:
                pre.next = pre.next.next
            else:
                pre = pre.next      
        return head
```
Success: 68 ms, faster than 39.65% ; 23 MB, less than 6.90%


---
### Other Solution
#### Approach 1: using one pointer for previous node
```python
class Solution(object):
    def removeElements(self, head, val):
        prev, current = None, head
        while current:
            if current.val == val:
                if prev:
                    # Remove the current node in the normal way.
                    prev.next = current.next
                    current = current.next
                else:
                    # We are at the head, advance the head and keep prev as None.
                    head = head.next
            else:
                # Advance the prev pointer.
                prev = current
            # Advance the current pointer.
            current = current.next
        return head
```
64 ms, faster than 61.73% ; 18.8 MB, less than 10.34% 

#### Approach 2: using dummy head
- The idea here is we do not know **where** `val` will appear, it could very well appear at the _beginning_ of the list. 
- To take care of this case we create _**a dummy_head that point to the current head**_. 
- To remove a list element we need to wire the node preceding `val` to the node following `val`. 
- We look ahead starting at the dummy node to see if the next node contains `val`. 
- If it does we wire the current node next to `next.next`, that is the node after val. 
- If val is not in the next node we just move our current node there.
```python
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummy_head = ListNode(0)
        dummy_head.next = head
        node = dummy_head
        while node.next:
            if node.next.val == val:
                node.next = node.next.next
            else:
                node = node.next
        return dummy_head.next
```
60 ms, faster than 80.47% ; 18.9 MB, less than 10.34%
