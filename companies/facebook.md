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
```

