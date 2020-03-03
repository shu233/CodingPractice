Given an array of size n, find the majority element. 
The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:
```
Input: [3,2,3]
Output: 3
```
Example 2:
```
Input: [2,2,1,1,1,2,2]
Output: 2
```

---
### My Answer
```Python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        m = len(nums) // 2
        for i in set(nums):
            if nums.count(i) > m: return i
```            
Success: 152 ms, faster than 71.67% ; 13.3 MB, less than 75.61% 
