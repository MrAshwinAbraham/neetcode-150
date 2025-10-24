# Encode and Decode Strings

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement `encode` and `decode`

#### Approach
For each string in the list, append its length, a delimiter (`#`), and the string itself to form one long encoded string.  
While decoding, iterate the string using two pointers`i` and `j`: move `j` until the delimiter `#` to extract the length, then use it to slice out the original string and add it to the result list.

```python
class Solution:
    def encode(self, strs: List[str]) -> str:
        res = ""
        for s in strs:
            res += str(len(s)) + "#" + s
        return res

    def decode(self, s: str) -> List[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != "#":
                j += 1
            length = int(s[i:j])
            i = j + 1
            j = i + length
            res.append(s[i:j])
            i = j
        return res
```

**TC : O(N)**, N is the total number of characters (N = sum(len(s) for s in strs))
**SC : O(N)**
