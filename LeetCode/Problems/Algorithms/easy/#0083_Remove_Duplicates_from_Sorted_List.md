Given a sorted linked list, delete all duplicates such that each element appear only _once_.

Example 1:
```
Input: 1->1->2
Output: 1->2
```
Example 2:
```
Input: 1->1->2->3->3
Output: 1->2->3
```

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None
```

---
### My Answer
```Python
class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return None
        
        newList = p = head
        
        while head.next != None:
            head = head.next
            if head.val != p.val:
                p.next = head
                p = p.next
            else:
                p.next = None
                
        return newList
```        
Success: 24 ms, faster than 94.54% ; 11.9 MB, less than 53.57%        

**Liked List**:
- newList points to the original HEAD
- p is a pointer of newList
- head is the pointer of original linked list
- p always point to the last element of newList
