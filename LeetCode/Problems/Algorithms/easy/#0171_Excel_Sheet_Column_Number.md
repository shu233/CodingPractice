Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```    

Example 1:
```
Input: "A"
Output: 1
```
Example 2:
```
Input: "AB"
Output: 28
```
Example 3:
```
Input: "ZY"
Output: 701
```

---
### My Answer
```Python
class Solution(object):
    def titleToNumber(self, s):
        """
        :type s: str
        :rtype: int
        """
        num = 0

        for i in range(len(s)):
            r = ord(s[i]) - 64
            num = num*26 + r
        return num
```        
Success: 20 ms, faster than 63.77% ; 11.8 MB, less than 16.13% 
