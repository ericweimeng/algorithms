# Binary Search

## Binary Search 

```python
def binary_search1(nums, target):
  if not nums or not target:
    return -1
  l, r = 0, len(nums) - 1
  while l <= r:
    mid = (l + r) // 2
    if nums[mid] == target:
      return mid
    elif target < nums[mid]:
      r = mid - 1
    else:
      l = mid + 1
  return -1

def binary_search2(nums, target):
  if not nums or not target:
    return -1
  l, r = 0, len(nums) - 1
  while l < r:
    mid = (l + r) // 2
    if nums[mid] == target:
      return mid
    elif target < nums[mid]:
      r = mid
    else:
      l = mid + 1
  return l if target == nums[l] else -1

def binary_search3(arr, target):
    left, right, mid = 0, len(arr) - 1, 0
    while left + 1 < right:
        mid = left + (right - left) / 2
        if arr[mid] == target:
            return mid
        elif arr[mid] > target:
            right = mid
        else:
            left = mid
    
    if arr[left] == target:
        return left
    elif arr[right] == target:
        return right
    else: 
        return -1
```

### Source code of bisect

```python
def bisect_right(a, x, lo=0, hi=None):
    """Return the index where to insert item x in list a, assuming a is sorted.
    The return value i is such that all e in a[:i] have e <= x, and all e in
    a[i:] have e > x.  So if x already appears in the list, a.insert(x) will
    insert just after the rightmost x already there.
    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        # since we are looking for an elem that all elems to its left are less than
        # or equal to the current mid (exclusive) then if x < a[mid] means the index
        # we are looking for must at left hand side and it must be the right most
        # element that satisfy above rule
        if x < a[mid]: hi = mid
        else: lo = mid+1
    return lo
    
def bisect_left(a, x, lo=0, hi=None):
    """Return the index where to insert item x in list a, assuming a is sorted.
    The return value i is such that all e in a[:i] have e < x, and all e in
    a[i:] have e >= x.  So if x already appears in the list, a.insert(x) will
    insert just before the leftmost x already there.
    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if a[mid] < x: lo = mid+1
        else: hi = mid
    return lo
```

