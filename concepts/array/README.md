# Array

## Knowledge points

* List addition creates new list
  * e.p. a = \[1\], a + \[2\] creates new list \[1, 2\], but a stays the same \[1\]
* List pop is slow and create O\(k\) space when do pop\(k\), use deque instead
  * list.pop\(\[i\]\)

    Remove the item at the given position in the list, and return it. If no index is specified, `a.pop()` removes and returns the last item in the list.

  * Essentially, a Python `list` is implemented as an array of pointers. The `list.pop(k)` first removes and returns the element at `k`, and then moves all the elements beyond `k` one position up.
  * [https://medium.com/@shuangzizuobh2/how-well-do-you-code-python-9bec36bbc322](https://medium.com/@shuangzizuobh2/how-well-do-you-code-python-9bec36bbc322)



