Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.

Example 1:
```
Input: "A man, a plan, a canal: Panama"
Output: true
```
Example 2:
```
Input: "race a car"
Output: false
```
Example 3:
```
Input: "0P"
Output:false
```

---
### My Answer
```Python
import re
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s: return True
        
        s = re.sub(r'[^A-Za-z]', '', s).lower()
        if len(s) == 1: return True
        
        mid = len(s)//2
        return s[:mid] == s[-mid:][::-1]
```        
WRONG ANSWER!!! "0P" -> expected false! "a." -> expected true?!?!?!
=> alphanumeric!!!

```Python
s = re.sub(r'[^A-Za-z0-9]', '', s).lower()
```
Success: 28 ms, faster than 94.25% ; 13.8 MB, less than 37.25%

---
### Solution
```Python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        left, right = 0, len(s) - 1  # two pointers
        while left < right:
            if s[left].isalnum() and s[right].isalnum():
                if s[left].lower() != s[right].lower():  # ignoring cases
                    return False
                else:
                    left += 1
                    right -= 1
            elif not s[left].isalnum():  # left is not a alphanumeric
                left += 1
            else:  # right is not a alphanumeric
                right -= 1
        return True
```
40 ms, faster than 62.85% ; 12.7 MB, less than 60.78% 
