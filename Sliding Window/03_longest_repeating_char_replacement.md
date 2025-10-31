# Longest Repeating Character Replacement

You are given a string `s` consisting of only uppercase english characters and an integer `k`. You can choose up to `k` characters of the string and replace them with any other uppercase English character.

After performing at most `k` replacements, return the length of the longest substring which contains only one distinct character.

#### Approach 1
Use a `hashmap` with a `sliding window` and keep (`window_size - max_freq`) is ≤ `k`. Expand the window by moving `right` pointer and update frequency of characters. If the window becomes invalid, shrink from the `left` until valid again. Keep track of the maximum valid window length.

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        freq = {}
        max_len = 0
        max_count = 0
        left = 0
        for right in range(len(s)):
            freq[s[right]] = freq.get(s[right],0) + 1
            max_count = max(max_count, freq[s[right]])
            if k + max_count < right - left + 1:
                freq[s[left]] -= 1
                left += 1
            max_len = max(max_len, right - left + 1)
        return max_len
```

**TC : O(n)**
**SC : O(1) or O(k)**, k is the number of unique characters

#### Approach 2
For each unique character `c`, use `sliding window` to find the longest valid substring with at most `k` replacements. Expand window by moving `right` pointer and count matching characters. If replacements needed exceed `k`, shrink the window from the left. Keep track of the maximum valid window length.

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        unique = set(s)
        max_len = 0
        for c in unique:
            count = left = 0
            for right in range(len(s)):
                if s[right] == c:
                    count += 1
                while right - left +1 - count > k:
                    if s[left] == c:
                        count -= 1
                    left += 1
                max_len = max(max_len, right - left + 1)
        return max_len
```

**TC : O(n k)**, k number of sliding windows
**SC : O(1) or O(k)**, k is the number of unique characters
