
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, 
the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and 
it **will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, 
determine the maximum amount of money you can rob tonight **without alerting the police**.

Example 1:
```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```
Example 2:
```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```             

Topic: **Dynamic Programming**

---
### My Answer
并不定非要是间隔一个rob，反例：[2,1,1,2] -> 4 rather than 3!

Objective: 
<img src="http://chart.googleapis.com/chart?cht=tx&chl= rob(n) = max(\sum_{i=1}^{n} x_i\cdot {a_i})" style="border:none;">
suth that <img src="http://chart.googleapis.com/chart?cht=tx&chl= x_{i-1}\cdot {x_i}=0)" style="border:none;">

For the house j: <img src="http://chart.googleapis.com/chart?cht=tx&chl= rob(j) = max(rob(j-1), rob(j-2) + {a_j})" style="border:none;">

Recursion:
```Python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        return self.rob_max(nums,len(nums)-1)
    
    def rob_max(self, nums, i):
        if i == 0: return nums[0]
        if i == 1: return max(nums[0],nums[1])
        return max(self.rob_max(nums,i-1),self.rob_max(nums,i-2)+nums[i])
```        
**Time Limit Exceeded**      !!!   

Bottom-Up DP
```Python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        
        memo = [0 for i in range(len(nums))]
        memo[0] = nums[0]
        if len(nums) > 1:
            memo[1] = max(nums[0],nums[1])
            for i in range(2,len(nums)):
                memo[i] = max(memo[i-1],memo[i-2]+nums[i])
        
        return memo[-1]
```        
Success: 12 ms, faster than 95.58% ; 11.8 MB, less than 44.68% 
