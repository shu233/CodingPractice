Given two sorted integer arrays _nums1_ and _nums2,_ merge _nums2_ into _nums1_ as one **sorted** array.

**modify nums1 in-place**

**Note**:

- The number of elements initialized in _nums1_ and _nums2_ are _m_ and _n_ respectively.
- You may assume that _nums1_ has enough space (size that is greater or equal to _m + n_) to hold additional elements from _nums2_.

Example:
```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```
Hint:
- You can easily solve this problem if you simply think about two elements at a time rather than two arrays. We know that each of the individual arrays is sorted. What we don't know is how they will intertwine. Can we take a local decision and arrive at an optimal solution?
- If you simply consider one element each at a time from the two arrays and make a decision and proceed accordingly, you will arrive at the optimal solution.

---
### My Answer
```Python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        ind = i = 0

        for j in range(n):
            n2 = nums2[j]
            while i < m:
                n1 = nums1[ind]
                if n2 < n1:
                    nums1[ind+1 : ind+m-i+1] = nums1[ind : ind+m-i]
                    nums1[ind] = n2
                    ind += 1
                    break
                else:
                    i += 1
                    ind += 1

            if i >= m:
                nums1[ind : ind+n-j] = nums2[j:n]
                break
```
Success: 24 ms, faster than 65.10% ; 11.9 MB, less than 5.13%

---
### Other Solution
```Python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        index = len(nums1)-1
        m -= 1
        n -= 1
        
        while n >= 0:
            if(m<0 or nums1[m]<nums2[n]):
                nums1[index] = nums2[n]
                n-=1
            else:
                nums1[index] = nums1[m]
                m-=1
            index-=1
```            
24 ms, faster than 65.10%  ; 11.8 MB, less than 46.15%            

**Idea**: 后部为空，所以从后部开始，添加最大值
