# Car Fleet

There are `n` cars traveling to the same destination on a one-lane highway.

You are given two arrays of integers `position` and `speed`, both of length `n`.
- `position[i]` is the position of the `ith car` (in miles)
- `speed[i]` is the speed of the `ith` car (in miles per hour)

The **destination** is at position `target` miles.
A car can **not** pass another car ahead of it. It can only catch up to another car and then drive at the same speed as the car ahead of it. A **car fleet** is a non-empty set of cars driving at the same position and same speed. A single car is also considered a car fleet.

If a car catches up to a car fleet the moment the fleet reaches the destination, then the car is considered to be part of the fleet.
Return the number of **different car fleets** that will arrive at the destination.

#### Approach
Sort cars by `position` in reverse after `zipping` `position` and `speed` together. Use a `stack` to track the **time each fleet needs** to reach target. For each car, compute `time=(target-position)/speed`. If `stack` is empty or the `time` is **greater** than time at the top of stack, **push** it. Else, do nothing because the car will eventually catch up to the fleet at the top of the stack. Return the **size** of the stack.

```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        pairs = sorted(zip(position,speed), reverse=True)
        stack = []
        for p,s in pairs:
            time = (target - p)/s
            if not stack or time > stack[-1]:
                stack.append(time)
        return len(stack)
```

**TC : O(n logn)**, because of sorting the pairs
**SC : O(n)**
