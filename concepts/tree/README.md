# Tree

## Basic Concepts

### Binary Tree Preorder & Inorder & Postorder Traversal

#### Preorder

```python
# recursion
def preorder_traversal(root):
  if not root:
    return
  
  print(root.data)
  preorder_traversal(root.left)
  preorder_traversal(root.right)

# non recursion
def preorder_non_recursion_traversal(root):
  if not root:
    return
  stack = [root]
  while stack:
    node = stack.pop()
    if node is not None:
      print(node.val)
      if node.right is not None:
        stack.append(node.right)
      if node.left is not None:
        stack.append(node.left)
```

#### **Inorder**

```python
# recursion
def inorder_traversal(root):
  if not root:
    return
  
  inorder_traversal(root.left)
  print(root.data)
  inorder_traversal(root.right)

# non recursion
def inorder_non_recursion_traversal(root):
  if not root:
    return
  
  cur = root
  stack = [root]
  while stack:
    if cur.left is not None:
      stack.append(cur.left)
      cur = cur.left
      continue
    node = stack.pop()
    print(node.val)
    if node.right is not None:
      stack.append(node.right)
      cur = node.right
      continue
```

#### **Postorder**

```python
def postorder_travseral(root):
  if not root:
    return
  
  postorder_travseral(root.left)
  postorder_travseral(root.right)
  print(root.data)
```

#### Tips

* Based on the trait of the tree data structure, the traversal will arrive the node of the tree 3 times. Therefore, the essence of traversal is essentially at which time you want to process the node
* the entire tree can be represented by only the right border of each subtree, and this is the basis for morris traversal

### **Successor and Precursor**

In inorder traversal, the **successor** is the node that **comes after the current node**, and the **precursor** is the node that **comes before the current node**.

```text
in tree:  
       1
      / \
    2    3
   / \   / \
  4   5 6   7

inorder traversal is 4251637, then 4 is 2's precursor, 5 is 2's successor
```

#### Tips

* If a node has right sub-tree, then the successor of this node is the leftmost node of its right sub-tree
* If a node does not have right sub-tree, then it should trace back to its parent node in order to check if this node is the left node of its parent. If it is the left node of its parent then the parent node is its successor, otherwise, keep tracing back upward and then apply the same rule
* If a node has left subtree, then the precursor of this node is the rightmost node of its left subtree
* If a node does not have left subtree, then the precursor is its parent node

### Serialization and Deserialization

* **Serialization** is the process of converting an object into a stream of bytes to store the object or transmit it to memory, a database, or a file. Its main purpose is to save the state of an object in order to be able to recreate it when needed. The reverse process is called deserialization.
* Traverse through the entire tree, if it's a node, then use its value plus a symbol \(a symbol can be any kinds of character ie ',', '\_'\)

```text
in tree:  
           1
          / \
        2    3
       / \   / \
      4   5 6   7
      
preorder plus ',' : '1,2,4,#,#,5,#,#,3,6,#,#,7,#,#'
```

* Deserialization is the reverse process of serialization

### **Balanced Binary Tree**

A binary tree with which the height of the two subtrees of _every_ node never differ by more than 1.

To determine if a binary tree is a balanced binary tree

* If left subtree is balanced
* If right subtree is balanced
* What is the height of left subtree
* What is the height of right subtree
* If the recursion result of left subtree is false, return false and height 0
* If the recursion result of right subtree is false, return false and height 0
* If both left and right subtree is balanced, then pick the one with maximum height: max\(left, right\), return true height + 1 

```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        
        if not root:
            return True
        
        return abs(self.get_height(root.left) - self.get_height(root.right)) <= 1 and self.isBalanced(root.left) and self.isBalanced(root.right)
    
                  
    def get_height(self, root):
        if not root:
            return 0
        return max(self.get_height(root.left), self.get_height(root.right)) + 1
```

### **Full Binary Tree and Complete Binary Tree**

* A **full binary tree** \(sometimes proper binary tree or 2-tree\) is a tree in which every node other than the leaves has two children.
* A **complete binary** tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
* Determine if a binary tree is a complete binary tree
  * If any left or right subtree is missing then it is not a complete binary tree
  * All nodes have to be leaves, if it's for the first time that sees a node has left child node but does not have right child node
* The total number of nodes of a full binary tree is 2 \*\* h - 1 \(h is the height of the tree\) square

### **Binary Search Tree**

* The inorder traversal is ascending order
* Usually no duplicated values, all duplicated nodes with same value will be stored in one node

## Trail of thoughts

### Recursion or Non-recursion

* Check the depth of the tree
  * It will be stack overflows if it's too deep
  * Stack overflow usually describes the overflow the stack space that the OS allocated. The stack memory is privately held by the program

### Time Complexity of Recursion

* Number of nodes \* processing time on each node

### Steps to Implement Recursion

* Definition of recursion
* Breakdown of recursion
* Exit of recursion
* Invoke of recursion

### Traversal vs Divide & Conquer

* Traversal
  * Traversal is a process of going down a searching path and access each node only once. Utilize global variable to record the result. Usually there's no return value from a traversal and result is passed in as parameters
* Divide and Conquer
  * Break down one problem into many sub-problems, and the combinations of the solutions of all sub-problems is the result of this problem. It usually requires a return value from each sub-problem
* They are both recursion algorithm
* result in parameter vs result in return value
* Top down vs Bottom up

### Tree DFS

```text
               DFS
            /      \ 
        recursion  non-recursion
        /       \ 
    traversal divide and conquer
```

### Basic Solutions

* Think about the relation between the solution of entire tree and the solutions of all subtrees

#### Tips

* If return a single value is not enough in divide and conquer, then you can wrap everything you want to return in a customized type

