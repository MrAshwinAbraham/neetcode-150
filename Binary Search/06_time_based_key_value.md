# Time Based Key-Value Store

Implement a time-based key-value data structure that supports:
- Storing multiple values for the same key at specified time stamps
- Retrieving the key's value at a specified timestamp

Implement the `TimeMap` class:
- `TimeMap()` Initializes the object.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns the most recent value of `key` if `set` was previously called on it _and_ the most recent timestamp for that key `prev_timestamp` is less than or equal to the given timestamp (`prev_timestamp <= timestamp`). If there are no values, it returns `""`.

Note: For all calls to `set`, the timestamps are in strictly increasing order.

#### Approach
Use a `dictionary` mapping each key to a list of `[value, timestamp]` pairs, stored in chronological order. When using `set()`, append the new value with its timestamp.  
When using `get()`, perform a binary search on the list to find the value with the **largest timestamp ≤ given timestamp**(similar to lower bound). Return that value or an empty string if none exists.

```python
class TimeMap:
    def __init__(self):
        self.keyStore = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.keyStore:
            self.keyStore[key] = []
        self.keyStore[key].append([value,timestamp])

    def get(self, key: str, timestamp: int) -> str:
        res = ""
        values = self.keyStore.get(key,[])
        left, right = 0, len(values)-1
        while left <= right:
            mid = (left + right) // 2
            if values[mid][1] <= timestamp:
                res = values[mid][0]
                left = mid + 1
            else:
                right = mid - 1
        return res
```

**TC : `set()` →O(1), `get()` →O(logn)**
**SC : O(n)**
