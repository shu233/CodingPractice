Given an array of integers, return _**indices**_ of the two numbers such that they add up to a specific target.

You may assume that each input would have _**exactly**_ one solution, and you may _**not use the same element twice**_.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

---
### My Answer:
```Python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        res = []
        for n in nums:
            index_n = nums.index(n)
            for m in nums[index_n + 1:]:
                if (m + n) == target:
                    index_m = nums.index(m,index_n+1)
                    res.append(index_n)
                    res.append(index_m)
                    return(res)
```
_Special Cases:[3,2,4] 6 or [3,3] 6_

**Attention: list.index(e[,start_index, end]) returns the FIRST index of the required element!**

Accepted: 2868 ms, 12.6 MB

#### Complexity Analysis
- Time complexity : O(n^2)  For each element, we try to find its complement by looping through the rest of array which takes O(n) time. Therefore, the time complexity is O(n^2)
- Space complexity : O(1).

#### Hints:
- A really brute force way would be to search for all possible pairs of numbers but that would be too slow. Again, it's best to try out brute force solutions for just for completeness. It is from these brute force solutions that you can come up with optimizations.
- Can we change our array somehow so that this search becomes faster?
- The second train of thought is, without changing the array, can we use additional space somehow? Like maybe a hash map to speed up the search?

---
### Solution
### 1. Two-pass Hash Table
What is the best way to maintain a mapping of each element in the array to its index? A hash table.

_Look up in hash table should be amortized O(1)O(1) time as long as the hash function was chosen carefully._

A simple implementation uses two iterations. In the first iteration, we add each element's value and its index to the table. 
Then, in the second iteration we check if each element's complement (target - nums[i]) exists in the table. 
**Beware that the complement must not be nums[i] itself!**

```Java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```
#### Complexity Analysis:
- Time complexity : O(n). We traverse the list containing n elements exactly twice. 
Since the hash table reduces the look up time to O(1), the time complexity is O(n).
- Space complexity : O(n). The extra space required depends on the number of items stored in the hash table, which stores exactly n elements.

### 2. One-pass Hash Table
It turns out we can do it in one-pass. While we iterate and inserting elements into the table, we also look back to check if current element's complement already exists in the table. If it exists, we have found a solution and return immediately.
```Java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```
#### Complexity Analysis:
- Time complexity : O(n). We traverse the list containing n elements only once. Each look up in the table costs only O(1) time.
- Space complexity : O(n). The extra space required depends on the number of items stored in the hash table, which stores at most n elements.

---
### Other Solution in Python3
```Python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        h = {}
        for i, num in enumerate(nums):
            n = target - num
            if n not in h:
                h[num] = i
            else:
                return [h[n], i]
```
40ms, 13.2 MB
