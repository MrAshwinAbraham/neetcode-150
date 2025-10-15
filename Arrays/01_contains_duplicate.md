## Contains Duplicate

Given an integer array `nums`, return `true` if any value appears **more than once** in the array, otherwise return `false`.

#### Approach
Use a `set` to add unique elements and compare if the element you're trying to add is already present.

```python
class Solution:
    def hasDuplicate(self, nums: List[int]) -> bool:
        numSet = set()
        for num in nums:
            if num in numSet:
                return True
            else:
                numSet.add(num)
        return False
```

**TC : O(n)**
**SC : O(n)**
