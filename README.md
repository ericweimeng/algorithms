---
description: Python implementations
---

# Algorithms

This is a central platform to store all knowledge base, notes and code for python related algorithms.

Github link for code: [here](https://github.com/ericweimeng/csbase/tree/master/algorithm)

## Ways of thinking

* 逆向思维 backward reasoning
  * 如果是这个是结果会有什么性质
* 找规律从小的数据量开始 starting from small set of data
* 寻找反例去尝试验证当前结论 try beating your conclusion
* 考虑 corner case
* 大问题分解为小问题，小问题分解为原子问题，递归思想。

## Input Size and Time Complexity

### CPU capacity

CPU: 2GHz ~ 2G ops \(w/o SIMD\) -&gt; $$2*10^{9} $$ \(single core/single thread\)

Overhead: memory access / branching. 

Large const factor: unordered\_set O\(1\) can be an order slower than set O\(logn\) even n is 128. O\(1\) ~ O\(100\)

Rough estimation: $$10^{6}$$ ~ $$10^{7}$$ ops/sec based on time complexity, so if n == 1000 then O\($$n^{2}$$\) is around $$10^{6}$$

![Reference: https://zxi.mytechroad.com/blog/sp/input-size-v-s-time-complexity/](.gitbook/assets/image%20%283%29.png)

* &lt; 10: O\(n!\) permutation
* &lt; 15: O\(2^n\) combination
* &lt; 50: O\(n^4\) DP
* &lt; 200: O\(n^3\) DP, all pairs shortest path
* &lt; 1,000: O\(n^2\) DP, all pairs, dense graph
* &lt; 1,000,000: O\(nlogn\), sorting-based \(greedy\), heap, divide & conquer
* &lt; 1,000,000: O\(n\), DP, graph traversal / topological sorting \(V+E\), tree traversal
* &lt; INT\_MAX: O\(sqrt\(n\)\), prime, square sum
* &lt; INT\_MAX: O\(logn\), binary search
* &lt; INT\_MAX: O\(1\) Math

## Amazon Questions Quick Links

### OA

* [0. Longest string made up of only vowels](leetcode-problems/0.-longest-string-made-up-of-only-vowels.md)
* [0. Top N Buzzwords](leetcode-problems/top-n-buzzwords.md)
* [1.Two Sum](leetcode-problems/1.-two-sum.md)
* 692. Top K Frequent Words / 0. Top K Frequent Words
* [200. Number of Islands](leetcode-problems/200.-number-of-islands.md)
* [994. Rotting Oranges](leetcode-problems/994.-rotting-oranges.md)
* [1102. Path With Maximum Minimum Value](leetcode-problems/1102.-path-with-maximum-minimum-value.md)
* [1167. Minimum Cost to Connect Sticks](leetcode-problems/1167.-minimum-cost-to-connect-sticks.md)
* [1192. Critical Connections in a Network](leetcode-problems/1192.-critical-connections-in-a-network-1.md)
* [1268. Search Suggestions System / Product Suggestion](leetcode-problems/1268.-search-suggestions-system.md)
* [937. Reorder Data in Log Files](leetcode-problems/937.-reorder-data-in-log-files.md)
* [1167. Minimum Cost to Connect Sticks / Min Cost to Connect Ropes / Min Time to Merge Files](leetcode-problems/1167.-minimum-cost-to-connect-sticks.md)
* [138. Copy List with Random Pointer](leetcode-problems/138.-copy-list-with-random-pointer.md)
* 1155. Number of Dice Rolls With Target Sum
* [21. Merge Two Sorted Lists](leetcode-problems/21.-merge-two-sorted-lists.md)

{% page-ref page="./" %}

## Matrix problems

* Things to keep in mind:
  * if coordinates in matrix
  * duplicate visit
  * pattern discovery
    * try draw lines to connect points

## Follow ups

## General checklist for a coding problem

* input
  * numbers
    * signed or unsigned
    * how large and small
    * type
      * int
      * float
      * string format
  * list
    * type of the elements
  * empty
* output
  * type
    * bool
    * numbers
    * list
      * nested list
    * string
    * dict
    * null
    * ...
* Specific checking
  * link list
    * cycle
    * 

## General Thoughts

* General checking at the end
  * '=' and '=='
  * if all params all passed in correctly \(especially for recursive calls\)
  * corner cases checking
* if you want to return from a function immediately, then might just consider to not use dfs recursion and use traverse like 'while'
* 如果有按某一key去group相似的数据在一起的这类题可以考虑用hashmap, 比如相同的prefix，age, level of a tree
* 字符串形式的数字在扫描每一位时要注意一个vaild的数字可能不止一位所以考虑去做 10 \* accumulated\_num + cur\_digit
* **On a board**
  * Check if current coordinate is within the range
  * Check if current coordinate was visited before
* **On a graph**
  * Consider disconnected component
  * Consider cycles
    * Check visited
* **While loop / double pointers, please remember to increase or decrease pointers**
* **When going through the code and doing checking, try imagining the process use real cases**
* Please watch out for '=' and '=='
* If do list addition, checking if values on both sides of '+' are type of list
* When doing graph/matrix\(and others\) dfs, checking if mark each to node that visited
* Remember that path.sort\(\) returns nothing, it sorts the array in-place
* For DFS or Non-recursive DFS, remember to **add next level elements** to stack/queue
* When using stack to do level order traverse, it pops element from top of the stack, then it causes issue
* When to possibly use binary search
  * give data set is sorted
  * It is asked to find certain element or you are trying to find a certain characteristics appeared/happened at/from a certain point 
* floating
  * **向上取整**
    * print "math.ceil---" print "math.ceil\(2.3\) =&gt; ", math.ceil\(2.3\) print "math.ceil\(2.6\) =&gt; ", math.ceil\(2.6\)
  * **向下取整**
    * print "\nmath.floor---" print "math.floor\(2.3\) =&gt; ", math.floor\(2.3\) print "math.floor\(2.6\) =&gt; ", math.floor\(2.6\)
  * **四舍五入**
    * print "\nround---" print "round\(2.3\) =&gt; ", round\(2.3\) print "round\(2.6\) =&gt; ", round\(2.6\)

      **这三个的返回结果都是浮点型**

