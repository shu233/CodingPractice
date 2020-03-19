Given a singly linked list, determine if it is a palindrome.

Example 1:
```
Input: 1->2
Output: false
```
Example 2:
```
Input: 1->2->2->1
Output: true
```

Follow up:
Could you do it in _O(n)_ time and _O(1)_ space?

```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None
```

---
### My Answer
```python
class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        temp = []
        while head:
            temp.append(head.val)
            head = head.next
          
        return temp == temp[::-1]
```
Success: 64 ms, faster than 90.12% ; 31 MB, less than 24.14%

---
### Solution
For _O(1)_ space? => Only use auxiliary pointers/nodes!

key point: reverse the first half of the linked list while scanning.
```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if not head or not head.next:
            return True

        dummy_head = ListNode(None)
        dummy_head.next = head
        
        # find the half-th node and reverse it while scanning
        pre, slow, fast = None, dummy_head, dummy_head
        while fast and fast.next:
            tmp = slow
            slow, fast = slow.next, fast.next.next

            tmp.next = pre
            pre = tmp
        
        tmp = slow.next
        if not fast:
            slow = pre
        else:
            slow.next = pre
        fast = tmp
        
        # compare
        while slow and fast:
            if slow.val != fast.val:
                return False
            else:
                slow, fast = slow.next, fast.next
        
        return True
```
64 ms, faster than 90.12% ; 30.9 MB, less than 48.28%
