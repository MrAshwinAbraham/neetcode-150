# Subtree of Another Tree

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.

#### Approach
Use a helper function `sameTree` to check if trees are identical. For each node in the main tree, check if `subRoot` matches exactly starting from that node; if not, recursively search in left and right subtrees. Return `True` if a match is found anywhere or if `subRoot` is empty (empty tree is subtree of any tree).

```python
class Solution:  
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        def sameTree(root, subRoot):
            if not root and not subRoot:
                return True
            if root and subRoot and root.val == subRoot.val:
                return sameTree(root.left, subRoot.left) and sameTree(root.right, subRoot.right)
            else: return False
        if not subRoot: return True
        if not root: return False
        if sameTree(root, subRoot): return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
```

**TC : O(m x n)**
**SC : O(m + n)**
