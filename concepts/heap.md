# Heap

A Heap is a special Tree-based data structure in which the tree is a complete binary tree. Generally, Heaps can be of two types:

Max-Heap: In a Max-Heap the key present at the root node must be greatest among the keys present at all of it’s children. The same property must be recursively true for all sub-trees in that Binary Tree.

Min-Heap: In a Min-Heap the key present at the root node must be minimum among the keys present at all of it’s children. The same property must be recursively true for all sub-trees in that Binary Tree.

## Heap in Python

Heap in Python is a binary heap, with O\(logN\) push and O\(logN\) pop. Python also implements the heap as min-heap, which the value on top of the stack is the smallest among all elements.

After heapifying a list to a heap or directly push element to the heap, the heap itself is still a list but just in binary tree format, heapify a list takes O\(n\) and in-place.

