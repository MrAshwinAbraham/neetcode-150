# Valid Parentheses

You are given a string `s` consisting of the following characters: `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`.

The input string `s` is valid if and only if:
1. Every open bracket is closed by the same type of close bracket.
2. Open brackets are closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

Return `true` if `s` is a valid string, and `false` otherwise.

#### Approach
Use a `map` to store all bracket pairs and `stack` to keep track of all the opening brackets. Check if the closing bracket matches with the opening one if so pop, else return `false`. In the end if stack empty return `true`.

```python
class Solution:
    def isValid(self, s: str) -> bool:
        mapping = {")":"(", "}":"{", "]":"["}
        stack = []
        for c in s:
            if c in mapping:
                if not stack or mapping[c] != stack[-1]:
                    return False
                stack.pop()
            else:
                stack.append(c)
        return stack == []
```

**TC : O(n)**
**SC : O(n)**
