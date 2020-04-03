Given two strings s and t , write a function to determine if t is an anagram of s.

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```
Example 2:
```
Input: s = "rat", t = "car"
Output: false
```

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

---
### My Answer
易位构词是一类文本游戏（更准确地说是一类“词语游戏”），是将组成一个词或短句的**字母重新排列顺序**，原文中所有字母的每次出现都被使用一次，这样构造出另外一些新的词或短句。

Idea: get the list of all characters, and sort them. (cannot use set: some char might appear several times)
```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        l1 = sorted(list(s))
        l2 = sorted(list(t))
        return l1==l2
```        
Succeed: 48 ms, faster than 45.49% ;  14.6 MB, less than 5.26%

**Python中排序函数sort()和sorted()的区别**
- sort()方法是在原来的列表上直接进行排序，并没有返回一个新的列表，所以返回值为None
- sorted()函数排好序后会返回一个新的列表，原来的列表并没有发生改变
Example:
```python
s='acdb'

l1 = list(s)
l1.sort()
print(l1)
```
Output: `['a', 'b', 'c', 'd']`
等于：
```python
s='acdb'

l1 = sorted(list(s))
print(l1)
```
Output: `['a', 'b', 'c', 'd']`

---
### Another Solution - Hash Table
Idea: To examine if t is a rearrangement of s, we can count occurrences of each letter in the two strings and compare them. Since both s and t contain only letters from a-z, a simple counter table of size 26 is suffice.

Do we need two counter tables for comparison? Actually no, because we could **increment the counter for each letter in s and decrement the counter for each letter in t, then check if the counter reaches back to zero**.

```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t):
            return False
        
        for e in set(s):
            if s.count(e) != t.count(e):
                return False
        
        return True
```        
24 ms, faster than 98.16% ; 13.6 MB, less than 15.79% 

