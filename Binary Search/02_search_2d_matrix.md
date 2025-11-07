# Search a 2D Matrix

You are given an `m x n` 2-D integer array `matrix` and an integer `target`.
- Each row in `matrix` is sorted in _non-decreasing_ order.
- The first integer of every row is greater than the last integer of the previous row.

Return `true` if `target` exists within `matrix` or `false` otherwise.
Can you write a solution that runs in `O(log(m * n))` time?

#### Approach
Treat the matrix as a `sorted 1D array`. Use `binary search`  mapping each mid index to its row and column using `//` and `%`. If the value at that position is less than target, move search to right half; if greater, move to left half. If equal, return `True`. If you can't the value, return `False`.

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows, cols = len(matrix), len(matrix[0])
        left, right = 0, rows * cols - 1
        while left <= right:
            mid = (left + right)//2
            val = matrix[mid // cols][mid % cols]
            if val == target:
                return True
            elif val < target:
                left = mid + 1
            else:
                right = mid - 1
        return False
```

**TC : O(log(mn))**
**SC : O(1)**
