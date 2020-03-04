Given an array, rotate the array to the right by _k_ steps, where _k_ is non-negative.

Example 1:
```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```
Example 2:
```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

Note:
- Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space?

Hints:
- The easiest solution would use additional memory and that is perfectly fine.
- The actual trick comes when trying to solve this problem without using any additional memory. 
This means you need to use the original array somehow to move the elements around. 
Now, we can place each element in its original location and **shift** all the elements around it to adjust as that would be **too costly** and most likely will time out on larger input arrays.
- One line of thought is based on reversing the array (or parts of it) to obtain the desired result. Think about how reversal might potentially help us out by using an example.
- The other line of thought is a tad bit complicated but essentially it builds on the idea of placing each element in its original position 
while keeping track of the element originally in that position. 
Basically, at every step, we place an element in its rightful position 
and keep track of the element already there or the one being overwritten in an additional variable. 
We can't do this in one linear pass and the idea here is based on **cyclic-dependencies** between elements.

---
### My Answer - Using Cyclic Replacements 
We can directly place every number of the array at its required correct position.
```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        if k != 0:
            temp = nums[-k:]
            nums[k:] = nums[:len(nums)-k]
            nums[:k] = temp
```            
Wrong Answer! [1,2] 3 -> Excepted: [2,1] NOT [1,2]

Corrected:
```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        if k != 0:
            k = k-len(nums) if k > len(nums) else k
            temp = nums[-k:]
            nums[k:] = nums[:len(nums)-k]
            nums[:k] = temp
```         
Success: 48 ms, faster than 72.65% ; 12.2 MB, less than 37.50%

Other Answer:

only use _O(1)_ memory size
```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        for i in range(k):
            temp = nums[-1]
            nums[1:] = nums[:-1]
            nums[0] = temp
```
Time Limit Exceeded! 

---
### Solution - Using Reverse 
This approach is based on the fact that when we rotate the array k times, k%nk elements from the back end of the array come to the front and the rest of the elements from the front shift backwards.

```
Original List                   : 1 2 3 4 5 6 7
After reversing all numbers     : 7 6 5 4 3 2 1
After reversing first k numbers : 5 6 7 4 3 2 1
After revering last n-k numbers : 5 6 7 1 2 3 4 --> Result
```

```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        k = k % len(nums)
        
        nums[:] = nums[::-1]
        nums[:k] = nums[:k][::-1]
        nums[k:] = nums[k:][::-1]
```        
52 ms, faster than 48.28% ; 12.2 MB, less than 35.42%
