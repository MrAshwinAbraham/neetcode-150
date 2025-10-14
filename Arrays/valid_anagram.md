## Valid Anagram

Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.

An **anagram** is a string that contains the exact same characters as another string, but the order of the characters can be different.

#### Approach 1
Use 2 `map`'s to count the number of each characters present in each and check if they are equal.

```python
class Solution:

    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
            
        countS, countT = {}, {}
        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i],0)
            countT[t[i]] = 1 + countT.get(t[i],0)
        return countS == countT
```

**TC : O(n)**
**SC : O(k)**, k is the number of unique characters in the string.
#### Approach 2
Use a `character array` to keep track of the characters, add if in `s` and subtract if in `t`, finally if everything is `0`, return `true`.

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        count = [0] * 26
        for i in range(len(s)):
            count[ord(s[i])-ord('a')] += 1
            count[ord(t[i])-ord('a')] -= 1
        for val in count:
            if val != 0:
                return False
        return True
```

**TC : O(n)**
**SC : O(1)**, maximum size of the array will be 26.
