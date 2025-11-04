# Daily Temperatures

You are given an array of integers `temperatures` where `temperatures[i]` represents the daily temperatures on the `ith` day.

Return an array `result` where `result[i]` is the number of days after the `ith` day before a warmer temperature appears on a future day. If there is no day in the future where a warmer temperature will appear for the `ith` day, set `result[i]` to `0` instead.

#### Approach
Use a `monotonic decreasing stack` that stores pairs of `(index, temperature)` while iterating through list. When current `temperature` is higher than the top of the `stack`, we `pop` from the `stack` and add the **difference between their indices** as the number of days for that index. After that push the current day onto the stack, ensuring each element is processed only once.

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        n = len(temperatures)
        result = [0] * n
        stack = [] # stores (index, temperature)
        for i,t in enumerate(temperatures):
            while stack and t > stack[-1][1]:
                ind, temp = stack.pop()
                result[ind] = i - ind
            stack.append((i,t))
        return result
```

**TC : O(n)**
**SC : O(n)**
