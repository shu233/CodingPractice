Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, 
determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

**Note that an empty string is also considered valid.**
Example 1:
```
Input: "()"
Output: true
```

Example 2:
```
Input: "()[]{}"
Output: true
```
Example 3:
```
Input: "(]"
Output: false
```
Example 4:
```
Input: "([)]"
Output: false
```
Example 5:
```
Input: "{[]}"
Output: true
```
Hint: **stack** data structure

---
### My Answer:
```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        dic = {'(':')','[':']','{':'}'}
        for i in s:
            if i in ['(','[','{']:
                stack.append(i)
            else:
                if not stack: return(False)
                
                last = stack.pop()
                if not (dic[last] == i): return(False)
                
        return(True if not stack else False)
```
Success: 24 ms, faster than 33.85% ; 11.9 MB, less than 30.25% 

---
### Other Solution
```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        while '()' in s or '{}' in s or '[]' in s:
            s = s.replace('()','').replace('{}','').replace('[]','')
        
        return(s == '')
```
48 ms, faster than 7.65% ; 12 MB, less than 9.24%




