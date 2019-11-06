# Disjoint Set / Union Find

## Disjoint Set

A [_disjoint-set data structure_](http://en.wikipedia.org/wiki/Disjoint-set_data_structure) is a data structure that keeps track of a set of elements partitioned into a number of disjoint \(non-overlapping\) subsets. 

### **Tree representation**

Suppose we have the following disjoint sets:

![Disjoint Set](../.gitbook/assets/image%20%286%29.png)

Then these disjoint sets may be represented as trees:

![Disjoint Set Tree Representations](../.gitbook/assets/image%20%284%29.png)

Note how every node has a parent pointer. A root node in particular has a parent pointer that points to itself.

We can implement the trees with an array which we denote as parent. The entry parent\[i\] indicates the parent of node i:

```
       i  : 1 2 3 4 5 6 7 
parent[i] : 2 2 2 5 5 6 7 
```

For instance, parent\[3\]=2 means that node 3 has node 2 as its parent. Another example is parent\[2\]=2 since node 2 points to itself. We can already see that a root node r is characterized by parent\[r\] == r.

## Union Find

A [_union-find algorithm_](http://en.wikipedia.org/wiki/Disjoint-set_data_structure) is an algorithm that performs two useful operations on such a data structure:

#### Find

Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset.

We can determine if two elements are in the same set by checking if the corresponding two nodes have the same root. For this we write a function called _find_ which returns the root of a tree.

```
def find(x)
     if parent[x] == x:
        return x
     else:
        return find(parent[x])
```

This recursive function starts at a node x and climbs up the tree until it finds a root node. Recall that a root node r has the property parent\[r\] == r. Here is a table that shows the result of find\(x\) for all nodes x:

```
     x  : 1 2 3 4 5 6 7
find(x) : 2 2 2 5 5 6 7
```

#### Union

Join two subsets into a single subset.

The union-find data structure is created by starting with n singleton sets. As an example lets start with n=8 singleton sets:

![](../.gitbook/assets/image%20%285%29.png)

![](../.gitbook/assets/image%20%281%29.png)

The parent array for the initial situation looks like this:

```
       i  : 1 2 3 4 5 6 7 8
parent[i] : 1 2 3 4 5 6 7 8
```

We perform some union operations: union\(2,1\), union\(4,3\), union\(6,5\), where union\(x, y\) means we perform the union of the sets with element x and element y:![\{1,2\}, \{3,4\}, \{5,6\}, \{7\}, \{8\}](https://s0.wp.com/latex.php?latex=%5C%7B1%2C2%5C%7D%2C+%5C%7B3%2C4%5C%7D%2C+%5C%7B5%2C6%5C%7D%2C+%5C%7B7%5C%7D%2C+%5C%7B8%5C%7D&bg=e9e9dc&fg=333333&s=0). For our tree data structure union\(x, y\) means we link the root of node x to the root of node y.

[![uf2\_union2](https://algocoding.files.wordpress.com/2014/09/uf2_union2.png?w=600&h=106)](https://algocoding.files.wordpress.com/2014/09/uf2_union2.png)

We perform union\(2, 4\), i.e. the root of 2 is linked to the root of 4:  
![\{1,2,3,4\}, \{5,6\}, \{7\}, \{8\}](https://s0.wp.com/latex.php?latex=%5C%7B1%2C2%2C3%2C4%5C%7D%2C+%5C%7B5%2C6%5C%7D%2C+%5C%7B7%5C%7D%2C+%5C%7B8%5C%7D&bg=e9e9dc&fg=333333&s=0)

[![uf2\_union3](https://algocoding.files.wordpress.com/2014/09/uf2_union3.png?w=600&h=159)](https://algocoding.files.wordpress.com/2014/09/uf2_union3.png)

Again we can check if two elements are in the same set by checking if their corresponding nodes have the same root. For example, find\(2\)=3 and find\(4\)=3 means that 2 and 4 have the same root, and therefore are in the same set. On the other hand find\(2\)=3 and find\(6\)=5 means that 2 and 6 have different roots, and therefore 2 and 6 are in different sets.

```
def union(x, y):
     x_root = find(x)
     y_root = find(y)
     parent[x_root] = y_root
```

#### **Path compression**

When we call the find function we traverse the path from a node x up to its root r. Instead of just returning r we will do some additional work, namely we will link all the nodes in this path directly to r. In other words we will set parent\[x\]=r for all nodes x in the path. The advantage is that if we call find for node x again \(or some other node in the path\), then we don’t have to walk that whole path again but instead are only one step away from r. This is called _path compression_ which helps to keep the trees flat.

[![uf3\_path\_compression](https://algocoding.files.wordpress.com/2014/09/uf3_path_compression.png?w=600&h=267)](https://algocoding.files.wordpress.com/2014/09/uf3_path_compression.png)

Path compression requires only a small modification of our original find function:

```
def find(x):
     if parent[x] != x:
        parent[x] = find(parent[x])
     return parent[x]
```

#### **Union by rank**

A problem with the union function is that a tree of height![\theta\(n\)](https://s0.wp.com/latex.php?latex=%5Ctheta%28n%29&bg=e9e9dc&fg=333333&s=0)can be created by performing the operations union\(n, n-1\), union\(n-1,n-2\), …, union\(2, 1\). As a consequence a find operation will take![\theta\(n\)](https://s0.wp.com/latex.php?latex=%5Ctheta%28n%29&bg=e9e9dc&fg=333333&s=0)time in the worst-case for this tree. We can prevent this by modifying union\(x, y\). Instead of simply linking the tree of x to the tree of y, we will first compare their heights. The tree with smaller height is then linked to the tree with greater height. This is called _union by rank_. Note: Technically the rank is an upper bound for the height of a tree. The rank is not the height because during a find operation with path compression the height of a tree might become smaller, whereas the rank is not updated in the find function.

[![uf4\_union\_by\_rank](https://algocoding.files.wordpress.com/2014/09/uf4_union_by_rank.png?w=600&h=458)](https://algocoding.files.wordpress.com/2014/09/uf4_union_by_rank.png)

We can implement union by rank as follows:

```

def union(x, y):
     x_root = find(x)
     y_root = find(y)
     if x_root == y_root:
         return

     if rank[x_root] > rank[y_root]:
         parent[y_root] = x_root
     else:
         parent[x_root] = y_root
         if rank[x_root] == rank[y_root]:
             rank[y_root] = rank[y_root] + 1
```

rank is an array, and rank\[i\] returns the rank for node i.

### When to use Union Find

* Determines if two nodes are in the same set
  * find O\(1\) - append the parent node of a node to the parent of another set
  * in an optimized compress\_find way, the complexity is still O\(1\), because the time complexity is amortized, path compress would be O\(n\) for the first time then find parent again for all those nodes later would be O\(1\)
* Sets union
  * union O\(1\) - use hash map or array to store the parent of a node

### What union find algorithm doesn't have

* Delete an element
* Never will have any circles

