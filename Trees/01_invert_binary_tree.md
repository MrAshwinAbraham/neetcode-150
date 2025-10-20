# Invert Binary Tree

You are given the root of a binary tree `root`. Invert the binary tree and return its root.

#### Approach
Swap `left` and `right` children of the `root` node before recursively calling the function on each of those children to invert their respective subtrees..

```python
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return
        root.left, root.right = root.right, root.left
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root
```

**TC : O(n)**
**SC : O(h)**, h is the maximum depth of the call stack.
