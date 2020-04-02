# Sets

* Sets are created through set\(\) function. An Empty list is created. Note that empty Set cannot be created through {}, it creates dictionary. If use {}, upon initialization, it has to have at least one initial element.
* Convert a list to set take O\(n\), check if an item in list takes O\(n\)
* **Checking if an item is in set :** Time complexity of this operation is O\(1\) on average. However u=in worst case it can become O\(n\).
* **Adding elements**:- Insertion in set is done through set.add\(\) function, where an appropriate record value is created to store in the hash table. Same as checking for an item, i.e., O\(1\) on average. However u=in worst case it can become O\(n\).
* Set operations
  * \| for union. O\(m + n\)
  * & for intersection. O\(min\(m, n\)\) 
  * – for difference. set1 - set2 -&gt; O\(len\(set1\)\)
  * ^ for symmetric difference set1 ^ set2 -&gt; O\(len\(set1\)\)
  * &lt;= subset
  * &gt;= superset

