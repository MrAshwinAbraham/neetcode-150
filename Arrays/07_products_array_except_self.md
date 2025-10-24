# Products of Array Except Self

Given an integer array `nums`, return an array `output` where `output[i]` is the product of all the elements of `nums` except `nums[i]`. Each product is **guaranteed** to fit in a **32-bit** integer.

Follow-up: Could you solve it in O(n)O(n) time without using the division operation?

#### Approach
Traverse array from left to right to compute `prefix` values, storing at each index of the `result` array. Then from right to left to multiply each stored `prefix` with `postfix` values. This two-pass method ensures each index holds the product of all elements except itself, return `result`.

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        product = [1] * len(nums)
        prefix = 1
        for i in range(len(nums)):
            product[i] *= prefix
            prefix = nums[i] * prefix
        postfix = 1
        for i in range(len(nums)-1,-1,-1):
            product[i] *= postfix
            postfix = nums[i] * postfix
        return product
```

**TC : O(n)**
**SC : O(1)**
