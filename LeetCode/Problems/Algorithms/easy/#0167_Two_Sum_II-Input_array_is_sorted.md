Given an array of integers that is already _**sorted in ascending order**_, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

Note:

- Your returned answers (both index1 and index2) are not zero-based.
- You may assume that each input would have _exactly_ one solution and you may not use the _same_ element twice.

Example:
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```
Topic: **Array**, **Two Pointers**, **Binary Search**

---
### My Answer
```Python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """  
        for i in range(len(numbers)):
            c = target - numbers[i]
            for j in range(i+1,len(numbers)):
                if numbers[j] == c: return [i+1,j+1]
```
**Time Limit Exceeded**

---
### Solution
```Python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """  
        dic = {} 
        for i, v in enumerate(numbers):
            if (target - v) in dic: break #find the pair present in dic.
            else: dic[v] = i+1 #Making a collection of 1st pair. 
        return sorted([dic[target - v],i+1])
```
48 ms, faster than 74.72% ; 12.1 MB, less than 27.27% 
