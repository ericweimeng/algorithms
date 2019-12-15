# Knapsack

## Knapsack

### Type I, 0/1 Without Values \(0/1 可行性型\)

Given _n_ items with size Ai, an integer _m_ denotes the size of a backpack. How full you can fill this backpack

There are 2 ways to think about this problems, one is use dp\[i\]\[j\] denote if it's possible to get weights j using items up to the i-th. Another way is to use dp\[i\]\[j\] denote maximum weight using items up to i-th to fit in a j size knapsack

**Thought I**

dp\[i\]\[j\] denotes if it's possible to get weights j using items up to the i-th item. 

**Recursive equation**

$$
dp[i][w] = dp[i - 1][w] OR dp[i - 1][w - A_{i}] + A_{i})
$$

**Initialization**

```text
dp[0][0] = True  # use 0 items to get weight 0, possible
dp[0][1...m] = False  # use 0 items to get weight 1...m, impossible
```

**Corner cases**

```text
dp[i-1][w-Ai-1] has to make sure w >= Ai-1
```

**Calculation**

```text
Initialize dp[0][0], dp[0][1], ... dp[0][m]
Calculate if using item 1 can get dp[1][0], dp[1][1], ..., dp[1][m]
Calculate if using item up to 2 can get dp[2][0], dp[2][1], ..., dp[2][m]
Calculate if using item up to n can get dp[n][0], dp[n][1], ..., dp[n][m]
Time O(NM)
space: O(m)
```

#### Very first version

```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        # write your code here
        
        n = len(A)
        if not n:
            return 0
        
        dp = [[False for _ in range(m + 1)] for _ in range(n + 1)]
        dp[0][0] = True
        
        for i in range(1, n + 1):
            for j in range(m + 1):
                dp[i][j] = dp[i - 1][j] # if i - 1 can, then can i-th
                if j >= A[i - 1]: # if A[i - 1] > j, then no need to keep going
                    dp[i][j] |= dp[i - 1][j - A[i - 1]]
                    
        for i in range(m, -1, -1):
            if dp[n][i]:
                return i
                    
                
        return 0
```

#### Second version with space optimization \(rolling array\)

```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        n = len(A)
        f = [[False] * (m + 1), [False] * (m + 1)]
        
        f[0][0] = True
        for i in range(1, n + 1):
            f[i % 2][0] = True
            for j in range(1, m + 1):
                if j >= A[i - 1]:
                    f[i % 2][j] = f[(i - 1) % 2][j] or f[(i - 1) % 2][j - A[i - 1]]
                else:
                    f[i % 2][j] = f[(i - 1) % 2][j]
                    
        for i in range(m, -1, -1):
            if f[n % 2][i]:
                return i
        return 0
```

**Thought II**

The dp\[i\]\[j\] denotes the the maximum weight using items up to i to fit in a j size knapsack, therefore for each dp\[i\]\[j\], the recursive equation can be easily represented as 

$$
dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - A_{i}] + A_{i})
$$

#### 

#### One dimensional array

```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        # write your code here
        
        n = len(A)
        if not n:
            return 0
        
        dp = [0 for _ in range(m + 1)]
        
        for i in range(n):
            for j in range(m, A[i] - 1, -1):
                dp[j] = max(dp[j - A[i]] + A[i], dp[j])
                
        return dp[m]
```

The reason for reversed order is we can only use every item once and each dp\[i\] relies on dp\[i - A\[j\]\] that comes before it.

#### Bonus solution

效率最高的算法，没有之一。算法为区间合并。

比如，输入的整数是 \[1,2,5\]。当一个物品都不选的时候，可以组成的最大和为 0，也就是 \[0,0\] 这段区间可以被组成。

当有 1 以后，把 \[0,0\] 的左右两边都+1，得到 \[1,1\]，然后合并 \[0,0\] 和 \[1,1\] 得到 \[0,1\]  
加入2以后，意味着，原本可以从前面的数里组成 \[0,1\] 区间中的任何和，现在可以组成 \[0,1\]里面的任意和加上 \[0+2,1+2\] 里的任意和。  
也就是 \[0,1\] + \[2,3\]，合并之后等于 \[0,3\]

最后加入5。 \[0,3\] + \[5,8\] =&gt; \[\[0,3\],\[5,8\]\]

这样就得到了这些物品能够组成的和有哪些（以区间的形式存储）。然后看看 &lt;= m 里最大被覆盖到的数是谁即可。

```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        A.sort()
        
        intervals = [[0, 0]]
        for item in A:
            new_intervals = []
            for interval in intervals:
                new_intervals.append([interval[0] + item, interval[1] + item])
                
            intervals = self.merge_intervals(intervals, new_intervals)

        max_size = 0
        for interval in intervals:
            if interval[0] <= m <= interval[1]:
                return m
            if interval[0] > m:
                break
            max_size = max(max_size, interval[1])
        return max_size
            
    def merge_intervals(self, list1, list2):
        i, j = 0, 0
        intervals = []
        while i < len(list1) and j < len(list2):
            if list1[i] < list2[j]:
                self.push_to_intervals(intervals, list1[i])
                i += 1
            else:
                self.push_to_intervals(intervals, list2[j])
                j += 1
                
        while i < len(list1):
            self.push_to_intervals(intervals, list1[i])
            i += 1
        
        while j < len(list2):
            self.push_to_intervals(intervals, list2[j])
            j += 1
            
        return intervals
        
    def push_to_intervals(self, intervals, interval):
        if not intervals or intervals[-1][1] + 1 < interval[0]:
            intervals.append(interval)
            return
        
        intervals[-1][1] = max(intervals[-1][1], interval[1])
```

### Type II 0/1 With values \(0/1 最值型\)

Given _n_ items with size Ai and value Vi, and a backpack with size _m_. What's the maximum value can you put into the backpack?

```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @param V: Given n items with value V[i]
    @return: The maximum value
    """
    def backPackII(self, m, A, V):
        # write your code here
        
        dp = [0 for _ in range(m + 1)]
        n = len(A)
        
        for i in range(n):
            for j in range(m, A[i] - 1, -1):
                if j >= A[i]:
                    dp[j] = max(dp[j], dp[j - A[i]] + V[i])
                    
        return dp[m]
```

### Type III Complete Knapsack \(完全最值型\)

Given n types of items with size Ai and value Vi\( each item has an infinite number available\) and a backpack with size m. What's the maximum value can you put into the backpack? 

The transitional equation can be represented as

dp\[i\]\[w\] = max\(dp\[i-1\]\[w\], dp\[i-1\]\[w-A\[i\]\] + Vi\)

Proof:

A\[i-1\] = 2, v

dp\[i\]\[5\] = max{dp\[i-1\]\[5\], dp\[i-1\]\[3\] + v, dp\[i-1\]\[1\] + 2v}

dp\[i\]\[7\] = max{dp\[i-1\]\[7\], dp\[i - 1\]\[5\] + v, dp\[i-1\]\[3\] + 2v, dp\[i-1\]\[1\] + 3v} 

= max{dp\[i-1\]\[5\], dp\[i-1\]\[3\] + v, dp\[i-1\]\[1\] + 2v} + v 

= dp\[i\]\[5\] + v

=dp\[i\]\[7-5\] + v

if we do it in one dimensional is

dp\[7\] = max\(dp\[7\], dp\[7-5\] + v\)

```python
class Solution:
    """
    @param A: an integer array
    @param V: an integer array
    @param m: An integer
    @return: an array
    """
    def backPackIII(self, A, V, m):
        # write your code here
        n = len(A)
        dp = [0 for _ in range(m+1)]
        for i in range(n):
            for j in range(A[i], m+1):
                dp[j] = max(dp[j-A[i]] + V[i], dp[j])
        return dp[-1]
```

### Type V 0/1 Counting Knapsack \(计数型背包，前i项有多少种方法拼出W\)

Given a `nums` integer array with size n and all elements are positive numbers. An integer `target` denotes the size of a knapsack. Find the number of possible ways to fill the backpack. Each item of nums can only be used once.

#### One dimensional array

```python
class Solution:
    """
    @param nums: an integer array and all positive numbers
    @param target: An integer
    @return: An integer
    """
    def backPackV(self, nums, target):
        # write your code here
        
        dp = [0 for _ in range(target + 1)]
        dp[0] = 1
        n = len(nums)
        
        for i in range(n):
            # Calculate reversely since each new dp[j] depends on 
            # an old dp[j - nums[i]] that comes before it, if calculation starts from
            # the front, then old values will be updated and get lost
            for j in range(target, nums[i] - 1, -1):
                dp[j] += dp[j - nums[i]]
                
        return dp[target]
```

### Type VI 0/1 Counting Knapsack \(计数型背包， 有多少种方法拼出W\)

Given n items with size nums\[i\] which an integer array and all positive numbers, no duplicates. An integer target denotes the size of a backpack. Find the number of possible ways to fill the knapsack.

The keys to this problem is that 

* Since we don't know what item is going to be the last item added to target, therefore the last step is to no longer see if use last item or not, instead, it's now who is going to be the last item. The dp\[i\] now denotes how many ways to add to target i.
* For items in those combinations that satisfies the restrictions, they added up to target

dp\[i\] denotes how many ways can get target i

dp\[i\] = dp\[i - A0\] + dp\[i - A1\] + ... + dp\[i - An-1\], dp\[0\] = 1

Therefore the calculation is to calculate dp\[1\], dp\[2\] ... dp\[target\]

```python
class Solution:
    """
    @param nums: an integer array and all positive numbers, no duplicates
    @param target: An integer
    @return: An integer
    """
    def backPackVI(self, nums, target):
        # write your code here
        dp = [0 for _ in range(target + 1)]
        dp[0] = 1
        n = len(nums)
        
        for i in range(1, target + 1):
            for j in range(n):
                if i >= nums[j]:
                    dp[i] += dp[i - nums[j]]
                
                
        return dp[target]
```

#### Notes

The key point to solve knapsack is to see the last step, if order does not matter then what is the last item and if order does matter, then to see whether the last item should be put in knapsack or not.

#### Reference

[https://blog.csdn.net/u013166817/article/details/85449218](https://blog.csdn.net/u013166817/article/details/85449218)

