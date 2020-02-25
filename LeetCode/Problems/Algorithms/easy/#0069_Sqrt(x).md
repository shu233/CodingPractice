Implement `int sqrt(int x)`.

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

Example 1:
```
Input: 4
Output: 2
```
Example 2:
```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```
Hints: 
- Try exploring all integers
- Use the sorted property of integers to reduced the search space.

---
### My Answer
```Python
x = 2147395599

r = 0
for i in range(1,x+1):
        if i*i <= x:
                r = i
        if i*i > x:
                break

print(r)
```
Runtime Error


```Python
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        import math
        return(int(math.sqrt(x)))
```
 16 ms, faster than 93.01% ; 11.7 MB, less than 66.67%    
 
 ---
 ### Solution - with Binary Search
 ```Python
 class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        lo, hi = 0, x
        
        while lo <= hi:
            mid = (lo + hi) // 2
            
            if mid * mid > x:
                hi = mid - 1
            elif mid * mid < x:
                lo = mid + 1
            else:
                return mid
        
        # When there is no perfect square, hi is the the value on the left
        # of where it would have been (rounding down). If we were rounding up, 
        # we would return lo
        return hi
```        


 
