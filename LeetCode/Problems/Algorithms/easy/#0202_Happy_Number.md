Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: 
- Starting with any positive integer, 
- replace the number by the sum of the squares of its digits, 
- and repeat the process until the number equals 1 (where it will stay), or it **loops endlessly** in a cycle which does not include 1. 
- Those numbers for which this process ends in 1 are happy numbers.

Example: 
```
Input: 19
Output: true
Explanation: 
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

---
### My Answer
- Handling the **endless loops**: try to find if the new number seire is a LOOP!
> Example: 4
16
37
58
89
145
42
20
4
16
37
58
89 ...
- As long as the new calculated number has already existed before
```Python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        number_list = [n]
        while n != 1:
            l = list(map(int,str(n)))
            n = sum([x**2 for x in l])
            if n in number_list:
                return False
            else:
                number_list.append(n)    

        return True
```
Success: 24 ms, faster than 49.13% ; 11.9 MB, less than 10.00%

---
### Other Solution
Donnot have to generate the list for digits! -> String is also iterable!!!
```Python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        dic = {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}
        number_list = [n]
        while n != 1:
            n = sum([dic[x]**2 for x in str(n)])
            if n in number_list:
                return False
            else:
                number_list.append(n)    

        return True
```
12 ms, faster than 97.96%; 11.9 MB, less than 10.00% 

