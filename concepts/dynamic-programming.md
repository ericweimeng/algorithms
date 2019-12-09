# Dynamic Programming

## Knapsack

### Type I, 0/1 Without Values

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

### Type II 0/1 With values

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

The key point to solve knapsack is to see the last step, if order does not matter then what is the last item and if order does not matter, whether last item will be put in knapsack or not.

#### Reference

[https://blog.csdn.net/u013166817/article/details/85449218](https://blog.csdn.net/u013166817/article/details/85449218)

### 如何判断是否是动态规划

* How many ways
* 多少种方式走到右下角
* 多少种方法选出K个数使得和是sum
* 计数型动态规划关键点是要在计数时
  * 没有重复
  * 没有遗漏
* Max / Min
  * 从左上到右下数字和
  * 最长上升子序列
* Existence
  * 取石子，先手是否必胜
  * 能不能取出k个数使得和为一个sum

动态规划组成部分

* 确定状态
  * 研究最优策略的最后一步
  * 化为子问题
* 转移方程
  * 根据子问题定义直接得到
* 初始条件和边界情况
  * 考虑周全
  * 明确实现方式
* 计算顺序
  * 利用之前的计算结果

### 常见题型

* 坐标型
  * 特性
    * 给定序列，网格或矩阵
    * 状态下标为序列下标i, 或者网格坐标i, j
      * dp\[i\], 以第i个元素结尾\(前i个元素\)的某种性质
      * dp\[i\]\[j\], 到格子\[i\]\[j\]的路径的性质
    * 初始化
      * dp\[0\], dp\[0\]\[n - 1\]...
    * 二维空间优化
      * 如果dp\[i\]\[j\]的值只依赖于当前行和前一行，则可以用滚动数组节省空间
  * Unique Paths
* 序列型
  * 特性
    * 给定序列
    * dp\[i\]表示前i项的某种性质
    * 错一位, 因为还要考虑前0项, 即空序列的状态. 初始状态 dp\[0\] -&gt; 空序列性质
  * 前i个，最小/方式数/可能性
  * 在需要状态辅助时开额外维度保存状态, 即序列 + 状态
  * 最简单的动态规划类型
    * 给定一个序列\(sequence\)或网格\(grid\)
    * 找到某个或某些
      * max/min
      * count
      * 存在性
    * 动态规划方程dp\[i\] 中的下标i表示以ai为结尾的满足条件的子序列的性质, dp\[i\]\[j\] 中的下标 i, j 表示以grid\[i\]\[j\]结尾的路径的性质，性质在这里就是
      * max/min
      * count
      * 存在性
    * 初始条件dp\[0\]就是指以a0为结尾的子序列的性质
  * 序列+状态型动态规划
    * 当思考动态规划的最后一步时, 这一步选择依赖于前一步的某种状态
    * 初始化时, dp\[0\]代表前0个元素/前0天/前0...的情况
      * 与坐标型动态规划的区别
    * 计算时, dp\[i\]代表前i个元素\(即元素0~i-1\)的某种性质
  * Paint House
* 划分型
  * Decode ways
* 区间型
* 背包型
  * 
* 最长序列型
  * 题目给定一个序列
  * 找出符合条件的最长序
  * 方法
    * 记录以每个元素i结尾的最长子序列的长度
    * 计算时, 在i之前枚举子序列上一个元素是哪个
  * 为坐标型动态规划
* 博弈型
* 综合型

### 

### 滚动数组

如果对于网格上的动归, 如果f\[i\]\[j\]只依赖于本行的f\[i\]\[x\]与前一行的f\[i - 1\]\[y\], 那么就可以采用滚动数组的方法压缩空间。Space Complexity O\(N\)

如果网格行数少列数多\(胖子网格\), 那么可以逐列计算, 滚动数组的长度为行数，Space Complexity O\(M\)

### 位操作型

* 即二进制类型的位操作
* & 与, \| 或, ^异或, !非
* 以上说的操作都为逐位操作
* 右移一位相当于mod 2 去掉最低位, 右移n位相当于除2的n次方, 左移一位相当于最低位加入一个0, 左移n位相当于乘以2的n次方
* [338. Counting Bits](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/338.-counting-bits)

## Problems

* [63. Unique Paths II](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/63.-unique-paths-ii)
* [91. Decode Ways](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/91.-decode-ways)
* [361. Bomb Enemy](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/361.-bomb-enemy)
* [64. Minimum Path Sum](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/64.-minimum-path-sum)
* [300. Longest Increasing Subsequence](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/300.-longest-increasing-subsequence)
* [256. Paint House](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/256.-paint-house)
* [322. Coin Change](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/322.-coin-change)
* [338. Counting Bits](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/338.-counting-bits)
* [198. House Robber](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/198.-house-robber)
* [265. Paint House II](https://app.gitbook.com/@ericwei0910/s/workspace/~/edit/drafts/-LpzX9SJvLyyGuVqkWHj/leetcode-problems/265.-paint-house-ii)
* [123. Best Time to Buy and Sell Stock III](https://app.gitbook.com/@ericwei0910/s/workspace/leetcode-problems/123.-best-time-to-buy-and-sell-stock-iii)

