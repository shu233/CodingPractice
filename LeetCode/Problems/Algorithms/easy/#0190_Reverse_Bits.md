Reverse bits of a given 32 bits unsigned integer.

Example 1:
```
Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.
```
Example 2:
```
Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
```
Note:
- Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using `2's complement notation`. Therefore, in Example 2 above the input represents the signed integer `-3` and the output represents the signed integer `-1073741825`.

Follow up:

If this function is called many times, how would you optimize it?

---
### My Answer
> python 存储数据是 number，下包含四种数字类型，其中int（有符号整型）。[Data types in Python](https://www.cnblogs.com/snaildev/p/7544558.html)

```Python
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):
        b = bin(n)
        
        # Starting with '0b'
        if len(b) < 34:
            b = '0b' + '0'*(34-len(b)) + b[2:]
            
        reverse_b = '0b' + b[2:][::-1]
        return int(reverse_b,2)
```
Success: 16 ms, faster than 83.98% ; 11.9 MB, less than 7.14%
