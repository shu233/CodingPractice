Given two strings **s** and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s** can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. 
_**No two characters may map to the same character but a character may map to itself**_.

Example 1:
```
Input: s = "egg", t = "add"
Output: true
```
Example 2:
```
Input: s = "foo", t = "bar"
Output: false
```
Example 3:
```
Input: s = "paper", t = "title"
Output: true
```

Note:
You may assume both **s** and **t** have the same length.

---
### My Answer
```python
def isIsomorphic(s,t):
    mapping = {}
    for i in range(len(s)):
        if s[i] in mapping:
            if t[i] != mapping[s[i]]:
                return False
        else:
            mapping[s[i]] = t[i]

    return True
```
**Wrong**: s = "ab", t = "aa" -> false! Two characters map to the same!!! => t as key!!!! => Notice: s="aa" t="ab" returns False!

```python
class Solution(object):
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        mapping = {}
        for i in range(len(s)):
            if t[i] in mapping:            # if the char t[i] is already a key, check if its value is s[i]
                if s[i] != mapping[t[i]]:
                    return False
            else:                        # if t[i] is not a key yet, s[i] should not be mapped yet!
                if s[i] in list(mapping.values()):   # check if s[i] has another key: s[i] can be replaced by two chars!!
                    return False
                mapping[t[i]] = s[i]
                
        return True
```        
Success: 20 ms, faster than 97.11% ; 13.1 MB, less than 52.63%






