# Binary Search

You are given an array of **distinct** integers `nums`, sorted in ascending order, and an integer `target`. Implement a function to search for `target` within `nums`. If it exists, then return its index, otherwise, return `-1`.

Your solution must run in O(logn) time.

#### Approach
Use two pointers, `l` and `r` at both ends of the array. While `l` <= `r`, calculate mid and compare `nums[mid]` to target. If equal return `mid`, if smaller, move `l` to `mid + 1` else move `r` to `mid - 1`. If the loop ends without finding the target, return `-1`.

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l<=r:
            mid = l + (r - l) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                l = mid + 1
            else:
                r = mid - 1
        return -1
```

**TC : O(logn)**
**SC : O(1)**
