# Interviewed

## Merge Sorted Arrays

> **Given two sorted lists of unique integers, please write a method to merge the two lists into one sorted list. For example,** 
>
> **list1: 1, 4, 5, 12, 33, 45, …**
>
> **list2: 2, 5, 7, 15, ...**

```python
def merge_two_arrays(arr1, arr2):
    if not arr1 and not arr2:
        return []
    if not arr1 or not arr2:
        return arr2 or arr1
    
    res = []
    i = j = 0

    while i < len(arr1) and j < len(arr2):
        if arr1[i] < arr2[j]:
            res.append(arr1[i])
            i += 1
        else:
            res.append(arr2[j])
            # if arr1[i] == arr2[j]:
            #     i += 1
            j += 1

    if i < len(arr1):
        res += arr1[i:]
    
    if j < len(arr2):
        res += arr2[j:]

    return res

print(merge_two_arrays([1, 4, 5, 12, 33, 45], [2, 5, 7, 88, 88]))
```

### **Followup**

What if we want to remove duplicates in final result?

```python
def merge_two_arrays(arr1, arr2):
    if not arr1 and not arr2:
        return []
    if not arr1 or not arr2:
        return arr2 or arr1
    
    res = []
    i = j = 0

    while i < len(arr1) and j < len(arr2):
        if arr1[i] < arr2[j]:
            res.append(arr1[i])
            i += 1
        else:
            res.append(arr2[j])
            if arr1[i] == arr2[j]:
                i += 1
            j += 1

    if i < len(arr1):
        res += get_distinct_arr(arr1[i:], i)
    
    if j < len(arr2):
        res += get_distinct_arr(arr2[j:], j)

    return res

def get_distinct_arr(arr, idx):
    tmp = []
    if not arr:
        return tmp
    if len(arr[idx:]) == 1:
        tmp = arr[idx:]
    else:
        tmp += [arr[0]]
        i = 1
        while i < len(arr[idx:]):
            if arr[i] != arr[i - 1]:
                tmp.append(arr[i])
            i += 1
    return tmp

print(merge_two_arrays([45, 88, 100], [83, 88, 100]))
```

