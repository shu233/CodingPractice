Merge two sorted linked lists and return it as a new list. 
The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
**Single Linked List**

--- 
### My Answer
Hint: [数据结构之单向链表](https://blog.csdn.net/weixin_39881922/article/details/80470896)

遍历解法:
同时不断遍历两个链表，取出小的追加到新的头节点后，直至两者其中一个为空;
再将另一者追加的新链表最后

```
# Definition for singly-linked list.
#class ListNode(object):
#    def __init__(self, x):
#        self.val = x
#        self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """    
        head = pre = ListNode(-1)

        while l1 or l2:
            if not l1:
                pre.next = l2
                break
            elif not l2:
                pre.next = l1
                break
            elif l1.val < l2.val:
                pre.next = l1
                l1 = l1.next
            else:
                pre.next = l2
                l2 = l2.next
            pre = pre.next
            
        return head.next
```
Success: 28 ms, faster than 44.80% ; 11.9 MB, less than 31.03%

---

### Other Solution: Recursion
```
class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1: return l2
        if not l2: return l1
        
        if l1.val < l2.val:
            l1.next =  self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```
24 ms, faster than 73.78%; 11.9 MB, less than 33.33% 



