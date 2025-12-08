# Find the Duplicate Number

You are given an array of integers `nums` containing `n + 1` integers. Each integer in `nums` is in the range `[1, n]` inclusive.

Every integer appears **exactly once**, except for one integer which appears **two or more times**. Return the integer that appears more than once.

Follow-up: Can you solve the problem **without** modifying the array `nums` and using O(1)O(1) extra space?

#### Approach 1
Treat the array as a `linked list` where each index points to `nums[i]`, which guarantees a **cycle** due to the duplicated value. Use Floyd’s algorithm to first find an **intersection** inside the cycle. Then reset one pointer to the start and move both one step at a time, the point where they meet is the **cycle entrance**, which is the **duplicate number**.

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        #phase 1: Intersection
        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
        #phase 2: Find cycle entrance
        slow = 0
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        return slow
```

**TC : O(n)**
**SC : O(1)**
