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
