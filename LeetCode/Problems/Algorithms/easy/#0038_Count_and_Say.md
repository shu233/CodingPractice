The count-and-say sequence is the sequence of integers with the first five terms as following:
```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```
- `1` is read off as `"one 1"` or `11`.
- `11` is read off as `"two 1s"` or `21`.
- `21` is read off as `"one 2`, then `one 1"` or `1211`.

Given an integer n where 1 ≤ n ≤ 30, generate the n-th term of the count-and-say sequence. 
You can do so recursively, in other words from the previous member read off the digits, 
counting the number of digits in groups of the same digit.

Note: Each term of the sequence of integers will be represented as a **string**.

Example 1:
```
Input: 1
Output: "1"
Explanation: This is the base case.
```
Example 2:
```
Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".

Hint: To generate the n-th term, just count and say the (n-1)-th term.

---
### My Answer
Idea: 将字符串按相同字符分割
```
class Solution(object):
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        s = '1'
        
        for x in range(n-1):
            l = []
            digit = s[0]
            k = 0
            for i,d in enumerate(s):
                if d != digit:
                    digit = d
                    l.append(s[k:i])
                    k = i

                if i == len(s)-1:
                    l.append(s[k:i+1])

            s = ''
            for i in l:
                s += str(len(i)) + str(i[0])
                
        return s
```
Success: 24 ms, faster than 52.68%; 11.8 MB, less than 81.48%

---
### Other Solution
Recursion
```
    # Base case
    if n == 1:
        return '1'
    
    # count and say resursion
    cur_num, rval = 1, ""
    
    prev = self.countAndSay(n-1)
    
    for idx in range(len(prev)):
        if idx > 0 and prev[idx-1] == prev[idx]:
            cur_num += 1
            rval = rval[:-2] + str(cur_num) + rval[-1]
        else:
            cur_num = 1
            rval += str(cur_num) + prev[idx]
    
    return rval
```
20 ms, faster than 78.58% ; 11.9 MB, less than 18.52%
