# Koko Eating Bananas

You are given an integer array `piles` where `piles[i]` is the number of bananas in the `ith` pile. You are also given an integer `h`, which represents the number of hours you have to eat all the bananas.

You may decide your bananas-per-hour eating rate of `k`. Each hour, you may choose a pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, you may finish eating the pile but you can not eat from another pile in the same hour.

Return the minimum integer `k` such that you can eat all the bananas within `h` hours.

#### Approach
Use `Binary search` for getting the eating speed from 1 to the largest pile. For each speed, compute how many hours it would take to finish all piles (ceiling division). If she can finish within `h` hours, try a slower speed, otherwise try faster. The smallest speed that still finishes on time is the answer.

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        left, right = 1, max(piles)
        best_speed = right
        while left <= right:
            speed = (left + right)//2
            hours = 0
            for pile in piles:
                hours += (pile + speed -1) // speed #ceiling division
            if hours<=h:
                best_speed = speed
                right = speed - 1
            else: left = speed + 1
        return best_speed
```

**TC : O(n logm)**, m is the size of the largest pile
**SC : O(1)**
