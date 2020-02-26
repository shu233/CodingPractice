## Idea
Solving the problem with the results of **subproblems** (already solved!)

## Two Ways
Example: Fibonacci Sequence
```
Fibonacci (n) = 1;   n = 0
Fibonacci (n) = 1;   n = 1
Fibonacci (n) = Fibonacci(n-1) + Fibonacci(n-2)
```
It can be easily solved by Recursion:
```Python
def fib(n):
  if n <= 0: return 0
  if n == 1: return 1
  
  return fib(n-1)+fib(n-2)
```

Note: 递归树中的每一个子节点都会执行一次，很多重复的节点被执行，fib(2)被重复执行了5次。由于调用每一个函数的时候都要保留上下文，所以空间上开销也不小。
这么多的子节点被重复执行，如果在执行的时候把执行过的子节点保存起来，后面要用到的时候直接查表调用的话可以节约大量的时间。
下面就看看动态规划的两种方法怎样来解决斐波拉契数列Fibonacci 数列问题。

### 1. Top-Down Memo Method
```Python
def fibonacci(n):
    if n <= 0: return 0

    memo = [-1 for i in range(n+1)] # Length n+1
    return fib(n,memo)

def fib(n,memo):
    if memo[n] != -1: return memo[n]

    if n <= 2: memo[n] = 1
    else: memo[n] = fib(n-1,memo) + fib(n-2,memo)
    return memo[n]
```    
创建了一个n+1大小的数组来保存求出的斐波拉契数列中的每一个值，在递归的时候如果发现前面fib（n）的值计算出来了就不再计算，如果未计算出来，则计算出来后保存在Memo数组中，下次在调用fib（n）的时候就不会重新递归了。

### 2. Bottom-Up
备忘录法还是利用了递归，上面算法不管怎样，计算fib（6）的时候最后还是要计算出fib（1），fib（2），fib（3）……,那么何不先计算出fib（1），fib（2），fib（3）……,呢？
这也就是动态规划的核心，**先计算子问题，再由子问题计算父问题**。
```Python
def fibonacci(n):
    if n <= 0: return 0

    memo = [0 for i in range(n+1)]
    memo[0] = 0
    memo[1] = 1
    for i in range(2,n+1):
        memo[i] = memo[i-1] + memo[i-2]
    
    return memo[n]
```    
 参与循环的只有 i，i-1 , i-2三项，因此该方法的空间可以进一步的压缩如下:
 ```Python
 def fibonacci(n):
    if n <= 1: return n

    memo_i_2 = 0
    memo_i_1 = 1
    memo_i = 1
    for i in range(2,n+1):
        memo_i = memo_i_1 + memo_i_2
        memo_i_2 = memo_i_1
        memo_i_1 = memo_i
    
    return memo_i
```

## Theory
### When to use DP:
- **Overlapping Subproblems**:
在斐波拉契数列和钢条切割结构图中，可以看到大量的重叠子问题，比如说在求fib（6）的时候，fib（2）被调用了5次，在求cut（4）的时候cut（0）被调用了4次。如果使用递归算法的时候会反复的求解相同的子问题，不停的调用函数，而不是生成新的子问题。如果递归算法反复求解相同的子问题，就称为具有重叠子问题（overlapping subproblems）性质。在动态规划算法中使用数组来保存子问题的解，这样子问题多次求解的时候可以直接查表不用调用函数递归。
- **Optimal Substructure**:
用动态规划求解最优化问题的第一步就是刻画最优解的结构，如果一个问题的解结构包含其**子问题的最优解**，就称此问题具有最优子结构性质。
因此，某个问题是否适合应用动态规划算法，它是否具有最优子结构性质是一个很好的线索。使用动态规划算法时，用子问题的最优解来构造原问题的最优解。因此必须考查最优解中用到的所有子问题。

### Another Example: 钢条切割问题
Given: 长度为n的钢条，价格表
| 长度 i       | 1   |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  |  10  |
| --------   | -----:  | :----:  | :----:  | :----:  | :----:  | :----:  | :----:  | :----:  | :----:  | :----:  |
| 价格 p_i     | 1   |   5 |  8  |  9  |  10  |  17  |  17  |  20  |  24  |  30  |

Problem: 求最优的切割方案，使得收益r_n最大

Solution: 
- Idea: `r_n =max(p_n,  r_1 + r_n-1,  r_2 + r_n-2,  ...,  r_n-1 + r_1)`
- So the objective:   <a href="https://www.codecogs.com/eqnedit.php?latex=\max&space;\limits_{1\leqslant&space;i\leqslant&space;n}\{p_i&space;&plus;&space;r_{n-i}\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\max&space;\limits_{1\leqslant&space;i\leqslant&space;n}\{p_i&space;&plus;&space;r_{n-i}\}" title="\max \limits_{1\leqslant i\leqslant n}\{p_i + r_{n-i}\}" /></a>
- Solutions:
  - Approach 1: Recursion
  ```Java
  public static int cut(int []p,int n)
    {
        if(n==0)
            return 0;
        int q=Integer.MIN_VALUE;
        for(int i=1;i<=n;i++)
        {
            q=Math.max(q, p[i-1]+cut(p, n-i));  
        }
        return q;
    }
  
  - Approach 2: Top-Down Memo
  ```Java
  public static int cutMemo(int []p)
    {
        int []r=new int[p.length+1];
        for(int i=0;i<=p.length;i++)
            r[i]=-1;                        
        return cut(p, p.length, r);
    }
    public static int cut(int []p,int n,int []r)
    {
        int q=-1;
        if(r[n]>=0)
            return r[n];
        if(n==0)
            q=0;
        else {
            for(int i=1;i<=n;i++)
                q=Math.max(q, cut(p, n-i,r)+p[i-1]);
        }
        r[n]=q;

        return q;
    }
  ```
  
 - Approach 3: **Bottom-Up DP**
 ```Java
 public static int buttom_up_cut(int []p)
    {
        int []r=new int[p.length+1];
        for(int i=1;i<=p.length;i++)
        {
            int q=-1;
            //①
            for(int j=1;j<=i;j++)
                q=Math.max(q, p[j-1]+r[i-j]);
            r[i]=q;
        }
        return r[p.length];
    }
 ```
注释①处的循环，这里外面的循环是求r[1],r[2]……，里面的循环是求出r[1],r[2]……的最优解，也就是说r[i]中保存的是钢条长度为i时划分的最优解

### Typical Models in DP
#### 1. Linear Model
线性模型的是动态规划中最常用的模型，上文讲到的钢条切割问题就是经典的线性模型，这里的线性指的是状态的排布是呈线性的。【例题1】是一个经典的面试题，我们将它作为线性模型的敲门砖。
```
【例题1】在一个夜黑风高的晚上，有n（n <= 50）个小朋友在桥的这边，现在他们需要过桥，但是由于桥很窄，每次只允许不大于两人通过，他们只有一个手电筒，所以每次过桥的两个人需要把手电筒带回来，i号小朋友过桥的时间为T[i]，两个人过桥的总时间为二者中时间长者。问所有小朋友过桥的总时间最短是多少。
```

#### 2. 区间模型

#### 3. 背包模型

---
讲解：[算法](https://blog.csdn.net/u013309870/article/details/75193592)
