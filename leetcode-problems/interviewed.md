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

## Remove duplicates that exceeded limit

```python
"""
'aaabbba', 2 -> aabba
"""
import unittest

def remove_duplicates(s, limit):
    if not s:
        return ''

    if not limit:
        return s

    last_char = s[0]
    res = s[0]
    i = 1
    count = 1

    while i < len(s):
        if s[i] == last_char:
            if count < limit:
                res += s[i]
            count += 1
            i += 1
        else:
            last_char = s[i]
            res += s[i]
            count = 1
            i += 1

    return res

# print(remove_duplicates('aaabbba', 2))

class TestRemoveDuplicates(unittest.TestCase):

    def test_remove_duplicates(self):
        self.assertEqual(remove_duplicates('aaabbba', 2), 'aabba')
        self.assertEqual(remove_duplicates('', 2), '')
        self.assertEqual(remove_duplicates('aaabbba', 0), 'aaabbba')
        self.assertEqual(remove_duplicates('aaabbba', 1), 'aba')
        self.assertEqual(remove_duplicates('aaabbba', 7), 'aaabbba')

if __name__ == '__main__':
    unittest.main()
```

## Remove Alternate Duplicates

> """ Remove Alternate Duplicate characters from a char array you have to do it in Place.Like keeping only the odd occurences of each character. Example: Input: “you got beautiful eyes”
>
> Output: ”you gt beaiful es” Allowed Time Complexity was O\(n\) and Space Complexity was O\(1\) """

```python
def remove_even_char(s):
    if not s:
        return ''

    s = list(s)
    orr = set()
    for i, c in enumerate(s):
        if c not in orr:
            orr.add(c)
        else:
            s[i] = ''
            orr.remove(c)
    return ''.join(ls)


print(remove_even_char('you got beautiful eyes'))
```

