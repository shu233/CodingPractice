Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
Example 1:
```
Input: 121
Output: true
```
Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```
Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Follow up**:
Coud you solve it without converting the integer to a string?
---
### My answer:
```
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        x_str = str(x)
        x_rev = ''.join(x_str[::-1])
        return(True if x_str == x_rev else False)
```
40 ms, faster than 92.48%,  11.8 MB, less than 34.94% 

---
### Solution:
- First Idea: convert the number into string, and check if the string is a palindrome, 
**but** this would require _**extra non-constant space**_ for creating the string which is not allowed by the problem description.
- Second idea: revert the number itself, and then compare the number with original number, if they are the same, 
then the number is a palindrome. However, if the reversed number is larger than [int.MAX], we will hit integer overflow problem.
- what if we only revert half of the int number? After all, the reverse of the last half of the palindrome should be the same as the first half of the number, if the number is a palindrome.
- Algorithm:
  - All negative numbers are not palindrome
  - how to revert the last half of the number
```
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if (x < 0) or (x % 10 == 0 and x != 0):
            return(False)
        
        reverted = 0
        while x > reverted:
            reverted = reverted * 10 + x % 10
            x = x // 10
        
        return((x == reverted) or (x == reverted//10))
  

48 ms, faster than 77.45%;  11.7 MB, less than 77.11% 
