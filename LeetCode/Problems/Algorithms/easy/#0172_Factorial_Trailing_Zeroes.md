Given an integer n, return the number of trailing zeroes in n!.

Example 1:
```
Input: 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```
Example 2:
```
Input: 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```
Note: Your solution should be in logarithmic time complexity.

---
### My Answer
```Python
class Solution(object):
    def trailingZeroes(self, n):
        """
        :type n: int
        :rtype: int
        """
        from math import factorial
        s = factorial(n)
        
        i = 0
        while s:
            if s % 10 == 0:
                i += 1
                s = s // 10
            else:
                return i
```                
**Time Limit Exceeded** !!!

---
### Solution
```Python
class Solution:
    def trailingZeroes(self, n: int) -> int:
        if n<5:
            return 0
        
        ans=0
        while n!=0: 
            n=n//5
            ans+= n
        
        return ans
```        
20 ms, faster than 47.50%  ;  11.8 MB, less than 41.18%
