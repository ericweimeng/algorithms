# Optimal Utilization

> Given 2 lists `a` and `b`. Each element is a pair of integers where the first integer represents the unique id and the second integer represents a value. Your task is to find an element from `a` and an element form `b` such that the sum of their values is less or equal to `target` and as close to `target` as possible. Return a list of ids of selected elements. If no pair is possible, return an empty list.
>
> **Example 1:**
>
> ```text
> Input:
> a = [[1, 2], [2, 4], [3, 6]]
> b = [[1, 2]]
> target = 7
>
> Output: [[2, 1]]
>
> Explanation:
> There are only three combinations [1, 1], [2, 1], and [3, 1], which have a total sum of 4, 6 and 8, respectively.
> Since 6 is the largest sum that does not exceed 7, [2, 1] is the optimal pair.
> ```
>
> **Example 2:**
>
> ```text
> Input:
> a = [[1, 3], [2, 5], [3, 7], [4, 10]]
> b = [[1, 2], [2, 3], [3, 4], [4, 5]]
> target = 10
>
> Output: [[2, 4], [3, 2]]
>
> Explanation:
> There are two pairs possible. Element with id = 2 from the list `a` has a value 5, and element with id = 4 from the list `b` also has a value 5.
> Combined, they add up to 10. Similarily, element with id = 3 from `a` has a value 7, and element with id = 2 from `b` has a value 3.
> These also add up to 10. Therefore, the optimal pairs are [2, 4] and [3, 2].
> ```
>
> **Example 3:**
>
> ```text
> Input:
> a = [[1, 8], [2, 7], [3, 14]]
> b = [[1, 5], [2, 10], [3, 14]]
> target = 20
>
> Output: [[3, 1]]
> ```
>
> **Example 4:**
>
> ```text
> Input:
> a = [[1, 8], [2, 15], [3, 9]]
> b = [[1, 8], [2, 11], [3, 12]]
> target = 20
>
> Output: [[1, 3], [3, 2]]
> ```

## Solutions

### Approach \#1

The idea to approach this problem is to sort both array by the value of each pair, then use two pointer to point to the leftmost of the first array and rightmost of the second array and move left/right pointers based on the comparisons of sum to target. Time complexity is O\(m + n + mnlog\(mn\)\), space: O\(m\*n\)

```python
def optimal_utilization(a, b, target):
    if not a or not b:
        return [[]]

    a.sort(key=lambda x: x[1])
    b.sort(key=lambda x: x[1])
    last_sum = float('-inf')
    left, right = 0, len(b) - 1
    res = []
    while left < len(a) and right >= 0:
        sum_value = a[left][1] + b[right][1]
        if sum_value > target:
            right -= 1
        else:
            if last_sum <= sum_value:
                if last_sum < sum_value:
                    res = []
                    last_sum = sum_value
                
                res.append([a[left][0], b[right][0]])
                p = right

                while p > 0 and b[p][1] == b[p - 1][1]:
                    # watch out for add [0] not [1]
                    res.append([a[left][0], b[p - 1][0]])
                    p -= 1
                # move left it gets a new comb, there for cannot assign right to p
                # right = p
            
            left += 1
        
    if not res:
        return [[]]

    return sorted(res)

a = [[1, -8], [2, 15], [3, -9]]
b = [[1, 8], [2, -11], [3, -12]]
target = 1

print(optimal_utilization(a, b, target))
```

```python
import unittest

def optimal_utilization(a, b, target):
    """
    :type a: List[List[int]]
    :type a: List[List[int]]
    :type target: int
    :rtype: List[int]
    """

    temp_value = float('-inf')
    a.sort(key=lambda x: x[1])
    b.sort(key=lambda x: x[1])
    left = 0
    right = len(b) - 1
    res = []

    while left < len(a) and right >= 0:
        sum_value = a[left][1] + b[right][1]

        if sum_value > target:
            right -= 1
        else:
            if temp_value <= sum_value:
                if temp_value < sum_value:
                    res = []
                    temp_value = sum_value
                
                res.append([a[left][0], b[right][0]])
                count = right

                while count > 0 and b[count][1] == b[count - 1][1]:
                    res.append([a[left][0], b[count - 1][0]])
                    count -= 1

            left += 1

    if not res:
        res = [[]]

    return sorted(res)

a = [[1, 8], [2, 15], [3, 9]]
b = []
target = 20

print(optimal_utilization(a, b, target))

class Test(unittest.TestCase):
    try:
        def test_optimal_utilization(self):
            a = [[1, 20], [2, 15], [3, 5]]
            b = [[1, 80], [2, 11], [3, 1]]
            target = 17

            self.assertEqual([[2, 3], [3, 2]], optimal_utilization(a, b, target), "Should return correct list of closes pairs to target when input is unsorted lists")

            a = [[1, 2], [2, 4], [3, 6]]
            b = [[1, 2]]
            target = 7

            self.assertEqual([[2, 1]], optimal_utilization(a, b, target), "Should return correct list of closes pairs to target")

            a = [[1, 3], [2, 5], [3, 7], [4, 10]]
            b = [[1, 2], [2, 3], [3, 4], [4, 5]]
            target = 10
            self.assertEqual([[2, 4], [3, 2]], optimal_utilization(a, b, target),
                            "Should return correct list of closes pairs to target")

            a = [[1, 8], [2, 7], [3, 14]]
            b = [[1, 5], [2, 10], [3, 14]]
            target = 20
            self.assertEqual([[3, 1]], optimal_utilization(a, b, target),
                            "Should return correct list of closes pairs to target")

            a = [[1, 8], [2, 15], [3, 9]]
            b = [[1, 8], [2, 11], [3, 12]]
            target = 20
            self.assertEqual([[1, 3], [3, 2]], optimal_utilization(a, b, target),
                            "Should return correct list of closes pairs to target")

            a = [[1, -8], [2, 15], [3, -9]]
            b = [[1, 8], [2, -11], [3, -12]]
            target = 1
            self.assertEqual([[1, 1]], optimal_utilization(a, b, target),
                            "Should return correct list of closes pairs to target when inputs have negative numbers")

            a = []
            b = [[1, 8], [2, 11], [3, 12]]
            target = 20
            self.assertEqual([[]], optimal_utilization(a, b, target),
                            "Should return empty list when a is empty list")

            a = [[1, 8], [2, 15], [3, 9]]
            b = []
            target = 20
            self.assertEqual([[]], optimal_utilization(a, b, target),
                            "Should return empty list when b is empty list")

            a = []
            b = []
            target = 20
            self.assertEqual([[]], optimal_utilization(a, b, target),
                            "Should return empty list when a and b is empty list")
    except Exception as e:
        print(e)

# if __name__ == '__main__':
#     unittest.main()
```

