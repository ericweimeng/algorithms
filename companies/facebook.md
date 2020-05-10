# Facebook

## Phone Interview

4/30号的店面，45mins，互相介绍5分钟，然后开始做题。一共一题然后有两问。不知道是不是力扣的原题。 给一个sorted int array，里面有duplicates，第一问求问count number of distinct value. 不能用extra space。 第二问，如果里面重复的数字很多，你要怎么样调整算法。 第一问直接two pointers，第二问 binary search + divide conquer

```python
def count_duplicate(nums):
    if not nums:
        return 0
    res = 1
    if len(nums) == 1:
        return res
    p = nums[0]
    for i in range(1, len(nums)):
        if nums[i] != p:
            res += 1
            p = nums[i]
    return res

            
if __name__ == '__main__':
    nums = [1,1,1,3,4,5,9,10,10]
    nums = [0, 0, 1]
    nums = [1,2,2,3,3,4]
    
    res = count_duplicate(nums)
    print(res)
    

"""
Two pointers, always be cautious about checking if pointers go out of
boundary
"""

def count_dist(a):
  if not a:
    return 0
  if len(a) == 1:
    return 1
  res = 1
  i = 0
  j = 1

  while j < len(a):
    while j < len(a) and a[j] == a[i]:
      j += 1
    # watch out for checking j < len(a)
    if j < len(a) and a[j] != a[i]:
      res += 1
      i = j
      j += 1
  
  return res
```

刚刚结束店面第一题：找lca，bt。followup是如果这个node不在树，该怎么改代码第二题：我没有在lc见过

题意是：给一个木头块数, 和一个整数piece, piece是我们返回给对方的要求木头块的数量，返回最长的木头块长度 比如 arr={5,5,9}, piece=4 5=4+1 5=4+1 9=4+4+1 返回4

arr={100,101}, piece=1 返回101，因为我们只要一个木头，就选一个最长的木头就好了

面试的时候现想的，我想的是用binary search做，这样找到能切的最大值和最小值（0），然后根据mid来看是否能够满足返回piece的条件。这个题目仿佛在哪里见过，但我又想不起来。



1. 给一个array 问swap一次可否变成sorted的。

   例子 1，2，5，4 -》 true

   例子1，5，2，4 -》 false

   楼主的解法是把给的数组sort一下 然后和原数组比较 如果有两个元素不同就是true 其他情况是false

   小哥问题“是否会出现1个元素不同？ 为什么如果4个元素不同 swap一次不能换回来？”

   楼主举了两个例子 但是不知道如果数学上证明不行

2.给一个sorted binary 2d matrix \[\[0, 1, 1\] \[0, 0, 1\] \[0, 0, 0\]\] return 第一个1出现的列的序号，上述例子return 1 用的for循环 + binary search O\(m \* logn\)时间复杂度， 征求面试官同意后开始写。写出来了



给一个长度为N的array， 然后里面有M个部分， 每一部分都是排好序的，输出排好序的array。  
例子\[2,5,6, 1,2,4, 9, 11, 12\] 输出\[1, 2, 2, 4, 5, 6, 9, 11, 12\] 刚开始见到没刷过的题有点紧张， 理解题意花了五分钟，之后代码写的蛮快的，之后和大哥聊了15分钟， 过两天催了HR给了onsite  
  
Given a api you can use: "String read4KB\(\)", which returns next 4kb of a file. \(no access to the file\). the file has zero or more lines in it, each line is separated by new line character: "\n"

Use the above api to implement a new api: String readLine\(\). where each time you call readLine\(\), it returns next line of the file. this maybe called multiple times.

For example: File contains: "Hello\nWorld\nGoodBye"

first time call readline\(\) returns "Hello\n" second time call readline\(\) returns "World\n" thrid time call readline\(\) returns "GoodBye" forth time call readline\(\) returns null



Today I had a phone interview for software developer position at facebook. The interviewer asked me a variation of this problem [https://leetcode.com/problems/continuous-subarray-sum/](https://leetcode.com/problems/continuous-subarray-sum/).

To be exact, Given a list of positive numbers and a target integer k, write a function to check if the array has a continuous subarray which sums to k.

I solved this using the hashmap method. The follow up question was that will my code work if negative numbers are allowed?

Next follow up question was to optimize the space complexity of the problem. She asked what if the list has million elements?

```python
def check_sub_sum(nums, k):
  prefix_sum = {0: -1}
  total_sum = 0  
  for i, num in enumerate(nums):
    total_sum += num
    if total_sum - k in prefix_sum and i - prefix_sum[total_sum - k] > 1:
      return True
    # if elems all non-negative, then the prefix sum is unique
    prefix_sum[total_sum] = i
  return False
  
# if negative elememts are allowed
def check_sub_sum(nums, k):
  # records all the index prefix_sum that appeared
  prefix_sum = collections.defaultdict(list)
  prefix_sum[0] = [-1]
  total_sum = 0
  for i, num in enumerate(nums):
    total_sum += num
    # as long as we can find the diff between cur idx and the farest idx to be
    # greater than 1, then it's possible
    if total_sum - k in prefix_sum and i - prefix_sum[total_sum - k][0] > 1:
      return True
    prefix_sum[total_sum].append(i)
  return False
```



  
**补充内容 \(2020-4-29 13:42\):**  
其实就是个变种的merge k sorted array， 用heap就可以

[328. Odd Even Linked List](../leetcode-problems/328.-odd-even-linked-list.md)

[896. Monotonic Array](../leetcode-problems/896.-monotonic-array.md)

[953. Verifying an Alien Dictionary](../leetcode-problems/953.-verifying-an-alien-dictionary.md)

[269. Alien Dictionary](../leetcode-problems/269.-alien-dictionary.md)

[543. Diameter of Binary Tree](../leetcode-problems/543.-diameter-of-binary-tree.md)

