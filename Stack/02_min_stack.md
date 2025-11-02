# Minimum Stack

Design a stack class that supports the `push`, `pop`, `top`, and `getMin` operations.

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

Each function should run in O(1).

#### Approach
Use two `stacks` (`stack`, `min_stack` - track current minimum value). When pushing a value, also push `min(value, min_stack[-1])` onto `min_stack`. When popping, remove the top element from both stacks to keep them in sync. The top of `stack` gives the latest value, and the top of `min_stack` gives the minimum.

```python
class MinStack:
    def __init__(self):
        self.stack, self.min_stack = [], []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if self.min_stack: self.min_stack.append(min(self.min_stack[-1], val))
        else: self.min_stack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

**TC : O(1)**
**SC : O(n)**
