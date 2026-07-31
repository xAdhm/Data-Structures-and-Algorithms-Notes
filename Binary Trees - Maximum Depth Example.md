# Binary Trees - Maximum Depth Example

## Problem: 104. Maximum Depth of Binary Tree
Given the root of a binary tree, find the length of the longest path from the root to a leaf.

**Note on definitions:** [[Binary Trees - Terminology|the usual definition]] has the root at depth 0, but this specific LeetCode problem effectively starts counting at 1 (since it's counting *nodes* on the root-to-leaf path, and the root itself counts as one of them).

## Thinking recursively
**Base case:** an empty tree (0 nodes, `root` is `None`) has depth 0 — no nodes, no path.

**Relationship between a node and its children:** since a root-to-leaf path can only go through *one* child at a time (not both), the max depth of the whole tree rooted at the current node is: `1 + max(maxDepth(left subtree), maxDepth(right subtree))`. The `+1` accounts for the current node itself contributing one step to whichever path is chosen.

This directly uses the [[Binary Trees - Subtrees|subtree]] principle: `maxDepth(root.left)` returns "the longest root-to-leaf path *starting from the left child*" — exactly what's needed, since `maxDepth` is defined identically regardless of which node it's called on.

## Tracing through a leaf
Calling `maxDepth` on a leaf: both `maxDepth(leaf.left)` and `maxDepth(leaf.right)` hit the base case and return 0 → leaf's result = `1 + max(0, 0) = 1`. Makes sense: a leaf treated as its own subtree has exactly one node on its longest path (itself).

Moving back up to the leaf's parent: if the leaf was the only child (say, the left one), the parent's result = `1 + max(1, 0) = 2`. **The `+1` propagates upward from the leaves to the root**, accumulating the total depth as the recursion unwinds.

**Key recursion reminder:** every function call has its own independent local variables — every node in the tree has its own separate `left`/`right` values computed during its own call, even though many calls exist on the stack simultaneously.

## Recursive code
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        left = self.maxDepth(root.left)
        right = self.maxDepth(root.right)
        return max(left, right) + 1
```

This is technically a **postorder** traversal — the "logic" (the return statement combining left/right) happens *after* both recursive calls.

## Iterative code (preorder-style, using a stack)
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        stack = [(root, 1)]
        ans = 0

        while stack:
            node, depth = stack.pop()
            ans = max(ans, depth)
            if node.left:
                stack.append((node.left, depth + 1))
            if node.right:
                stack.append((node.right, depth + 1))

        return ans
```
Each stack entry pairs a node with its depth, since the recursive version's "free" per-call depth tracking has to be made explicit iteratively (see [[Binary Trees - Iterative DFS]]).

## Complexity
**O(n) time, O(n) space** (worst case — straight-line tree), per the general reasoning in [[Binary Trees - Iterative DFS]].

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - DFS Overview]], [[Binary Trees - Iterative DFS]]
