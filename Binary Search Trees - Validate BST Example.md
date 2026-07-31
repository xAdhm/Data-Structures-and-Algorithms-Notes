# Binary Search Trees - Validate BST Example

## Problem: 98. Validate Binary Search Tree
Given the root of a binary tree, determine whether it's a valid BST.

## What extra state does each call need?
The [[Binary Search Trees - Overview|BST property]] is relative — a node's value isn't checked against a fixed rule, but against the range implied by its **ancestors**. Track an allowed `(small, large)` range as an argument: `small < node.val < large` must hold.

**Root's range:** the root has no parent, so it can hold *any* value — initialize `small = -infinity`, `large = infinity`.

**Updating the range going down:**
- Recursing into the **left** subtree: those values must all be less than the current node → update `large = node.val`
- Recursing into the **right** subtree: those values must all be greater than the current node → update `small = node.val`

## The recursive structure — same idea as Same Tree
Directly parallels [[Binary Trees - Same Tree Example]]: since a tree is only a valid BST if *every* subtree is also a valid BST (the BST property applies "at any given node," per the definition), `isValidBST` needs to call itself on both children and require **both** to return true, in addition to the current node satisfying its own range check.

```
isValidBST(node.left) AND isValidBST(node.right) AND (small < node.val < large)
```

## Base case
Empty tree → `True`. An empty tree is trivially a valid BST. This also correctly handles single-node trees: a lone node's range check passes (assuming valid input), and both its (empty) child calls hit this base case and return `True`.

## Recursive code
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def dfs(node, small, large):
            if not node:
                return True

            if not (small < node.val < large):
                return False
            left = dfs(node.left, small, node.val)
            right = dfs(node.right, node.val, large)
            # tree is a BST if left and right subtrees are also BSTs
            return left and right
        return dfs(root, float("-inf"), float("inf"))
```

Because each recursive call keeps its own independent copy of `small`/`large`, the constraint stays accurate for every node, regardless of how deep it is or which path led there (same per-call-independence principle used throughout the [[Binary Trees - DFS Overview|DFS chapter]]).

## Iterative code
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        stack = [(root, float("-inf"), float("inf"))]
        while stack:
            node, small, large = stack.pop()
            if not (small < node.val < large):
                return False

            if node.left:
                stack.append((node.left, small, node.val))
            if node.right:
                stack.append((node.right, node.val, large))

        return True
```
Each stack entry bundles a node with its own `(small, large)` range — the iterative equivalent of each recursive call's independent local state.

## Complexity
**O(n) time, O(n) space** — standard bounds for any DFS-style tree traversal (see [[Binary Trees - Iterative DFS]]).

#dsa #algorithms #trees #binary-search-trees #recursion

Related: [[Binary Search Trees - Overview]], [[Binary Trees - Same Tree Example]]
