Given an array of integers and an integer _k_, 
find out whether there are two distinct indices _i_ and _j_ in the array such that 
**nums[i] = nums[j]** and the **absolute** difference between _i_ and _j_ is at most _k_.

Example 1:
```
Input: nums = [1,2,3,1], k = 3
Output: true
```
Example 2:
```
Input: nums = [1,0,1,1], k = 1
Output: true
```
Example 3:
```
Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```
---
### My Answer
```python
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """  
        for i,e in enumerate(nums):
            if e in nums[i+1:]:
                if nums[i+1:].index(e) +1 <= k:
                    return True
        return False
```
**Time Limit Exceeded** !!!

---
### Solution
#### Approach 1: Using Dictionary
Use a dictionary to save **the most last index** of each num 

=> the keys should be the num: Every num has one ml_index and its value can be updated 

=> For one num: when i(current index) - the_most_last_index > k, it means the old value is invalid, we will try to find the next occurence of num, and the i became the most last index.

```python
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """  
        positions = {}
        for i,n in enumerate(nums):
            if n in positions and i - positions[n] <= k:
                return True
            positions[n] = i
            
        return False
```
Time _O(n)_ / Space _O(n)_

72 ms, faster than 91.63% ; 16.4 MB, less than 64.29%

#### Approach 2: Using Set
Starting from the **k**:

when we consider one num, only the nums with a distance less than k should be considered.

=> a rolling window of length k!

```python
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """  
        rolling_window = set()
        
        for i, n in enumerate(nums):
            if i > k:
                rolling_window.remove(nums[i-k-1])
            if n in rolling_window:
                return True
            rolling_window.add(n)
        
        return False
```        
Time _O(n)_ / Space _O(k)_

80 ms, faster than 54.57% ; 15.7 MB, less than 100.00% 



