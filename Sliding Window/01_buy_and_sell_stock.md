# Best Time to Buy and Sell Stock

You are given an integer array `prices` where `prices[i]` is the price of stock on the `ith` day.
You may choose a **single day** to buy one stock and choose a **different day in the future** to sell it.

Return the maximum profit you can achieve. You may choose to **not make any transactions**, in which case the profit would be `0`.

#### Approach
Use a sliding window with 2 pointers `l` and `r`. If price at `r` greater than that at `l` and the difference in price greater than max profit yet, update max profit. Otherwise move `l` to `r`.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l = 0
        maxProf = 0
        for r in range(1, len(prices)):
            if prices[r] > prices[l]:
                maxProf = max(maxProf, (prices[r] - prices[l]))
            else:
                l = r
        return maxProf
```

**TC : O(n)**
**SC : O(1)**
