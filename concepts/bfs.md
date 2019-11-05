---
description: Breath First Search
---

# BFS

## When to Use

* Traversal in Graph
  * Level Order Traversal \(层级遍历\)
  * Connected Component \(由点及面\)
  * Topological Sorting \(拓扑排序\)
* Shortest Path in Simple Graph
  * Find shortest path in a simple graph
    * i.e. every edge in a graph has length of 1 , undirected, unweighted \(无向无权重\)

## BFS in Various data structure

### BFS \| Tree

* Traverse by level
* Queue
* Stack, reverse

### BFS \| Graph

* Difference between graph and tree
  * Graph has circle, tree never has circle
* Directed Graph
  * Topological Sorting
    * in-degree / out-degree

### BFS \| Topological Sorting

* Topological sorting for Directed Acyclic Graph \(DAG\) is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering
* Topological Sorting for a graph is not possible if the graph is not a DAG
* The first vertex in topological sorting is always a vertex with in-degree as 0 \(a vertex with no incoming edges\)
* Implementation
  * At each level, collection all nodes with 0 in-degree in a queue, traverse them, and then move to nest level

## Problems

* [Number of Islands](../leetcode-problems/200.-number-of-islands.md)
* [Friend Circles](../leetcode-problems/547.-friend-circles.md)
* [Accounts Merge](../leetcode-problems/721.-accounts-merge.md)

