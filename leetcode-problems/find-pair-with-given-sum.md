# Find Pair With Given Sum

> Given a list of positive integers `nums` and an int `target`, return indices of the two numbers such that they add up to a `target - 30`.
>
> Conditions:
>
> * You will pick exactly 2 numbers.
> * You cannot pick the same element twice.
> * If you have multiple pairs, select the pair with the largest number.
>
> **Example 1:**
>
> ```text
> Input: nums = [1, 10, 25, 35, 60], target = 90
> Output: [2, 3]
> Explanation:
> nums[2] + nums[3] = 25 + 35 = 60 = 90 - 30
> ```
>
> **Example 2:**
>
> ```text
> Input: nums = [20, 50, 40, 25, 30, 10], target = 90
> Output: [1, 5]
> Explanation:
> nums[0] + nums[2] = 20 + 40 = 60 = 90 - 30
> nums[1] + nums[5] = 50 + 10 = 60 = 90 - 30
> You should return the pair with the largest number.
> ```

## Solutions

### Approach \#1

The idea to approach this problem is to traverse the array and for each element we check if it has existed in a hashmap. If not, we use target subtracts current number as the key, current index as value so that if it finds an element later that with current element, add up to the target - 30, we can access its index to add to result. It also checks if the current candidate pair with either values greater than a largest\_seen value from previous found pairs.

Time: O\(n\)

Space: O\(n\)

```python
def findSum(nums, target):
    if not nums:
        return []
    target -= 30
    m = {}
    largest_seen = -1
    res = []
    for i, num in enumerate(nums):
        if num not in m:
        # if target - num not in m:
            m[target - num] = i # only here need target - num
        else:
            if num > largest_seen or target - num > largest_seen:
                # res = [m[target - num], i]
                res = [m[num], i]
                largest_seen = max(num, target - num)
    return res
```

```python
def findSum(nums, target):
    if not nums or not target:
        return []
    target -= 30
    m = {}
    largest = -1
    res = [-1,-1]
    for i in range(len(nums)):
        if nums[i] not in m:
            m[target - nums[i]] = i
        else:
            if nums[i] > largest or target - nums[i] > largest:
                res[0] = m[nums[i]]
                res[1] = i
                largest = max(nums[i], target - nums[i])
    if res != [-1,-1]:
        return res

    return []
```

