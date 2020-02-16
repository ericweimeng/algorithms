---
description: Python implementations
---

# Algorithms

This is a central platform to store all knowledge base, notes and code for python related algorithms.

Github link for code: [here](https://github.com/ericweimeng/csbase/tree/master/algorithm)

## Ways of thinking

* Counterintuitive Thinking
* Backward Reasoning

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

* [Longest string made up of only vowels](leetcode-problems/0.-longest-string-made-up-of-only-vowels.md)
* [1.Two Sum](leetcode-problems/1.-two-sum.md)
* [994. Rotting Oranges](leetcode-problems/994.-rotting-oranges.md)
* [1102. Path With Maximum Minimum Value](leetcode-problems/1102.-path-with-maximum-minimum-value.md)
* 1167. Minimum Cost to Connect Sticks
* [1192. Critical Connections in a Network](leetcode-problems/1192.-critical-connections-in-a-network.md)

{% page-ref page="./" %}

