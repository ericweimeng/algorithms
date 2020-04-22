# Sorting

### Bucket Sort

Bucket sort, or bin sort, is a sorting algorithm that works by partitioning an array into a number of buckets. Each bucket is then sorted individually, either using a different sorting algorithm, or by recursively applying the bucket sorting algorithm.

### Quick Sort

### Version 1

```python
def quick_sort(a, i, j):
    if a and i < j:
        pivot = partition(a, i, j)
        
        quick_sort(a, i, pivot - 1)
        quick_sort(a, pivot + 1, j)
    
def partition(a, lo, hi):
    i = j = lo
    pivot = a[hi]
    while j < hi:
        if a[j] < pivot:
            a[i], a[j] = a[j], a[i]
            i += 1
        j += 1
    a[i], a[hi] = a[hi], a[i]
    return i
```

### Version 2

```python
def quick_sort(nums):
    _sort(nums, 0, len(nums) - 1)
    
def _sort(nums, low, high):
    if low < high:
        pivot = partition(nums, low, high)
        
        _sort(nums, low, pivot - 1)
        _sort(nums, pivot + 1, high)
        
def partition(array, low, high):
    i = low - 1
    pivot = array[high]
    
    for j in range(low, high):
        if array[j] < pivot:
            i += 1
            array[i], array[j] = array[j], array[i]
    array[i + 1], array[high] = array[high], array[i + 1]
    return i + 1

if __name__ == '__main__':
    
    nums = [4, 7, 6, 1, 3, 9, 5, 8, 7, 5]
    quick_sort(nums)
    print(nums)
```

