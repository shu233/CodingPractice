Count the number of prime numbers less than a non-negative number, _**n**_.

Example:
```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

---
### My Solution
Notice: Not exceed time limit!

Hints:
- Start with a _isPrime_ function, but time complexity is _O(n^2)_
- As we know the number must not be divisible by any number > n / 2, we can immediately cut the total iterations half by dividing only up to n / 2. Could we still do better?
- we only need to consider factors up to **√n** because, if n is divisible by some number p, then n = p × q and since p ≤ q, we could derive that p ≤ √n.
```python
class Solution(object):
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        import math
        
        def isPrime(m):
            if m<=1: return False
            
            u = int(math.sqrt(m))
            for i in range(2,u+1):
                if m % i == 0:
                    return False
            return True
        
        c = 0
        for m in range(2,n):
            if isPrime(m):
                c += 1
                
        return c
```        
***Time Limit Exceeded*** !!!
        
Hints:
- The [Sieve of Eratosthenes](https://www.codesdope.com/blog/article/prime-numbers-using-sieve-algorithm-in-python/) is one of the most efficient ways to find all prime numbers up to n: 
    -  Let's look at the first number, 2. We know all multiples of 2 must not be primes, so we mark them off as non-primes.
    - Then we look at the next number, 3. Similarly, all multiples of 3 such as 3 × 2 = 6, 3 × 3 = 9, ... must not be primes, so we mark them off as well. 
    - Now we look at the next number, 4, which was already marked off!
```python
class Solution(object):
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        import math
        
        primer = []
        for i in range(2,n):
            primer.append(i)
        
        i = 2
        while i <= int(math.sqrt(n)):
            if i in primer:
                for j in range(i*2, n, i):
                    if j in primer:
                        primer.remove(j)
            i += 1
                
        return len(primer)
```
**Time Limit Exceeded** !!!

Hints:
- 4 is not a prime because it is divisible by 2, which means all multiples of 4 must also be divisible by 2 and were already marked off. So we can skip 4 immediately and go to the next number, 5. Now, all multiples of 5 such as 5 × 2 = 10, 5 × 3 = 15, 5 × 4 = 20, 5 × 5 = 25, ... can be marked off. There is a slight optimization here, we do not need to start from 5 × 2 = 10. Where should we start marking off?
- In fact, we can mark off multiples of 5 starting at 5 × 5 = 25, because 5 × 2 = 10 was already marked off by multiple of 2, similarly 5 × 3 = 15 was already marked off by multiple of 3. Therefore, if the current number is p, we can always mark off multiples of p starting at p2, then in increments of p: p2 + p, p2 + 2p, ... Now what should be the terminating loop condition?
- It is easy to say that the terminating loop condition is p < n, which is certainly correct but not efficient. Do you still remember Hint #3?
- Yes, the terminating loop condition can be p < √n, as all non-primes ≥ √n must have already been marked off. When the loop terminates, all the numbers in the table that are non-marked are prime.
```python
class Solution(object):
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        import math
        
        primer = []
        for i in range(2,n):
            primer.append(i)
        
        i = 2
        while i <= int(math.sqrt(n)):
            if i in primer:
                for j in range(i*i, n, i):
                    if j in primer:
                        primer.remove(j)
            i += 1
                
        return len(primer)
```
Still **Time Limit Exceeded** ?!?!?!?!?!?!??!!?

---
### Other Solution
```python
def countPrimes(self, n: int) -> int:
        if n < 3: return 0     ###// No prime number less than 2
        lst = [1] * n          ###// create a list for marking numbers less than n
        lst[0] = lst[1] = 0    ###// 0 and 1 are not prime numbers
        m = 2
        while m * m < n:       ###// we only check a number (m) if its square is less than n
            if lst[m] == 1:    ###// if m is already marked by 0, no need to check its multiples.
			
			    ###// If m is marked by 1, we mark all its multiples from m * m to n by 0. 
			    ###// 1 + (n - m * m - 1) // m is equal to the number of multiples of m from m * m to n
                lst[m * m: n: m] = [0] *(1 + (n - m * m - 1) // m)
				
			###// If it is the first iteration (e.g. m = 2), add 1 to m (e.g. m = m + 1; 
			### // which means m will be 3 in the next iteration), 
            ###// otherwise: (m = m + 2); This way we avoid checking even numbers again.	
            m += 1 if m == 2 else 2
        return sum(lst)
```        
128 ms, faster than 98.39%  ;  35.1 MB, less than 44.44%        
        











