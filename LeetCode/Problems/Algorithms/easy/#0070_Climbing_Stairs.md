You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note**: Given n will be a positive integer.

Hint: To reach n-th step, what could have been your previous steps? (Think about the step sizes)

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

Topic: **Dynamic Programming**

---
### My Answer

---
### Solution:
#### Idea: 求 ways(n)
考虑第n阶：
- **1**： 与第`n-1`阶有关 -> 确定最后一步为1: 在所有`ways(n-1)`的所有可能性后加1步，可能性数量不变，`ways(n-1)` 
- 或 **2**：与第`n-2`阶有关 -> 确定最后一步为2: 在所有`ways(n-2)`的所有可能性后加2步，可能性数量不变，`ways(n-2)`
- 两种可能性相加：`[n] = ways[n - 1] + ways[n - 2]`

-> like _**fabonacci sequence**_ !!

```Python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 2: return n
        
        ways = [1,2,3]
        for i in range(3,n+1):
            ways[2] = ways[0] + ways[1]
            ways[0] = ways[1]
            ways[1] = ways[2]
            
        return ways[2]
```        
16 ms, faster than 70.07% ; 11.7 MB, less than 53.13%      
