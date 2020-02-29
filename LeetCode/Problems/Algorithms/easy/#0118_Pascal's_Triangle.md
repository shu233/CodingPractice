Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

---
### My Answer
```Python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        res = []
        for i in range(numRows):
            if i==0:
                res.append([1])
                continue
            elif i==1:
                res.append([1,1])
                continue
            else:
                line = [1 for x in range(i+1)]
                for j in range(1,i):
                    line[j] = res[i-1][j-1] + res[i-1][j]
                res.append(line)
        return res
```        
Success: 20 ms, faster than 47.75% ; 11.8 MB, less than 30.00%


---
### Solution - Dynamic Programming
Although the algorithm is very simple, the iterative approach to constructing Pascal's triangle can be classified as dynamic programming 
because we construct each row based on the previous row.

First, we generate the overall `triangle` list, which will store each row as a sublist. 
Then, we check for the special case of 0, as we would otherwise return [1]. 
If _numRows > 0_, then we initialize `triangle` with [1] as its first row, and proceed to fill the rows as follows:
```Python
class Solution:
    def generate(self, num_rows):
        triangle = []

        for row_num in range(num_rows):
            # The first and last row elements are always 1.
            row = [None for _ in range(row_num+1)]
            row[0], row[-1] = 1, 1

            # Each triangle element is equal to the sum of the elements
            # above-and-to-the-left and above-and-to-the-right.
            for j in range(1, len(row)-1):
                row[j] = triangle[row_num-1][j-1] + triangle[row_num-1][j]

            triangle.append(row)

        return triangle
        

