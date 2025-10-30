# Longest Substring Without Repeating Characters

Given a string `s`, find the _length of the longest substring_ without duplicate characters.
A **substring** is a contiguous sequence of characters within a string.

#### Approach 1
Use `two pointers` to maintain a `sliding window` of **unique characters**. If a duplicate appears, shrink the window from the left until it’s unique again. Add each new character and update the maximum length each step.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        window = set()
        left = 0
        maxLength = 0
        for right in range(len(s)):
            while s[right] in window:
                window.remove(s[left])
                left += 1
            window.add(s[right])
            maxLength = max(maxLength, right - left + 1)
        return maxLength
```

**TC : O(n)**
**SC : O(k)**, k is the number of unique characters

#### Approach 2
Use `sliding window` with two pointers (`left`, `right`). Track the last index of each character in a `hashmap`. When a repeat is found, move `left` to exclude the previous occurrence. Update the maximum window size each step.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = {}
        left = 0
        maxLength = 0
        for right in range(len(s)):
            if s[right] in seen:
                left = max(seen[s[right]]+1, left)
            seen[s[right]] = right
            maxLength = max(maxLength, right - left + 1)
        return maxLength
```

**TC : O(n)**
**SC : O(k)**, k is the number of unique characters
