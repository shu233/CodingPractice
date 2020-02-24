Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:
```
Input: [1,3,5,6], 5
Output: 2
```
Example 2:
```
Input: [1,3,5,6], 2
Output: 1
```
Example 3:
```
Input: [1,3,5,6], 7
Output: 4
```
Example 4:
```
Input: [1,3,5,6], 0
Output: 0
```

---
### My Answer
```
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if target in nums:
            return(nums.index(target))
        else:
            for i in range(len(nums)):
                if target <= nums[i]:
                    return(i)
            return(len(nums))
```
Success: 40 ms, faster than 37.52% ; 12.4 MB, less than 10.53%

---
### Other Solution: Using Enumerate
```
for i,n in enumerate(nums):
        if target <= n:
            return i
        
        return len(nums)
```

36 ms, faster than 68.21%; 12.3 MB, less than 22.81%


