# Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements within the array. The test cases are generated such that the answer is always **unique**.

You may return the output in **any order**.

#### Approach 1
Count frequencies using `Counter(nums)`. Store numbers in `buckets` where `index = frequency`. Iterate in `reverse` (highest to lowest frequency) and collect the top `k` elements. As soon as you reach `k`, you `return topK` immediately.

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        bucket = [[] for _ in range(len(nums) + 1)]
        count = Counter(nums)
        topK = []
        for num, freq in count.items():
            bucket[freq].append(num)
        for i in range(len(nums),0,-1):
            for num in bucket[i]:
                topK.append(num)
                if len(topK) == k:
                    return topK
        return topK
```

**TC : O(n)**
**SC : O(n)**

#### Approach 2
Count frequencies using `Counter(nums)`. Use a `min-heap` to push in the `frequency` and `number` from the `Counter` as an array. Pop out the elements to keep `len(heap)==k`. Add the numbers to `topK` and `return` immediately.

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = Counter(nums)
        heap = []
        topK = []
        for num, freq in count.items():
            heapq.heappush(heap, (freq, num))
            if len(heap) > k:
                heapq.heappop(heap)
        for i in range(k):
            topK.append(heapq.heappop(heap)[1])
        return topK
```

**TC : O(n logk)**
**SC : O(n + k)**
