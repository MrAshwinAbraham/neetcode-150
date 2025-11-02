# Evaluate Reverse Polish Notation

You are given an array of strings `tokens` that represents a **valid** arithmetic expression in Reverse Polish Notation.

Return the integer that represents the evaluation of the expression.

- The operands may be integers or the results of other operations.
- The operators include `'+'`, `'-'`, `'*'`, and `'/'`.
- Assume that division between integers always truncates toward zero.

#### Approach
Use a stack to evaluate the Reverse Polish Notation expression. Traverse each token: if it’s a number, push it onto the stack; if it’s an operator, pop the top two elements, apply the operation (`a op b`), and push the result back. Continue this until all tokens are processed — the final value in the stack is the result.

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for token in tokens:
            if token in "+-*/":
                b, a = stack.pop(), stack.pop()
                if token == "+":
                    stack.append(a + b)
                elif token == "-":
                    stack.append(a - b)
                elif token == "*":
                    stack.append(a * b)
                else:
                    stack.append(int(a / b))
            else:
                stack.append(int(token))
        return stack[-1]
```

**TC : O(n)**
**SC : O(n)**
