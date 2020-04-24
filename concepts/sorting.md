# Sorting

## Bucket Sort

Bucket sort, or bin sort, is a sorting algorithm that works by partitioning an array into a number of buckets. Each bucket is then sorted individually, either using a different sorting algorithm, or by recursively applying the bucket sorting algorithm.

## Quick Sort

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

## Merge Sort

Key Point for merge sort

* Split
  * To split elements until there's only one element \(base case\) which is sorted
* Merge
  * Merge the sorted two sequences from each subproblem
* Time
  * O\(nlogn\)
* Space 
  * O\(n\)

```python
def merge_sort(a):
    if len(a) > 1:
        mid = len(a) // 2
        left = a[:mid]
        right = a[mid:]
        
        merge_sort(left)
        merge_sort(right)
        
        i = j = k = 0
        
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                a[k] = left[i]
                i += 1
            else:
                a[k] = right[j]
                j += 1
            
            k += 1
        
        while i < len(left):
            a[k] = left[i]
            i += 1
            k += 1
        
        while j < len(right):
            a[k] = right[j]
            j += 1
            k += 1
```

