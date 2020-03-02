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

