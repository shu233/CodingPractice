Say you have an array for which the _i-th_ element is the price of a given stock on day _i_.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note**: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:
```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```
Example 2:
```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```             
Example 3:
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.  
```

---
### My Answer
???

---
### Solution
#### Approach 1: Brute Force
In this case, we simply calculate the profit corresponding to all the possible sets of transactions and find out the maximum profit out of them.
```Java
class Solution {
    public int maxProfit(int[] prices) {
        return calculate(prices, 0);
    }

    public int calculate(int prices[], int s) {
        if (s >= prices.length)
            return 0;
        int max = 0;
        for (int start = s; start < prices.length; start++) {
            int maxprofit = 0;
            for (int i = start + 1; i < prices.length; i++) {
                if (prices[start] < prices[i]) {
                    int profit = calculate(prices, i + 1) + prices[i] - prices[start];
                    if (profit > maxprofit)
                        maxprofit = profit;
                }
            }
            if (maxprofit > max)
                max = maxprofit;
        }
        return max;
    }
}
```
Recursive function is called _n^n_ times!

#### Approach 2: Peak Valley Approach
If we analyze the graph, we notice that the points of interest are the consecutive valleys and peaks.

Mathematically speaking: <a href="https://www.codecogs.com/eqnedit.php?latex=TotalProfit&space;=&space;\sum_i(height(peak_i)-height(valley_i))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?TotalProfit&space;=&space;\sum_i(height(peak_i)-height(valley_i))" title="TotalProfit = \sum_i(height(peak_i)-height(valley_i))" /></a>

```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices: return 0
        
        ind = 0
        valley = peak = prices[0]     
        max_profit = 0
        
        while ind < len(prices)-1:
            # Find the downhill and thus the valley
            while ind < len(prices)-1 and prices[ind] >= prices[ind+1]:
                ind += 1
            valley = prices[ind]
            
            # Find the uphill and then the peak    
            while ind < len(prices)-1 and prices[ind] <= prices[ind+1]:
                ind += 1
            peak = prices[ind]
            
            max_profit += peak - valley
            
        return max_profit
```
40 ms, faster than 96.43% ; 12.6 MB, less than 60.46%

#### Approach 3: Simple One Pass
This solution follows the logic used in Approach 2 itself, but with only a slight variation. 
In this case, instead of looking for every peak following a valley, we can simply go on crawling over the slope and keep on adding the profit obtained from every consecutive transaction. 
In the end,we will be using the peaks and valleys effectively, but we need not track the costs corresponding to the peaks and valleys along with the maximum profit, 
but we can directly keep on adding the difference between the consecutive numbers of the array 
if the second number is larger than the first one, and at the total sum we obtain will be the maximum profit. 
This approach will simplify the solution. 
```Python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices: return 0
    
        max_profit = 0
        for i in range(1,len(prices)):
            if prices[i] > prices[i - 1]:
                max_profit += prices[i] - prices[i - 1]
                 
        return max_profit
```        
44 ms, faster than 86.05%  ;  12.7 MB, less than 32.56%        
        

