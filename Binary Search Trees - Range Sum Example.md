# Binary Search Trees - Range Sum Example

## Problem: 938. Range Sum of BST
Given the root of a BST and integers `low`/`high`, return the sum of all node values within the inclusive range `[low, high]`.

## Naive approach vs. BST-aware approach
Naive: plain BFS/DFS visiting every node, summing values in range — works, but ignores the BST's structural guarantees entirely.

**Using the [[Binary Search Trees - Overview|BST property]]:** if the current node's value is **less than** `low`, the entire left subtree is guaranteed to be even smaller (all less than the current node) — so it's pointless to search left at all. Symmetrically, if the current node's value is **greater than** `high`, the entire right subtree can be skipped.

This can eliminate huge portions of the tree without visiting them — e.g. a full tree of a million nodes where the root is already greater than `high` immediately rules out checking the root's entire right subtree (500,000 nodes saved with zero visits).

## Recursive code
```python
class Solution:
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        if not root:
            return 0
        ans = 0
        if low <= root.val <= high:
            ans += root.val
        if low < root.val:
            ans += self.rangeSumBST(root.left, low, high)
        if root.val < high:
            ans += self.rangeSumBST(root.right, low, high)
        return ans
```

## Iterative code
```python
class Solution:
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        stack = [root]
        ans = 0
        while stack:
            node = stack.pop()
            if low <= node.val <= high:
                ans += node.val
            if node.left and low < node.val:
                stack.append(node.left)
            if node.right and node.val < high:
                stack.append(node.right)

        return ans
```

## Complexity
**Worst case still O(n) time** (e.g. all node values happen to fall within `[low, high]`, so nothing gets pruned) — but on average, this performs meaningfully better than visiting every node, thanks to the pruning. **O(n) space** for the recursion/stack in the worst case.

#dsa #algorithms #trees #binary-search-trees #recursion

Related: [[Binary Search Trees - Overview]], [[Binary Search Trees - Validate BST Example]]
