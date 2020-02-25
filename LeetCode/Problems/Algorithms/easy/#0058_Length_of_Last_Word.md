Given a string s consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word (last word means the last appearing word if we loop from left to right) in the string.

If the last word does not exist, return 0.

**Note**: A word is defined as a maximal substring consisting of non-space characters only.

Example:
```
Input: "Hello World"
Output: 5
```

---
### My Answer
```
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        l = s.split()
        
        if (not l) or (not l[-1]): return 0
        
        return len(l[-1])
```
Success: 20 ms, faster than 48.43% ; 12 MB, less than 10.71%  
  
