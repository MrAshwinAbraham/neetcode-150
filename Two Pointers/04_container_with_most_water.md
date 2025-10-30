# Container With Most Water

You are given an integer array `heights` where `heights[i]` represents the height of the `ith` bar.
You may choose any two bars to form a container. Return the _maximum_ amount of water a container can store.

#### Approach
Use `two pointers` at both ends. Compute `area` at each step and update the `maximum area`. **Move the pointer at the shorter line inward** to find a potentially larger area. Continue until the pointers meet.

```python
class Solution:
    def maxArea(self, heights: List[int]) -> int:
        maxArea = 0
        left, right = 0, len(heights)-1
        while left < right:
            area = min(heights[left], heights[right]) * (right - left)
            maxArea = max(maxArea, area)
            if heights[left] < heights[right]:
                left += 1
            else:
                right -= 1
        return maxArea
```

**TC : O(n)**
**SC : O(1)**
