# Longest Consecutive Sequence

Given an array of integers `nums`, return _the length_ of the longest consecutive sequence of elements that can be formed.

A _consecutive sequence_ is a sequence of elements in which each element is exactly `1` greater than the previous element. The elements do _not_ have to be consecutive in the original array.

You must write an algorithm that runs in `O(n)` time.

#### Approach
Store all numbers in a `set` for O(1) lookups. For each number, only start counting if it’s the **start** of a sequence (`num-1` not in `set`). Count consecutive numbers forward and track the maximum streak length.

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        unique = set(nums)
        longest = 0
        for num in unique:
            if num-1 not in unique:
                count = 1
                while num + count in unique:
                    count += 1
                longest = max(longest, count)
        return longest
```

**TC : O(n)**
**SC : O(n)**
