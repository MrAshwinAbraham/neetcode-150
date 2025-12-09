# Same Binary Tree

Given the roots of two binary trees `p` and `q`, return `true` if the trees are **equivalent**, otherwise return `false`.
Two binary trees are considered **equivalent** if they share the exact same structure and the nodes have the same values.

#### Approach
Recursively check if two trees p and q are identical. If both nodes are None trees are same, return `True`. If both exist and have same value, recursively check left and right subtrees. Otherwise not the same, return `False`

```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p and not q:
            return True
        if p and q and p.val == q.val:
            return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        else:
            return False
```

**TC : O(n)**
**SC : O(n)**
