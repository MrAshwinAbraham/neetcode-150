# Maximum Depth of Binary Tree

Given the `root` of a binary tree, return its **depth**.

The **depth** of a binary tree is defined as the number of nodes along the longest path from the root node down to the farthest leaf node.

#### Approach
Recursively calculates the maximum depth of the `left` and `right` subtrees from the `root` node. Return the greater of the two and add 1, with the base case being that an empty node has a depth of 0.

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

**TC : O(n)**
**SC : O(h)**, h is the maximum depth of the call stack.
