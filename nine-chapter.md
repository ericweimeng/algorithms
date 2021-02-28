# Nine chapter



**Binary search**

**Keypoints:**

1. **Start + 1 &lt; end // 保证退出条件是两元素相挨**
2. **Start + \(end - start\) / 2 // 防止 \(start + end\) / 2 可能的 stack overflow**
3. **A\[mid\] ==, &lt;, &gt;**
4. **A\[start\], A\[end\] ? target**
5. **有关二分法的题目基本可以概括为要不找满足条件的first position 或是满足条件的 last position**

**LinkedList**

**当你不确定head的时候用dummy node, 在LikedList里删除一个node其实跟被删除的node无关，而是跟这个node的前后两个node有关。在list中一定要注意检查你要访问的节点是否为空。即\(head.next != null\)**  


**O\(nlogn\) time complexity**

**堆排序，快速排序，归并排序**  


**Data Structure**

 **Linear Data Structure**

 **Queue**

 **Stack**

 **Hash**

 **Tree Data Structure**

 **Heap**

 **Trie**

 **Queue \(first in first out\)**

 **Operation: O\(1\) push, O\(1\) pop, O\(1\) top**

 **Always used for BFS**

 **Stack \(first in last out\)**

 **Operation: O\(1\) push, O\(1\) pop, O\(1\) top**

 **- Min-stack**

 **Implement a stack, enable O\(1\) push, pop, top, min. Where min\(\) will return the value of the minimum number in the stack.** 

**Hash**

**Operations: insert - O\(1\), delete - O\(1\), find - O\(1\)**

**Hash Function**

**Collision** 

* **Open Hashing \(LinkedList\), create a linked list where elements with the same hashcode.**
* **Closed Hashing \(Array\), put element to right or left direction the first position follows it without element**
* **Rehashing, double the original size and rehash the array**

**Heap**

**Priority Queue**

**Trie Tree -- search tree**

 **Hash vs Trie**

 **Time complexity Hash O\(1\) is for the whole string, not for character.**

 **The advantage of trie: 1. Needs iterate a string character by character. 2. Save space.**

**Graph & Search**

* **Graph:**
  * **Clone Grap: Copy list with random pointer**
  * **Topological Sorting**
    * **拓扑排序实例：**
    * **某一步的进行需要上一步进行完的结果，这一步进行完的结果会是下一步的需要。**
    * **同样适用宽度优先搜索。**
    * **对于有向图，有出度和入度**
    * **入度为有多少点指向此点，出度为此点有多少出去的指向。**
    * **所以此种类型的题可以变为先遍历入度为0的点，完成后擦去此点的所有出度点，然后再向前走找上一个点被擦除后剩下入度为零的点再遍历。**
* **Search:**
  * **Depth First Search \(O\(2^n\), O\(n!\)\) \(思想:构建搜索树+判断可行性\)**
    * **找所有情况时考虑用此法 \(find all possible solutions\)**
    * **Permutations / Subsets**
  * **Breadth First Search \(O\(m\), O\(n\)\) \(每个点只遍历一次\)**
    * **此方法用的情况为：从某个点出发找到或遍历所有点**
    * **经常配合队列使用**
    * **Graph traversal**
    * **Find shortest path in a simple graph**
    * **广度优先搜索的基本思路一般为，如果是树，队列里从头到尾可以依次存取深度逐渐增加的元素，如果是图，则出现在队列里的都是互相之间有联系的点。**

**Dynamic Programming**

* **递归有两种**
  * **Traverse遍历**
    * **比如求三角形最小和，这个方法把sum值作为参数传入**
  * **Divide and Conquer 分治**
    * **比如求三角形最小和，这个方法把sum值作为返回值返回**
* **Memorization Search 就是 动态规划 的递归实现方式**
  * **即 大问题 -&gt; 小问题 //比递归好在解决了重复计算的问题，子 问题间存在交集**
* **如何想到使用DP 满足下面条件**
  * **Maximum/Minimum \(or longest shortest\)**
  * **Yes/No \(有没有可行方案\)**
  * **Count\(\*\) \(可行方案的个数\)**
  * **\(之前三点之外如果再匹配这个就更确定是动归\)Can not sort / swap**
  * **注意要说列出所有方案就一定不是动归**
* **动态规划的4点要素**
  * **状态 State  存储小规模问题的结果**
  * **方程  状态之间的联系**
  * **初始化  最极限的小状态是什么，起点**
  * **答案  最大的那个状态是什么，终点** 
* **动归4大常考题型**
  * **Matrix DP \(矩阵动归\)**
    * **State: f\[x\]\[y\] 表示从起点走到坐标x,y的....**
    * **Function: 研究走到x,y这个点之前的一步**
    * **Initialize: 起点**
    * **Answer: 终点**
    * **如果是二维动归矩阵就要考虑 f\[i\]\[0\]如何初始化，f\[0\]\[i\]如何初始化**
  * **Sequence DP**
* **State: f\[i\] 表示前”i”个位置/数字/字母, 以第i个为...**
* **Function: f\[i\] = f\[j\]... j 是i之前的一个位置**
* **Initialize: f\[0\] …**
* **Answer: f\[n - 1\]...**
* **很重要的是研究上一步/最后一步怎么来的**

**Advanced**

* **Kth 规律**
  * **1. 见到需要维护一个集合的最小值/最大值的时候要想到用堆**
  * **2. 第k小的元素，heap用来维护当前候选集合**
  * **3.见到数组要想到先排序**
* **Data Structure**
  * **Union Find**
    * **并查集，一种用来解决结合查询合并的数据结构**
    * **支持 O\(1\) find/ O\(1\) union**
    * **并查集可以**
      * **判断在不在同一个集合中**
        * **Find操作**
      * **集合合并**
        * **Union操作**
    * **不支持删除**
    * **不会出现环**
    * **完整模板**

![Screen Shot 2016-10-28 at 15.03.27.png](https://lh3.googleusercontent.com/nOJRXS8bPf6Pr8GkWrHTAvQFe6JoWkt2muw7zyXH3LRcUQIRDqkVgx2eahfODoWZiVyhXUaD67YseWbL6joFXKSL5nKIq0veyEaj7eNFO4K6voYBdUxIAMfCb0xxtMqIuM8AvAL-)

**在无向图中找出同属一个集合的点可以让其中一点成为代表他们那个集合的代表点，其他属于这一集合的都标为此点，如下图 \(BFS\)**  


![](https://lh3.googleusercontent.com/sYrAYzkzHtCC929303T9f5JLpq_utWhmODOD5p0_tF_diHRFAt_k-vkvKYVcAIM5XH3mb5sj9HhL9CSVo5zi1TeXWn76_3bTM-MUD5Td93xOm9IsC4DWgzwOErTFIRDOlCgfd1hB)

**同样也可以用union find, 即最开始时初始化每个点为自己单独的集合然后遍历整个所有边，遍历到有共同边的两点即把两点做union，而且在做union的时候查看两个点所在集合的size，把size小的集合并到size大的集合上**  


![](https://lh5.googleusercontent.com/Fhw3O-mirHG08oLrTrt8p2IdLQUW9o2gwkb80XKknfofvVDl-q9IaCq38c7f5IaULx_O1nDqfDVqvY6us7XQvpIrR16utwszQTXxO23RSAODWbiwNwWv7WRjToQi29VyFiRxwC7m)

* **有向图比起无向图来说不同的一点是对于某一点你能拿到邻接点而不是所有相邻点。** 
* **判断输入的边是否能构成一个树，我们需要确定两件事：**
  * **这些边是否构成环路，如果有环则不能构成树**
  * **这些边是否能将所有节点连通，如果有不能连通的节点则不能构成树**
* **Trie树\(字典树\)**
  * **每个点都是26叉**
  * **有一个空的虚根**
* **Two pointers**
* **Partition**
  * **Find top k elements**
    * **PriorityQueue is a perfect solution**
    * **O\(nlogk\)**
  * **Find kth** 
    * **O\(n\)**
    * **Quick select**
      * **Find any element as a pivot, then swap it with most left element, pivot stored in pointer, therefore the leftmost position is not actually sits the pivot element. Do it on every elements in array, finally we got a state where all elements sit at the left side of the pivot less than pivot, all elements sit at the right side of the pivot less than pivot.**
    * **Partition**
      * **Two pointers, one is left, the other is right, first right is pivot compare it with left. If greater than pivot, swap right with left, if less than, continue. Then compare right with left less than, swap, greater than continue.**
      * **Left alternate with right forward**
* **Questions**
  * **Two Sum 2**
  * **Triangle count**
* **双指针优化类型:**
  * **优化思想通过两层循环，即两个指针**
  * **外层指针依然是依次遍历**
  * **内层指针证明是否需要回退**
* **通过两层for循环改进算法:**
  * ![Screen Shot 2016-10-27 at 10.14.35.png](https://lh4.googleusercontent.com/Z0YdXwe3UjrWamX4UHVViyVlqtm_GNTbfV8R94j0Na90MnGIKiswVLf0KGebydTNwv-iNWAE4qb8NKlamHF4IA1VImV8QwMdnGKIF99VEzW6_q5pfFoFadWIWt2lKTFDd-NGKffd)

