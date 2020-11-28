# Dynamic Programming

## 

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

### LC 对应刷过题型

* 其他
  * 10
  * 1335
* 序列型
  * 单序列型
    * 300
  * 双序列型
    * 基本方向-&gt; 解决两个字符串的动态规划问题，一般都是用两个指针 `i,j` 分别指向两个字符串的最后/开始，然后一步步往前走/后走，缩小问题的规模
    * 1143
    * 583 -&gt; 删除后的结果为两串最长公共序列\(LCS\)
    * 72 s1 -&gt; s2 same as s2 -&gt; s1
* 背包型
  * 322
  * 416
  * 494
    * 完全背包
      * 518



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

