# Binary Trees - Count Good Nodes Example

## Problem: 1448. Count Good Nodes in Binary Tree
Given the root of a binary tree, count nodes that are "good" — a node is good if no node on the path from the root to it has a greater value.

## What extra state does each call need?
Track the **maximum value seen so far** on the current root-to-node path — call it `maxSoFar`. Define `dfs(node, maxSoFar)` that returns the count of good nodes in the subtree rooted at `node`, given that `maxSoFar` is the largest value encountered on the path leading to `node`.

## Reusing the structural observation from Path Sum
Same idea as [[Binary Trees - Path Sum Example]]: every path from the root through a child of `node` necessarily passes through `node`. So `maxSoFar` should be updated with `node.val` **before** recursing into children — this keeps `maxSoFar` accurate for whichever call receives it.

## Base case
Empty tree → 0 good nodes (nothing to count).

## Combining subtree results
Total good nodes in a subtree = (good nodes in left subtree) + (good nodes in right subtree) + (1, if the current node itself is good). A node is good if `node.val >= maxSoFar`.

## Recursive code
```python
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        def dfs(node, max_so_far):
            if not node:
                return 0

            left = dfs(node.left, max(max_so_far, node.val))
            right = dfs(node.right, max(max_so_far, node.val))
            ans = left + right
            if node.val >= max_so_far:
                ans += 1
            return ans
        return dfs(root, float("-inf"))
```
Initial call starts with `max_so_far = float("-inf")`, guaranteeing the root itself always counts as good (nothing can be greater than negative infinity).

## Iterative code
```python
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        if not root:
            return 0

        stack = [(root, float("-inf"))]
        ans = 0

        while stack:
            node, max_so_far = stack.pop()
            if node.val >= max_so_far:
                ans += 1

            if node.left:
                stack.append((node.left, max(max_so_far, node.val)))
            if node.right:
                stack.append((node.right, max(max_so_far, node.val)))

        return ans
```

## Complexity
**O(n) time, O(n) space** worst case — same reasoning as every other DFS tree problem in this chapter (see [[Binary Trees - Iterative DFS]]).

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Path Sum Example]], [[Binary Trees - Maximum Depth Example]]
