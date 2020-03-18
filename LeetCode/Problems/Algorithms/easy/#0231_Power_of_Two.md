Given an integer, write a function to determine if it is a power of two.

Example 1:
```
Input: 1
Output: true 
Explanation: 20 = 1
```
Example 2:
```
Input: 16
Output: true
Explanation: 24 = 16
```
Example 3:
```
Input: 218
Output: false
```

---
### My Answer
```python
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        import math
        
        if math.log(n,2) == 0:
            return True
        else:
            return False
```            
Wrong Answer !!! 536870912 -> Output false, but expected true!

---
### Solution
思路：
- 判断是否<=0 或者>2147483647，是的话返回false
- 判断n%2 == 0，是的话n /= 2，循环进行，一旦 n%2 != 0，返回false
- 进行到最后n==1,返回true
```python
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if not n: return False
        
        while n % 2 == 0:
            n = n // 2
            
        return True if n == 1 else False
```        
20 ms, faster than 61.17% ; 11.7 MB, less than 82.35%

### Other Solution - bitwise operation
```
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return not n&n-1 if n else False
```        
8 ms, faster than 99.62% ; 11.8 MB, less than 52.94%
