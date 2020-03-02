Given a **non-empty** array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a _linear runtime complexity_. Could you implement it without using extra memory?

Example 1:
```
Input: [2,2,1]
Output: 1
```
Example 2:
```
Input: [4,1,2,1,2]
Output: 4
```

---
### My Answer
```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        for i in nums:
            if nums.count(i) == 1: return i
```
Success: 6248 ms, faster than 5.02% ; 13.7 MB, less than 43.24%

---
### Solutions
#### Approach 1: List operation
Algorithm

Iterate over all the elements in \text{nums}nums
If some number in \text{nums}nums is new to array, append it
If some number is already in the array, remove it

Time complexity : _O(n^2)_

#### Approach 2: Hash Table
We use hash table to avoid the O(n)O(n) time required for searching the elements.

1. Iterate through all elements in `nums`
2. Try if _hash table_ has the key for `pop`
3. If not, set up key/value pair
4. In the end, there is only one element in _hash table_, so use `popitem` to get it

Time complexity : O(n * 1) = O(n)
```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        hash_table = {}
        for i in nums:
            try:
                hash_table.pop(i)
            except:
                hash_table[i] = 1
            
        return hash_table.popitem()[0]
```        
80 ms, faster than 36.99% ; 14.4 MB, less than 6.75%

#### Approach 3: Math
2*(a+b+c)−(a+a+b+b+c)=c
```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return 2*sum(set(nums)) - sum(nums)
```        
72 ms, faster than 66.99% ; 14 MB, less than 29.73% 


#### Approach 4: Bit Manipulation
- If we take XOR of zero and some bit, it will return that bit: a XOR 0 = a
- If we take XOR of two same bits, it will return 0: a XOR a = 0
- a XOR b XOR a = (a XOR a) XOR b = 0 XOR b = b
So we can XOR all bits together to find the unique number.
```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        a = 0
        for i in nums:
            a ^= i
        return a
```        
72 ms, faster than 66.99% ; 13.7 MB, less than 45.94%
