Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up**:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

---
### My Answer
```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        s = min(nums)
        for i in range(len(nums)):
            sums = [sum(nums[i:x]) for x in range(i+1,len(nums)+1)]
            if max(sums) > s : s = max(sums) 
            
        return s
``` 
**Time Limit Exceeded**
  
---
### Solutions:
```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        
        s_max = s = nums[0]
        for i in range(1,len(nums)):
            s = nums[i] if s < 0 else s + nums[i]
            s_max = s if s > s_max else s_max
            
            
        return s_max
```

44 ms, faster than 95.64%; 12.4 MB, less than 43.59% 
