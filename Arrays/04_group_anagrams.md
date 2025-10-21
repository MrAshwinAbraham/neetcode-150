# Group Anagrams

Given an array of strings `strs`, group all _anagrams_ together into sublists. You may return the output in **any order**.

An **anagram** is a string that contains the exact same characters as another string, but the order of the characters can be different.

#### Approach 1
Use a `defaultdict(list)` to store `anagrams` as a list mapped to a `sorted` version of it as the key. After iterating and storing the strings in groups, return the groups as a `list`.

```python
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        group = defaultdict(list)
        for s in strs:
            sortedS = "".join(sorted(s))
            group[sortedS].append(s)
        return list(group.values())
```

**TC : O(n k logk)**, k is the length of the string.
**SC : O(n k)**

#### Approach 2
Use a `defaultdict(list)` to store `anagrams` as a list mapped to `tuple` of its `count array` as the key. After iterating and storing the strings in groups, return the groups as a `list`. More optimal since we are not sorting.

```python
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        group = defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c)-ord('a')] += 1
            group[tuple(count)].append(s)
        return list(group.values())
```

**TC : O(n k)**, k is the length of the string.
**SC : O(n k)**
