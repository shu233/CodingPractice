Given a non-negative index _k_ where _k ≤ 33_, return the _k-th_ index row of the Pascal's triangle.

Note that the row index starts from 0.

Example:
```
Input: 3
Output: [1,3,3,1]
```
**Follow up**: Could you optimize your algorithm to use only _O(k)_ extra space?

---
### My Answer
```Python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        triangle = []

        for row_num in range(rowIndex+1):
            # The first and last row elements are always 1.
            row = [None for _ in range(row_num+1)]
            row[0], row[-1] = 1, 1

            # Each triangle element is equal to the sum of the elements
            # above-and-to-the-left and above-and-to-the-right.
            for j in range(1, len(row)-1):
                row[j] = triangle[row_num-1][j-1] + triangle[row_num-1][j]

            triangle.append(row)

        return triangle[rowIndex]
```   
Success: 20 ms, faster than 51.39% ; 11.9 MB, less than 7.69% -> _O(k^2)_

**Improvement**

only store the previous row
```Python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        triangle = [1]

        for row_num in range(rowIndex+1):
            # The first and last row elements are always 1.
            row = [None for _ in range(row_num+1)]
            row[0], row[-1] = 1, 1

            for j in range(1, len(row)-1):
                row[j] = triangle[j-1] + triangle[j]

            triangle = row

        return triangle
```
16 ms, faster than 80.86% ; 11.7 MB, less than 50.00% -> _O(2k)_



