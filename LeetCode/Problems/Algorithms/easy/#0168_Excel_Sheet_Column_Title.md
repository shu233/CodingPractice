Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```
Example 1:
```
Input: 1
Output: "A"
```
Example 2:
```
Input: 28
Output: "AB"
```
Example 3:
```
Input: 701
Output: "ZY"
```
---
### My Answer
```Python
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        dic = {i+1:chr(65+i) for i in range(26)}
        
        if n <= 26: return(dic[n])
        else:
            res = []
            while n > 0:
                x = n % 26
                n = n // 26

                if x != 0:
                    res.append(dic[x])
                else:
                    res.append(dic[26])
                    n -= 1 

            return(''.join(res[::-1]))
```            
Success: 16 ms, faster than 69.07% ; 11.9 MB, less than 6.67%             

---
### Other Solution
```Python
class Solution:
    def convertToTitle(self, n: int) -> str:
    	s = ''
    	while n > 0:
    		r = n%26
    		if r == 0: r = 26
    		s = chr(64+r)+s
    		n = int((n-r-1)/26)
    	return(s)
```      
16 ms, faster than 69.07% ; 11.8 MB, less than 33.33% 
