# Binary Trees - Lowest Common Ancestor Example

⚠️ Bonus/classic problem, noticeably harder than the other examples in this chapter — don't be discouraged if it doesn't click immediately.

## Problem: 236. Lowest Common Ancestor of a Binary Tree
Given the root of a binary tree and two nodes `p` and `q` known to be in the tree, find their **lowest common ancestor (LCA)** — the lowest node that has both `p` and `q` as descendants (a node counts as its own descendant).

## Base case
Empty tree → no LCA exists → return `None`.

## The three possibilities at any given node
1. **The current node itself is `p` or `q`.** The answer can't be strictly below this node — going lower would mean losing this node (which is one of the two targets) as a required descendant of the answer. So this node is the best candidate so far.
2. **`p` is in the left subtree, `q` is in the right subtree (or vice versa).** The current node **must** be the LCA — it's the exact point where the two searches "meet," and it's the lowest such connection point.
3. **Both `p` and `q` are in the same subtree** (both left, or both right). The current node is *not* the answer — a lower node within that subtree could still be the LCA, so we need to look deeper.

## Turning this into recursion
- **Case 1:** if the current node is `p` or `q`, return the node itself immediately — no need to check subtrees at all, since we already know the answer can't be found below.
- Recursively call on both `node.left` and `node.right`. A call returns **non-`None`** only if `p` or `q` (or both) exist in that subtree; it returns `None` if neither is present.
- **Case 2 (implied):** if *both* the left and right calls return non-`None`, the current node is the LCA — return it.
- **Case 3 (implied):** if only *one* call returns non-`None`, that result is the answer — propagate it upward.

## Code
```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root:
            return None

        # first case
        if root == p or root == q:
            return root

        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        # second case
        if left and right:
            return root

        # third case
        if left:
            return left

        return right
```

**Implementation subtlety:** it might seem like "if `left` is `None`, `right` must be non-`None`" — but that's not strictly true; both could legitimately be `None` if the current subtree contains neither `p` nor `q`. The code still works correctly despite this, because if both are `None`, `right` (which is also `None`) gets returned — exactly the desired behavior, since a subtree containing neither target should propagate `None` upward.

## Complexity
**O(n) time, O(n) space** worst case (call stack) — same reasoning as the rest of this chapter (see [[Binary Trees - Iterative DFS]]). An iterative version exists but is significantly more cumbersome than the recursive one — not covered here.

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Same Tree Example]], [[Binary Trees - Subtrees]]
