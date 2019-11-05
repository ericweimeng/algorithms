# Binary Search and Sweep Line

## Binary Search

```python
def binary_search(arr, target):
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

## Sweep Line

