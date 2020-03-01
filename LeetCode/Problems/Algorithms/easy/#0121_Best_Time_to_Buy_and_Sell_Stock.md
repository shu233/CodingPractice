Say you have an array for which the _i-th_ element is the price of a given stock on day _i_.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:
```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```             

Example 2:
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

---
### My Answer - Brute Force
```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_p = 0

        for i in range(len(prices)):
            for j in range(i,len(prices)):
                profit = prices[j] - prices[i]
                max_p = profit if profit > max_p else max_p
                
        return max_p
```  
**Time Limit Exceeded**!!

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_p = 0

        for i in range(len(prices)):
            profit = max(prices[i:]) - prices[i]
            max_p = profit if profit > max_p else max_p
                
        return max_p
```        
Success: 6528 ms, faster than 5.31%  ; 13 MB, less than 5.50%



---
### Other Solution - One Pass
Given array on a graph (line chart):

The points of interest are the peaks and valleys in the given graph. We need to find the largest peak following the smallest valley. 
We can maintain two variables - minprice and maxprofit corresponding to the smallest valley and maximum profit 
(maximum difference between selling price and minprice) obtained so far respectively.

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        min_price = float('inf')
        max_profit = 0

        for i in range(len(prices)):
            if prices[i] < min_price:
                min_price = prices[i]
            elif prices[i] - min_price > max_profit:
                max_profit = prices[i] - min_price
                
        return max_profit
```        
52 ms, faster than 48.69% ; 12.8 MB, less than 6.42%

