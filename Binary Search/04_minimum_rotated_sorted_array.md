# Find Minimum in Rotated Sorted Array

You are given an array of length `n` which was originally sorted in ascending order. It has now been **rotated** between `1` and `n` times. For example, the array `nums = [1,2,3,4,5,6]` might become:

- `[3,4,5,6,1,2]` if it was rotated `4` times.
- `[1,2,3,4,5,6]` if it was rotated `6` times.

Notice that rotating the array `4` times moves the last four elements of the array to the beginning. Rotating the array `6` times produces the original array.

Assuming all elements in the rotated sorted array `nums` are **unique**, return the minimum element of this array.

A solution that runs in `O(n)` is trivial, write an algorithm that runs in `O(log n) time`?

#### Approach
Use `Binary Search` because the array is rotated, one half is always sorted. Compare `nums[mid]` and `nums[right]` to decide which half contains the rotation (the minimum). If `nums[mid] > nums[right]`, search the right half, otherwise search the left half. When the pointers meet, that index holds the minimum element.

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums)-1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                right = mid
        return nums[left]
```

**TC : O(logn)**
**SC : O(1)**
