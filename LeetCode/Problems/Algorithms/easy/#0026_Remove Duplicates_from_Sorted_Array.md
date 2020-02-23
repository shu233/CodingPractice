Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

Example 1:
```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

Example 2:
```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```
Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference* (**i.e., without making a copy**), which means modification to the input array will be known to the caller as well.

---
### My Answer
注意这题要求空间复杂度为O(1) ,即在原数组的基础上进行数据的处理。
我们看数组可以发现，只需要设置一个游标，然后如果有不同的数字就复制到游标的最新位置，遍历一波数组即可完成操作。

```
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        k = 1
        for i in range(len(nums)-1):
            if nums[i] != nums[i+1]:
                nums[k] = nums[i+1]
                k += 1
        
        return k
```

Success: 72 ms, faster than 56.38% ; 13.6 MB, less than 56.25% 

