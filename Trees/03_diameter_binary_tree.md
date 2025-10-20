# Diameter of Binary Tree

The **diameter** of a binary tree is defined as the **length** of the longest path between _any two nodes within the tree_. The path does not necessarily have to pass through the root.

The **length** of a path between two nodes in a binary tree is the number of edges between the nodes. Note that the path can _not_ include the same node twice.

Given the root of a binary tree `root`, return the **diameter** of the tree.

#### Approach
Do a `DFS` to recursively calculate the height of each node. During traversal, update a global `result` by computing the diameter at each node and keep track of the maximum diameter found so far. Return `result`.

```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.res = 0
        def dfs(cur):
            if not cur:
                return 0
            left = dfs(cur.left)
            right = dfs(cur.right)
            self.res = max(self.res, (left + right))
            return 1 + max(left, right)
        dfs(root)
        return self.res
```

**TC : O(n)**
**SC : O(h)**, h is the maximum depth of the call stack.
