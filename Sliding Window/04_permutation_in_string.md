# Permutation in String

You are given two strings `s1` and `s2`. Return `true` if `s2` contains a permutation of `s1`, or `false` otherwise. That means if a permutation of `s1` exists as a substring of `s2`, then return `true`.

Both strings only contain lowercase letters.

#### Approach
Use a **sliding window** of size `len(s1)`. First, count the character frequencies of `s1` and the first window in `s2`. Slide the window one character at a time, update the counts by adding the new `right` character and removing the old `left` one. If at any point the two frequency maps match, return `True`, otherwise, return `False`.

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        n, m = len(s1), len(s2)
        if n > m:
            return False
        target = Counter(s1)
        window = Counter(s2[:n])
        if target == window: return True
        for r in range(n, m):
            l = r - n
            window[s2[r]] += 1
            window[s2[l]] -= 1
            if window[s2[l]] == 0:
                del window[s2[l]]
            l += 1
            if target == window:
                return True
        return False
```

**TC : O(m)**, m is the length of longer string `s2`
**SC : O(1) or O(k)**, k is the number of unique characters(maximum 26)
