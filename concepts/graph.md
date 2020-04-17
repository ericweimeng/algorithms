# Graph

## Key points

* Cycles
  * visited set or dictionary
* Disconnected Components

## Graph Representation

Graphs are mathematical structures that represent pairwise relationships between objects. A graph is a flow structure that represents the relationship between various objects. It can be visualized by using the following two basic components:

* Nodes: These are the most important components in any graph. Nodes are entities whose relationships are expressed using edges. If a graph comprises 2 nodes A and B and an undirected edge between them, then it expresses a bi-directional relationship between the nodes and edge.
* Edges: Edges are the components that are used to represent the relationships between various nodes in a graph. An edge between two nodes expresses a one-way or two-way relationship between the nodes.

### **Types of nodes**

* Root node: The root node is the ancestor of all other nodes in a graph. It does not have any ancestor. Each graph consists of exactly one root node. Generally, you must start traversing a graph from the root node.
* Leaf nodes: In a graph, leaf nodes represent the nodes that do not have any successors. These nodes only have ancestor nodes. They can have any number of incoming edges but they will not have any outgoing edges.

### **Types of graphs**

* Undirected: An undirected graph is a graph in which all the edges are bi-directional i.e. the edges do not point in any specific direction.

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/5069914.jpg)

* Directed: A directed graph is a graph in which all the edges are uni-directional i.e. the edges point in a single direction.

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/59ec874.jpg)

* Weighted: In a weighted graph, each edge is assigned a weight or cost. Consider a graph of 4 nodes as in the diagram below. As you can see each edge has a weight/cost assigned to it. If you want to go from vertex 1 to vertex 3, you can take one of the following 3 paths:

  * 1 -&gt; 2 -&gt; 3
  * 1 -&gt; 3
  * 1 -&gt; 4 -&gt; 3

  Therefore the total cost of each path will be as follows: - The total cost of 1 -&gt; 2 -&gt; 3 will be \(1 + 2\) i.e. 3 units - The total cost of 1 -&gt; 3 will be 1 unit - The total cost of 1 -&gt; 4 -&gt; 3 will be \(3 + 2\) i.e. 5 units

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/6fd9992.jpg)

* Cyclic: A graph is cyclic if the graph comprises a path that starts from a vertex and ends at the same vertex. That path is called a cycle. An acyclic graph is a graph that has no cycle.

  A **tree** is an undirected graph in which any two vertices are connected by only one path. A tree is an acyclic graph and has N - 1 edges where N is the number of vertices. Each node in a graph may have one or multiple parent nodes. However, in a tree, each node \(except the root node\) comprises exactly one parent node.

  _**Note**_: A root node has no parent.

  A tree cannot contain any cycles or self loops, however, the same does not apply to graphs.

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/9acf1bc.jpg)

### **Graph representation**

You can represent a graph in many ways. The two most common ways of representing a graph is as follows:

#### **Adjacency matrix**

An adjacency matrix is a **VxV** binary matrix **A**. Element **Ai, j** is 1 if there is an edge from vertex i to vertex j else **Ai, j** is 0.

_**Note**_: A binary matrix is a matrix in which the cells can have only one of two possible values - either a 0 or 1.

The adjacency matrix can also be modified for the weighted graph in which instead of storing 0 or 1 in **Ai, j**, the weight or cost of the edge will be stored.

In an undirected graph, if **Ai, j** = 1, then **Aj, i** = 1. In a directed graph, if **Ai, j** = 1, then **Aj, i** may or may not be 1.

Adjacency matrix provides **constant time access** **\(O\(1\) \)** to determine if there is an edge between two nodes. Space complexity of the adjacency matrix is **O\(V2\)**.

The adjacency matrix of the following graph is:  
**i/j** : **1 2 3 4**  
**1** : 0 1 0 1  
**2** : 1 0 1 0  
**3** : 0 1 0 1   
**4** : 1 0 1 0

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/b64ec49.jpg)

The adjacency matrix of the following graph is:

**i/j**: **1 2 3 4**  
**1** : 0 1 0 0  
**2** : 0 0 0 1  
**3** : 1 0 0 1  
**4** : 0 1 0 0

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/c6f238c.jpg)

Consider the directed graph given above. Let's create this graph using an adjacency matrix and then show all the edges that exist in the graph.

#### **Adjacency list**

The other way to represent a graph is by using an adjacency list. An adjacency list is an array A of separate lists. Each element of the array **Ai** is a list, which contains all the vertices that are adjacent to vertex i.

For a weighted graph, the weight or cost of the edge is stored along with the vertex in the list using pairs. In an undirected graph, if vertex j is in list **Ai** then vertex i will be in list **Aj**.

The space complexity of adjacency list is **O\(V + E\)** because in an adjacency list information is stored only for those edges that actually exist in the graph. In a lot of cases, where a matrix is sparse using an adjacency matrix may not be very useful. This is because using an adjacency matrix will take up a lot of space where most of the elements will be 0, anyway. In such cases, using an adjacency list is better.

_**Note:**_ A sparse matrix is a matrix in which most of the elements are zero, whereas a dense matrix is a matrix in which most of the elements are non-zero.

![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/f19ece7.jpg)

Consider the same undirected graph from an adjacency matrix. The adjacency list of the graph is as follows:

A1 → 2 → 4  
A2 → 1 → 3  
A3 → 2 → 4  
A4 → 1 → 3  
![enter image description here](https://he-s3.s3.amazonaws.com/media/uploads/031c285.jpg)

Consider the same directed graph from an adjacency matrix. The adjacency list of the graph is as follows:

A1 → 2  
A2 → 4  
A3 → 1 → 4  
A4 → 2

