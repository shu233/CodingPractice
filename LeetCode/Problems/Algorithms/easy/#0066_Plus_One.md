Given a **non-empty** array of digits representing a *non-negative* integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

Example 1:
```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```
Example 2:
```
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

---
### My Answer
```
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        n = int(''.join(map(str,digits))) + 1
        digits = list(str(n))
        return list(map(int,digits))
```
Success: 24 ms, faster than 28.78%; 11.8 MB, less than 10.42%

Another solution:
```
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        for i in range(len(digits))[::-1]:
            if digits[i] < 9:
                    digits[i] += 1
                    break
            elif digits[i] == 9 and i == 0:
                    digits[i] = 0
                    digits.insert(0,1)
            else:
                    digits[i] = 0

        return(digits)
```
Success: 20 ms, faster than 62.71% ; 11.7 MB, less than 62.50%      
        
