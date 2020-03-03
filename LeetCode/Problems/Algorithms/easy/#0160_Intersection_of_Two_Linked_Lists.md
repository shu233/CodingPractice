Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:
```
A:       a1 -> a2 ->
                     c1 -> c2 -> c3
B: b1 -> b2 -> b3 ->
```
begin to intersect at node c1.

Example 1:
```
A:      4 -> 1 ->
                  8 -> 4 -> 5
B: 5 -> 0 -> 1 ->

Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). 
From the head of A, it reads as [4,1,8,4,5]. 
From the head of B, it reads as [5,0,1,8,4,5]. 
There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

Exanple 2:
```
A: 2 -> 6 -> 4

B:      1 -> 5

Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. 
                    Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

**Notes**:

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in _O(n)_ time and use only _O(1)_ memory.

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
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None: return None
        
        pres = []
        while headA is not None or headB is not None:
            if headA is not None:
                if headA not in pres:
                    pres.append(headA)
                    headA = headA.next
                else:
                    return headA
                 
            if headB is not None:
                if headB not in pres:
                    pres.append(headB)
                    headB = headB.next
                else:
                    return headB
            
        return None
```
**Time Limit Exceeded** !!!

---
### Solution
#### Approach 1: Brute Force
For each node ai in list A, traverse the entire list B and check if any node in list B coincides with ai.
```Python
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None: return None
        
        while headA != None:
            pb = headB
            while pb != None:
                if pb == headA: return headA
                pb = pb.next
            headA = headA.next
        return None
```        
Time Limit Exceeded

Complexity Analysis:
- Time complexity : O(mn).
- Space complexity : O(1).

#### Approach 2: Hash Table
Traverse list A and store the address / reference to each node in a hash set. Then check every node bi in list B: 
if bi appears in the hash set, then bi is the intersection node.
- Time complexity : O(m+n).
- Space complexity : O(m) or O(n)

```Python
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None: return None
        
        nodesA = []
        while headA != None:
            nodesA.append(headA)
            headA = headA.next
        while headB != None:
            if headB in nodesA: return headB
            headB = headB.next
            
        return None
```        
Time Limit Exceeded

#### Approach 3: Two Pointers
- Maintain two pointers pA and pB initialized at the head of A and B, respectively. Then let them both traverse through the lists, one node at a time.
- When pApA reaches the end of a list, then redirect it to the head of B (yes, B, that's right.); similarly when pB reaches the end of a list, redirect it the head of A.
- If at any point pA meets pB, then pA/pB is the intersection node.

```Python
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if headA is None or headB is None: return None
        
        pa = headA
        pb = headB
        while pa != pb:
            pa = pa.next if pa != None else headB
            pb = pb.next if pb != None else headA
        return pa
```        
204 ms, faster than 42.09%  ; 41.9 MB, less than 16.00%
