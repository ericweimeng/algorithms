# Binary & Bitwise

## Binary

* Smallest unit in computer is bit, which is just a slot to be charged or uncharged represent on or off \(1/0\)
* 8 bits represent 1 bytes that represents a range 1 ~ 256 \(2 ^ 8\)
  * e.p. 16 GB ~= 16 billion bits
* Every thing that can be stored and processed in computer has to be converted in this binary format in the machine
* How python store integers
  * positive integers
    * 0110 = 6
  * negative integers
    * 2's complement =&gt; flip + 1
      * 6 -&gt; 0110 -&gt; flip to 1001 -&gt; add 1 to 1010 = -6 but it also 10 but here the most significant pos will be a sign, if it is a 0 then it's positive number
* When we do 32 - bit math, then at the cpu level, it's a overflow, and needs to use more bits
* ~a invert -&gt; invert x = -\(x + 1\)
* a & b bitwise and -&gt; keep same bits, mostly used for masking
* a \| b or most used for setting a bit
* a ^ b xor -&gt; find the difference, can recover later, double xor gets back to original data
* bin\(\), oct\(\), hex\(\)
* &lt;&lt;, &gt;&gt;
  * a &lt;&lt;, &gt;&gt; b
    * &lt;&lt; \* 2 ^ b
      * quickly to do multiplication
    * &gt;&gt; // 2 ^ b
      * get the rightmost bit

{% embed url="https://blog.csdn.net/MoreWindows/article/details/7354571" %}

### Basics

{% embed url="https://zhuanlan.zhihu.com/p/37549805" %}

### Application

{% embed url="https://zhuanlan.zhihu.com/p/37909700" %}



