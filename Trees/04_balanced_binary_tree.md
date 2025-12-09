# Balanced Binary Tree

Given a binary tree, return `true` if it is **height-balanced** and `false` otherwise.
A **height-balanced** binary tree is defined as a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

#### Approach
Use a `bottom-up DFS` that returns both whether the subtree is `balanced` and its `height`. For each node, recursively check left and right subtrees; the current node is balanced if both subtrees are balanced and their height difference is at most 1.

```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            if not root:
                return [True, 0]
            left = dfs(root.left)
            right = dfs(root.right)
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, 1 + max(left[1], right[1])]
        return dfs(root)[0]
```

**TC : O(n)**
**SC : O(h)**, h is the maximum depth of the call stack.
