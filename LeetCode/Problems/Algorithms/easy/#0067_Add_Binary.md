Given two binary strings, return their sum (also a binary string).

The input strings are both **non-empty** and contains only characters `1` or `0`.

Example 1:
```
Input: a = "11", b = "1"
Output: "100"
```
Example 2:
```
Input: a = "1010", b = "1011"
Output: "10101"
```

---
### My Answer
```
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        a = int(a,2)
        b = int(b,2)
        c = a + b
        
        return bin(c)[2:]
```
Success: 16 ms, faster than 92.30%; 11.7 MB, less than 68.42%     
        
