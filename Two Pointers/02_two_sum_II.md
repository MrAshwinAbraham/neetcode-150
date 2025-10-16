# Two Sum II

Given an array of integers `numbers` that is sorted in **non-decreasing order**.

Return the indices (**1-indexed**) of two numbers, `[index1, index2]`, such that they add up to a given target number `target` and `index1 < index2`. Note that `index1` and `index2` cannot be equal, therefore you may not use the same element twice.

There will always be **exactly one valid solution**. Your solution must use O(1)O(1) additional space.

#### Approach
Use 2 pointers, one from each end that converge towards the middle and check if the sum of numbers at those indices add upto the target, increment left or decrement right accordingly.

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers)-1
        while l<r:
            curSum = numbers[l] + numbers[r]
            if curSum == target:
                return [l+1, r+1]
            elif curSum > target:
                r -= 1
            else:
                l += 1
        return []
```

**TC : O(n)**
**SC : O(1)**
